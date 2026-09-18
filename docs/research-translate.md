# Translation (ru ↔ en)

> Current runtime (2026-09-16): desktop and MCP translation share the primary LLM. The separate-process topology and third tray section below are historical proposals, superseded by [configuration decisions](../configuration-decisions.md#desktop-and-shared-inference--2026-09-16). Evaluation evidence remains valid; see [current operation](../desktop-translation.md).

Historical design and candidate evaluation for Russian ↔ English translation. Decisions were settled in a
design review on 2026-09-15 and revised after the source review in
[translate-review-sources.md](translate-review-sources.md) on 2026-09-16; see
"Review response" for what changed. The evaluation has been run; recorded results and remaining quality-judging limitations appear under "Results".

## Scope and shape

- Russian ↔ English only, both directions weighted equally.
- Two request shapes: an interactive sentence or paragraph, and batches of
  roughly ten pages arriving as one text.
- Exposed as an MCP `translate` tool, so every client gets the same
  capability and the tool owns the prompt format per model.

## The machine this runs on

| Resource | Value | Consequence |
| --- | --- | --- |
| GPU | RTX 3060, 12 GiB; ~10.9 GiB free with the desktop up | Everything that runs must fit here |
| CPU | Xeon E5-2620 v3 (2014), 6 cores, AVX2, ~40 GB/s memory bandwidth | Weights that spill to RAM cost ~1 token/s — measured, not estimated |
| RAM | 31 GiB, ~11 GiB available | Rules out MoE expert offload for anything over ~10 GB |

The primary model is Qwen3-8B-UD-Q5_K_XL at 32K context. **Measured** with it
loaded and idle on 2026-09-15: 7897 MiB used, **4014 MiB free** (the estimate
of 5.47 GiB weights + ~1.35 GiB KV + ~0.5 GiB buffers came to 7.3 GiB; the
measurement is what counts). There is no fit margin to subtract: both
processes run with `--fit off`, so `--fit-target` is inert. The headroom rule
is instead explicit — **leave at least 1 GiB free under load** — which makes
the translator's working budget **about 3 GiB** for weights plus its own
caches. That figure is an idle snapshot; "Evaluate before choosing" includes
the measurement under load that turns it into evidence.

## Decisions

**Primary stays Qwen3-8B.** GigaChat3.1-10B-A1.8B was considered as a
Russian-native replacement and rejected on Sber's own benchmark table: BBH
**0.5758** for GigaChat-3.1-Lightning against 0.717 for Qwen3-4B-Instruct (an
earlier draft cited 0.453, which is the GigaChat-3.0 column). BBH is a
reasoning benchmark, not a translation one; it bears on the primary's own job,
"simple reasoning", where a model below Qwen3-4B is not a candidate to replace
Qwen3-8B. It says nothing about GigaChat's Russian translation quality, which
is why the model stays in reserve for that role. Its tool-calling *would* have
worked — the fork's `libllama-common.so` has a dedicated `GigaChatV3` chat
parser — so that was not the reason.

**Concurrent translator on GPU.** A second `llama-server` beside the primary,
both fully resident. Alternatives rejected: swapping models per request (a
reload per translation), translating with the primary (weaker quality, but it
stays in the evaluation as the zero-cost baseline), and CPU-only (the Xeon).

**Fail loudly, do not spill.** Both processes run `-ngl all` with `--fit off`.
A model that does not fit errors at start instead of silently running on the
CPU at 1 token/s, which is the failure this project already hit once. `--fit
on` remains an explicit opt-in. No start-ordering logic is needed: whichever
process starts second and does not fit is the one that fails.

**Paragraph-level chunking.** TranslateGemma was trained on sentences and
blocks of up to 512 tokens, and its documented input is 2K tokens; HY-MT1.5
documents contextual translation but its tested unit is likewise the segment.
Paragraph is therefore the unit these models are known to handle, and it keeps
each request inside the per-slot context. Whether coherence survives across
paragraph boundaries — reused terminology, gender and pronoun agreement — is
**not** established by the sources and is a case in the evaluation; HY-MT's
context-passing prompt is built only if that case fails. Fenced code, inline
code, and URLs pass through verbatim; everything else, headings included, is
translated inline — but a heading's `##`, a list's `-` or `1.`, and a
blockquote's `>` are syntax, not text, and are kept in front of the
translation. The first real run showed why: asked to translate "## Request",
Qwen3-8B returned "Запрос" and the heading was gone. Each marked line is its
own request so the marker re-attaches to exactly its own translation.

One placeholder effect to watch in judging: with a code span replaced by a
placeholder, the same model rendered "for a `409`" as "для a `409`", keeping
the English article beside the token. Count it as a fluency slip; if it
recurs across models, the placeholder wording is the lever.

**Token ceiling, sentence fallback.** Each profile carries a maximum input
size (2048 for TranslateGemma, the per-slot context for the others). A
paragraph over budget — after the prompt preamble and an output allowance are
reserved — is split at sentence boundaries into sub-chunks. Silent truncation
is never an option: it produces a translation that looks finished and is not.

**Per-chunk timeout, partial results, progress.** `timeout_ms` bounds each
chunk, so a ten-page batch is bounded by chunks × timeout without a special
ceiling. A failed chunk returns the translation so far plus an `error` naming
the chunk, matching the `Error` field the other tools already carry. That
does not help a client that stopped waiting on its own request deadline, so
the tool sends an MCP progress notification after every chunk — compliant
clients reset their timeout on progress — and clients that ignore progress
must set a long call timeout for batches.

**Two slots, one batch.** `--parallel 2` is capacity, not policy: two batches
would fill both slots and an interactive sentence would queue behind them. The
tool enforces the policy, being the translator's only caller: a batch (more
than one translatable chunk) holds the single batch permit, a second batch is
rejected at once with "batch already running", and single-chunk requests
always proceed. Note that llama-server divides `-c` across slots, so the
translator's 8192 context is **4096 per slot**, prompt and output included.

**Explicit lifecycle.** A third tray section starts and stops the translator;
the tool reports "translator not running" rather than starting it, because a
lazy start would take 30+ seconds and claim VRAM at an unpredictable moment.

## Candidates

Sizes are from the Hugging Face file listings, not estimates.

| Model | Quant | Weights | Fits beside the primary | Status |
| --- | --- | --- | --- | --- |
| HY-MT1.5-1.8B | Q8_0 | 1.78 GiB | Yes, comfortably | **Evaluate** |
| TranslateGemma-4B | Q4_K_M | 2.32 GiB | Yes | **Evaluate** |
| TranslateGemma-4B | Q5_K_M | 2.64 GiB | Marginal | Try only if Q4 wins and feels short |
| TranslateGemma-4B | Q8_0 | 3.85 GiB | No | — |
| Qwen3-8B (primary) | UD-Q5_K_XL | — | Already loaded | **Baseline** |
| GigaChat3.1-10B-A1.8B | q4_K_M | 6.03 GiB | No; possible with `--cpu-moe` (~5 GB of experts in RAM, ~10–20 tok/s estimated) | Reserve: only if both translators lose to DeepL by an unacceptable margin |
| TranslateGemma-12B | Q4_K_M | ~7.3 GiB | No | Ruled out by budget; would need the primary stopped |
| TranslateGemma-27B | Q4_K_M | ~16 GiB | No | Ruled out |
| HY-MT1.5-7B | Q4_K_M | ~4.5 GiB | No | Ruled out |
| Opus-MT | CT2 int8 | ~80 MB | CPU | Dropped: a second inference engine (CTranslate2 has a C++ API, so not a Python dependency as such) with its own conversion and tokenizer workflow; not worth it while two GGUF candidates cover the pair |
| MADLAD-400 3B | Q8_0 | ~3 GiB | Tight | Dropped: T5 path in llama.cpp is slower than decoder-only |

Sources: `tencent/HY-MT1.5-1.8B-GGUF` (official), `mradermacher/translategemma-4b-it-GGUF`
(Google's weights are gated), `ai-sage/GigaChat3.1-10B-A1.8B-GGUF` (official; note
3.1, not the 3.0 in the community quants).

The [Nuenki translation benchmark](https://nuenki.app/blog/best_language_models_for_translation_v2)
compares hosted models against DeepL and is useful for calibrating how far the
reference ceiling sits above small local models. Its tables render
client-side, so it cannot be quoted from the static page; read it through the
service's own `get_web_page` when the primary is running.

## What each model needs from the tool

These were read from the model cards and, for TranslateGemma, from the chat
template embedded in the GGUF (the card is public; the weights, and so the
official Jinja file, are gated).

**HY-MT1.5** — a single user turn, no system prompt:

```
Translate the following segment into {Language}, without additional explanation.

{text}
```

Tencent's recommended sampling is `temperature 0.7, top_p 0.6, top_k 20,
repetition_penalty 1.05`. This overrides the review's "near-greedy for
translation" default for this model; the vendor's numbers win. Standard
`/v1/chat/completions` works.

**TranslateGemma** — its chat template is not OpenAI-shaped. It requires the
user content to be one item `{type: "text", source_lang_code, target_lang_code,
text}` and raises on anything else. `llama-server`'s `/v1/chat/completions`
normalizes content parts and drops those keys, so the tool renders the Gemma
turn itself and posts to `/completion`:

```
<start_of_turn>user
You are a professional Russian (ru) to English (en) translator. Your goal is to
accurately convey the meaning and nuances of the original Russian text while
adhering to English grammar, vocabulary, and cultural sensitivities.
Produce only the English translation, without any additional explanations or
commentary. Please translate the following Russian text into English:


{text}<end_of_turn>
<start_of_turn>model
```

Google's model card is public (the weights are gated) and its generation
example uses `do_sample=False`, i.e. greedy; the profile's near-greedy values
match that. The card also states a **2K-token input context**, which is the
profile's input ceiling. The GGUF is multimodal, so `--no-mmproj` applies.

`llama-server` adds `<bos>` itself on `/completion` (the fork tokenizes that
route with `add_special = true`), so the rendered turn correctly starts at
`<start_of_turn>`. The fork accepts request-level `chat_template_kwargs`, but
this template reads the language codes from inside `content[0]`, and the
fork's `chat.cpp` has no TranslateGemma compatibility shim, so the
OpenAI-compatible route cannot feed it.

It is worse than unusable through that route: **with `--jinja` the server
does not start at all.** Its init renders the template with a plain-string
probe message to derive a parser, the template raises, and llama-server
exits suggesting `--no-jinja` (observed 2026-09-16, build `b11794`). The
`translategemma` profile therefore runs `--no-jinja`; the tool never used the
server's template for this model anyway. With the engine off,
`/apply-template` cannot render the model's template, so the harness proves
the tool's render another way: the loaded GGUF's template from `/props` must
contain the exact phrases the tool emits, and `/tokenize` must show `<bos>`
prepended and `<start_of_turn>`/`<end_of_turn>` as single tokens. Both held
on the real model in both directions.

**Historical Qwen3-8B baseline** — the recorded runs used a plain instruction with `/no_think`, so the thinking
mode does not add latency and reasoning tokens to a translation.

## Evaluate before choosing

Rankings anywhere in this file come from published benchmarks. The choice is
made on this project's own text, in the workloads the tool promises:

1. **Sentences**: 46 in [translate-eval/sentences.tsv](translate-eval/sentences.tsv),
   23 per direction and parallel across them, from the owner's domain —
   dispatch operations, crawling and outreach, the software behind them, and
   the localization business. Each carries something the judging counts: a
   negation, a modal, a number with a unit or time, a tool name, a
   conditional, an idiom, or a register shift.
2. **Paragraphs and documents**, in [translate-eval/documents/](translate-eval/documents/):
   terminology reused across paragraphs, Russian gender and pronoun
   dependencies resolved by an earlier paragraph, numbers and dates, code and
   URLs, one paragraph over the token ceiling, and one markdown page as
   `read_page` produces it. The mechanical cases ship with the repository;
   the domain cases are the owner's to write.
3. The harness runs everything **through the `translate` tool's own path** —
   never raw `curl` — for each candidate, so the model's own prompt format is
   what gets measured. It first proves the TranslateGemma prompt against
   `/apply-template`, records the fork build, model, profile and the server's
   `/props`, and runs each stochastic candidate **twice** with recorded seeds
   so output stability is visible.
4. **Fit under load**: with the primary loaded and answering a request, a
   batch that occupies both translator slots is run and VRAM is recorded here.
   The ≥1 GiB headroom rule decides whether a candidate's quant stands.
5. Judgement is by a bilingual reader against the **source**, scoring
   **fidelity** (omissions, additions, meaning errors) and **fluency**
   separately in [translate-eval/judging.md](translate-eval/judging.md). DeepL
   is a comparator, not the answer key; matching its wording is not the
   criterion.
6. **Tie criterion, fixed in advance**: a dedicated translator earns the
   second process only if it has **fewer fidelity errors than the Qwen3-8B
   baseline in both directions**. Fluency alone does not. If neither does,
   run one model. If both lose to DeepL by a margin the owner cannot accept,
   bring GigaChat3.1 in via `--cpu-moe` — noting that its 10–20 tok/s figure
   is an estimate with no measurement behind it.

## Review response

The source review of 2026-09-16 changed the following: the GigaChat BBH
figure (wrong column; conclusion unchanged); the fit-margin arithmetic
(replaced by measurement and an explicit headroom rule); the claim that
translation models degrade on documents (narrowed to what the sources say,
with coherence moved into the evaluation); the TranslateGemma sampling note
(the vendor example is greedy); the Opus-MT exclusion reason (engine count,
not Python); and it added the token ceiling with sentence fallback, the batch
admission policy, progress notifications, the per-slot context note, the
`/apply-template` proof, the fit-under-load measurement, the document-level
cases, the fidelity/fluency split, and the tie criterion. It did not change
the primary model, the concurrent topology, the shortlist, or the choice of
`/completion` for TranslateGemma. Its BOS uncertainty is resolved: the server
adds it.

## Results

**Status: pipeline verified on all three models; quality not yet judged;
provisional read is that the baseline stays.** The sentence set has been run
on all three models with two seeds each, but its DeepL references are not
yet pasted in, so the tie criterion has not been formally applied. A
source review on 2026-09-16 ([translate-review-sources.md](translate-review-sources.md))
found that an earlier version of this section overclaimed; the corrections
are recorded under "Corrected claims" below.

Artifacts:

- Side-by-side table: [translate-eval/table.md](translate-eval/table.md)
- Raw runs, with server build and prompt-proof record:
  [Qwen3-8B baseline](translate-eval/results/Qwen3-8B-UD-Q5_K_XL-seed1.json),
  [HY-MT1.5-1.8B](translate-eval/results/HY-MT1.5-1.8B-Q8_0-seed1.json),
  [TranslateGemma-4B](translate-eval/results/translategemma-4b-it.Q4_K_M-seed1.json)
- Fit under load: [HY-MT](translate-eval/results/fit.json),
  [TranslateGemma](translate-eval/results/fit-translategemma/fit.json)
- Scoring: [translate-eval/judging.md](translate-eval/judging.md)

### Run summary (2026-09-16, build `b11794-78af83265`, seed 1)

46 sentences (references pending) and four document cases: the two mechanical
ones — the oversized paragraph now **72 distinct sentences**, so a dropped
one is unambiguous — and Test 3 of the owner's LLM comparison suite as a
bilingual pair (`suite-test3-en`, `suite-test3-ru`), each side's reference
being the suite's own translation of the other.

| | Qwen3-8B (baseline) | HY-MT1.5-1.8B Q8_0 | TranslateGemma-4B Q4_K_M |
| --- | --- | --- | --- |
| mean per sentence (46) | 0.81 s | 0.49 s | 0.53 s |
| oversized paragraph: sentences returned of 72 | **72** (1 request) | **73** (8 requests; one sentence split in two) | **72** (10 requests) |
| suite-test3-en numbers kept | all | dropped **10,000**, **40%** | dropped the whole **"2–3×"** sentence |
| markdown page: `409` code span | kept | **dropped** | **dropped** |
| chunks flagged by the length guard | 0 | 1 (sentence e17: an invented clause) | 1 (the suite chunk missing the 2–3× sentence) |
| VRAM idle beside primary | — | 10196 MiB used, 1714 free | 10803 MiB used, 1107 free |
| fit under load (≥ 1 GiB rule) | — | **passed**, min free 1960 MiB | **passed**, min free 1373 MiB |
| prompt proof | n/a (chat route) | n/a (chat route) | full prompt reconstructed from the loaded template, identical in both directions |
| sentences changed between seed 1 and seed 2 (of 46) | 16 | **33** | **0** |

Both translators fit beside the primary; TranslateGemma is the tighter of
the two. Both are faster than the primary. TranslateGemma at top-k 1 is
deterministic across seeds; HY-MT at Tencent's recommended temperature 0.7
changed 33 of 46 sentences between seeds, so a single run of it is not
representative and judging it needs both. **Neither is more faithful on this
evidence**: each lost material the baseline kept, and the baseline lost
nothing that was checked. The baseline has meaning errors of its own — "fail
gracefully" became «завершаться без ошибок» (terminate without errors),
«халтурный» became "low-cost" — but nothing was omitted or invented.

### Sentence set (46 sentences, seeds 1 and 2)

Generated from the result files on 2026-09-16; references were empty at the time, so this is a comparison between models, not a score.

| | Qwen3-8B | HY-MT1.5-1.8B | TranslateGemma-4B |
| --- | --- | --- | --- |
| mean per sentence, seed 1 | 0.81 s | 0.49 s | 0.53 s |
| mean per sentence, seed 2 | 0.80 s | 0.48 s | 0.47 s |
| outputs changed between seeds | 16 | 33 | 0 |
| length-guard flags (both seeds) | 0 | 1 | 0 |
| placeholder omissions (both seeds) | 0 | 0 | 0 |
| one source sentence returned as several, seed 1 | 0 | 22 | 0 |

Every source sentence is a single sentence, so the last row counts restructuring, not error; it is where HY-MT differs most.

The eight sentences below carry the traps the judging counts — negation, a modal, a number with a unit, an idiom, a specific error code — in both directions, seed 1. The full 46 × 6 comparison is in [translate-eval/table.md](translate-eval/table.md).

**r03** (ru-en): Мы не можем гарантировать доставку в тот же день, если заказ оформлен после полудня.

| model | output |
| --- | --- |
| Qwen3-8B | We cannot guarantee same-day delivery if the order is placed after noon. |
| HY-MT1.5-1.8B | We cannot guarantee delivery on the same day, if the order is placed after noon. |
| TranslateGemma-4B | We cannot guarantee same-day delivery if the order is placed after noon. |

**e09** (en-ru): No reply within a week does not mean a refusal; many authors check their mail once a month.

| model | output |
| --- | --- |
| Qwen3-8B | Отсутствие ответа в течение недели не означает отказ; многие авторы проверяют почту один раз в месяц. |
| HY-MT1.5-1.8B | Не получение ответа в течение недели не означает отказа от письма. Многие авторы проверяют свои письма раз в месяц. |
| TranslateGemma-4B | Отсутствие ответа в течение недели не означает автоматического отказа; многие авторы проверяют свою почту раз в месяц. |

**r07** (ru-en): Груз весом свыше 1 250 кг требует второй подписи и не может быть выдан одному сотруднику.

| model | output |
| --- | --- |
| Qwen3-8B | A load exceeding 1,250 kg requires a second signature and cannot be issued to a single employee. |
| HY-MT1.5-1.8B | A cargo weighing more than 1,250 kilograms requires a second signature before it can be released. It cannot be given to just one employee alone. |
| TranslateGemma-4B | Any shipment weighing more than 1,250 kg requires a second signature and cannot be issued to a single employee. |

**e07** (en-ru): A load over 1,250 kg requires a second signature and cannot be released to a single employee.

| model | output |
| --- | --- |
| Qwen3-8B | Груз свыше 1 250 кг требует второй подписи и не может быть выдан одному сотруднику. |
| HY-MT1.5-1.8B | Объем груза, превышающий 1250 кг, требует подписи еще одного человека. Груз не может быть передан одному сотруднику. |
| TranslateGemma-4B | Перевозка груза весом более 1250 кг требует подписи двух лиц и не может быть передана одному сотруднику. |

**r17** (ru-en): Без редактора-человека вы получите не качество, а «высококачественную» халтуру.

| model | output |
| --- | --- |
| Qwen3-8B | Without a human editor, you'll get not quality, but "high-quality" shoddy work. |
| HY-MT1.5-1.8B | Without a human editor, you won’t get quality work at all. You’ll only get “high-quality” crap. |
| TranslateGemma-4B | Without a human editor, you will receive not quality, but "high-quality" amateur work. |

**e17** (en-ru): Without a human editor you won't get quality — you'll get "high-quality" slop.

| model | output |
| --- | --- |
| Qwen3-8B | Без редактора вы не получите качественный текст — вы получите «высококачественный» хлам. |
| HY-MT1.5-1.8B ⚠ flagged | Без участия человека, который будет отбирать и редактировать текст, получится лишь некачественный текст. Вы получите „высококачественный“ текст, но это всего лишь формальность. |
| TranslateGemma-4B | Без участия человека-редактора вы не получите качественный текст – вместо этого вы получите "высококачественный" набор бессвязных и нелогичных фраз. |

**r13** (ru-en): Сервер вернул ошибку 409, поэтому повторять запрос бессмысленно — заказ нужно открыть заново.

| model | output |
| --- | --- |
| Qwen3-8B | The server returned an error 409, so repeating the request is pointless — the order needs to be placed again. |
| HY-MT1.5-1.8B | The server returned an error code 409. Therefore, it’s pointless to make another request. The order needs to be opened again. |
| TranslateGemma-4B | The server returned a 409 error, so repeating the request would be pointless – the order needs to be initiated again. |

**e13** (en-ru): The server returned a 409, so retrying is pointless — the order has to be reopened.

| model | output |
| --- | --- |
| Qwen3-8B | Сервер вернул 409, поэтому повторная попытка бесполезна — заказ нужно переоткрыть. |
| HY-MT1.5-1.8B | Сервер вернул ответ с кодом 409. Поэтому повторные попытки бессмысленны – заказ необходимо снова открыть. |
| TranslateGemma-4B | Сервер вернул код 409, поэтому повторная попытка бессмысленна – заказ необходимо повторно открыть. |

### Corrected claims

An earlier draft of this section said the oversized paragraph "reassembled
successfully" and that "numbers were preserved by all three". Both were
wrong. The paragraph was then six repeats of twelve sentences, and at
~1300-token chunks HY-MT returned 48 of 72 sentences and TranslateGemma 47,
with no error — each had collapsed three repetitions to two. Number
preservation had been checked on one paragraph and generalized. The speed
comparison in that draft therefore compared unequal work.

Three changes followed. Requests to translation models are now capped at
**512 tokens** — TranslateGemma's training block size, and the size at which
HY-MT stopped dropping — which restored 72 of 72 on both. A **length guard**
flags any chunk whose output is implausibly short or long for its input
(character ratio outside 0.5–2×, or fewer than 75% of the sentences), and the
tool reports the count as `suspect`; it caught HY-MT inventing a clause and
TranslateGemma dropping a sentence. And the fit measurement now fails on a
partial result, not only on a transport error.

### Pipeline findings from the real runs, all fixed

- The model ate `##` heading markers; line-leading markdown is now kept as a
  prefix and never sent.
- The URL placeholder swallowed a trailing full stop; sentence punctuation is
  now left outside it.
- A dropped code span left an omission nobody could see; the tool reports
  `omitted`, and the table flags it.
- TranslateGemma's GGUF makes this fork's `llama-server` exit at startup
  under `--jinja`; its profile runs `--no-jinja`.
- The TranslateGemma prompt proof looked for fragments; it now reconstructs
  the full prompt from the loaded template's own literals and requires a
  byte-identical match, and fails on a swapped language, a reworded phrase,
  or an extra template variable.
- The table labelled every reference "DeepL"; it now says "reference" and
  points at the provenance recorded in `documents/README.md`.

### Observations for the judging — not verdicts

On the comparison-suite pair, where the suite's own error counters apply:

- **Negation** ("absence of evidence … evidence of absence"): Qwen3-8B kept
  the parallelism («отсутствие доказательств как доказательство
  отсутствия»); HY-MT shifted it to «признаком отсутствия информации»;
  TranslateGemma produced a circular «на основании её отсутствия».
- **Numbers**: see the table. Formatting also differed — Qwen `1 248`, HY-MT
  `1,248`, TranslateGemma `1248`.
- **Idiom** ("higher-quality slop" / «халтурный»): none of the three landed
  it cleanly in either direction.
- **Unfenced code**: the EN case ends with an unfenced Go snippet, as the
  suite presents it; it was sent as two prose "paragraphs". Compare what
  each model did with it in the table.

On the sentences (seed 1, all three visible in the table): HY-MT
habitually splits one source sentence into two and shifts nouns — «Объем
груза» (*volume*) for "load", «отказа от письма» adding *from the letter*;
TranslateGemma adds qualifiers the source lacks — «автоматического отказа»,
«подписи двух лиц» (*two signatures*) for "a second signature", and an
invented elaboration for "slop"; Qwen3-8B rendered «открыть заново» (*reopen*)
as "placed again" in r13, its clearest meaning slip in the set, while
handling the negations and «халтуру» → "shoddy work" / "slop" → «хлам»
cleanly.

On the mechanical cases: both dedicated translators dropped the same `409`
code span from "Do not retry a `409`" while Qwen3-8B kept it — a placeholder
immediately after an article is fragile for translation-tuned models. HY-MT
rendered a 6 PM deadline as «по 18 часов» and "Weights" as «Весы» (scales).
TranslateGemma chose «переназначил» — the reference's verb — where Qwen3-8B
said «переделал».

### What decides

The tie criterion in "Evaluate before choosing": a dedicated translator earns
the second process only with fewer fidelity errors than the baseline in both
directions. On this evidence neither does — both omitted or invented material
the baseline did not — so **Qwen3-8B stays the provisional translator and the
translator process is not started by default**. That stands until the
sentence set is scored with references. If a
dedicated translator is still wanted for speed, the fidelity gap is what it
must close.

### Current Qwen prompt correction — 2026-09-16

New translation requests disable thinking with `chat_template_kwargs.enable_thinking=false` instead of appending `/no_think` to the source text. The appended marker leaked into translations. The local server handles the boolean request setting. Historical evaluation outputs above retain their original prompt and have not been regenerated.
