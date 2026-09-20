# AI agent software roadmap, grouped by purpose

158 software projects from the reviewed catalogue and follow-up reviews, grouped by their main role. Descriptions summarize documentation, discussion evidence and selected source inspection. Each project appears once; the groups overlap in practice.

**Statistics checked: 2026-09-20 (UTC).** Stars are GitHub stars. Issues are open issues, excluding pull requests. Last updated is the most recent repository push (`pushed_at`, any branch), shown as a UTC date. Contributors use GitHub's displayed count, with a linked API total for Every Code; bots may be included. Counts describe the linked repository, including its fork history or documentation scope.

**—** means a comparable repository metric was not verified for that product. **Disabled** means GitHub issues are disabled. Archived repositories are labelled in their descriptions. GitHub links are the sources for repository statistics; website links identify product-only entries.

## 1. Agents and execution harnesses

Tools that perform coding or other tasks using a model and access to tools.

| Name | Link | Description | Stars | Issues | Last updated | Contributors |
| --- | --- | --- | ---: | ---: | --- | ---: |
| Aider | [GitHub](https://github.com/Aider-AI/aider) | Terminal pair programming focused on editing and versioning repository changes. | 49,068 | 1,378 | 2026-05-22 | 171 |
| Amp | [Website](https://ampcode.com) | Commercial coding-agent product; detailed capabilities were not verified in the review. | — | — | — | — |
| Claude Code | [GitHub](https://github.com/anthropics/claude-code) | Anthropic coding agent for terminal and repository work; linked repository includes plugins and issue tracking. | 146,760 | 11,612 | 2026-09-20 | 58 |
| Cline | [GitHub](https://github.com/cline/cline) | Coding agent with editor, CLI and SDK interfaces. | 68,802 | 801 | 2026-09-19 | 347 |
| Codex CLI | [GitHub](https://github.com/openai/codex) | OpenAI coding agent for terminal and repository work. | 125,338 | 17,743 | 2026-09-20 | 628 |
| Continue | [GitHub](https://github.com/continuedev/continue) | Coding-agent tooling with configurable models and development workflows. | 35,957 | 451 | 2026-09-19 | 472 |
| Crush | [GitHub](https://github.com/charmbracelet/crush) | Go-based terminal coding agent from Charm. | 28,194 | 444 | 2026-09-20 | 135 |
| Cursor CLI | [Website](https://cursor.com/cli) | Cursor's terminal and automation interface for coding tasks. | — | — | — | — |
| Deep Agents / Deep Agents Code | [GitHub](https://github.com/langchain-ai/deepagents) | Agent harness with planning, subagents, file tools and configurable execution backends. | 29,580 | 153 | 2026-09-19 | 170 |
| Devin | [Website](https://devin.ai) | Hosted software-engineering agent product. | — | — | — | — |
| Every Code | [GitHub](https://github.com/just-every/code) | Codex-derived coding harness with agent delegation, browser tools and automated review. | 4,029 | 27 | 2026-09-16 | [467](https://api.github.com/repos/just-every/code/contributors?per_page=1&anon=false) |
| Gajae-Code | [GitHub](https://github.com/Yeachan-Heo/gajae-code) | Experimental coding harness with planner, critic, executor and verifier roles. | 2,823 | 37 | 2026-09-19 | 148 |
| Gemini CLI | [GitHub](https://github.com/google-gemini/gemini-cli) | Google terminal agent for coding and tool-driven tasks. | 107,090 | 577 | 2026-09-20 | 696 |
| GitHub Copilot CLI | [GitHub](https://github.com/github/copilot-cli) | GitHub Copilot terminal interface for agent-assisted development. | 11,185 | 2,309 | 2026-09-18 | 31 |
| Goose | [GitHub](https://github.com/aaif-goose/goose) | Extensible development agent connecting models to tools and integrations. | 54,474 | 263 | 2026-09-19 | 659 |
| Hermes Agent | [GitHub](https://github.com/NousResearch/hermes-agent) | Persistent assistant with memory, skills, delegation, schedules and messaging integrations. | 247,191 | 13,983 | 2026-09-20 | 3,316 |
| Kimi Code CLI | [GitHub](https://github.com/MoonshotAI/kimi-cli) | Moonshot terminal coding agent with repository tools. | 11,407 | 490 | 2026-09-01 | 76 |
| OpenCode | [GitHub](https://github.com/anomalyco/opencode) | Coding agent with terminal and automation interfaces and multiple model providers. | 208,679 | 4,427 | 2026-09-20 | 1,008 |
| OpenFox | [GitHub](https://github.com/co-l/openfox) | Local-model-oriented coding assistant with configurable workflows and OpenAI-compatible backends. | 301 | 39 | 2026-09-19 | 27 |
| OpenHands | [GitHub](https://github.com/OpenHands/OpenHands) | Software-development agent platform with managed execution environments and repository workflows. | 88,557 | 434 | 2026-09-19 | 579 |
| OpenHuman | [GitHub](https://github.com/tinyhumansai/openhuman) | Local assistant with checkpointed agent workflows and a canvas for reviewing recurring processes. | 39,900 | 197 | 2026-09-19 | 183 |
| Pi | [GitHub](https://github.com/earendil-works/pi) | Extensible coding CLI and toolkit for custom agent runtimes and model providers. | 107,378 | 147 | 2026-09-19 | 290 |
| Plandex | [GitHub](https://github.com/plandex-ai/plandex) | Coding agent for larger tasks with planning and project-context management. | 15,645 | 39 | 2025-10-03 | 23 |
| Qwen Code | [GitHub](https://github.com/QwenLM/qwen-code) | Qwen coding agent for terminal-based development. | 27,997 | 1,173 | 2026-09-20 | 571 |
| Roo Code | [GitHub](https://github.com/RooCodeInc/Roo-Code) | **Archived.** Editor-based coding agent with specialized working modes. | 24,301 | 550 | 2026-05-15 | 301 |
| Sir Thaddeus | [GitHub](https://github.com/raydeStar/sir-thaddeus) | Local assistant with tools and a public evaluation suite. | 14 | 0 | 2026-09-14 | 5 |
| Steiner | [GitHub](https://github.com/luispabon/steiner) | Go coding agent with bounded context and configurable sandboxed execution. | 7 | 27 | 2026-09-19 | 3 |
| SWE-agent | [GitHub](https://github.com/SWE-agent/SWE-agent) | Repository issue-to-patch agent and reference implementation for software-agent evaluation. | 20,366 | 45 | 2026-09-14 | 103 |
| Windsurf / Devin Desktop | [Website](https://windsurf.com) | Coding IDE lineage now presented as Devin Desktop. | — | — | — | — |

## 2. Planning, specifications and development methods

Tools and workflow packages for turning an idea into specifications, plans and development steps.

| Name | Link | Description | Stars | Issues | Last updated | Contributors |
| --- | --- | --- | ---: | ---: | --- | ---: |
| Agent OS | [GitHub](https://github.com/buildermethods/agent-os) | Captures codebase standards and supplies relevant conventions to coding agents. | 5,430 | 0 | 2026-08-29 | 18 |
| BMAD Method | [GitHub](https://github.com/bmad-code-org/BMAD-METHOD) | Agent-assisted planning and development method with roles and structured project artifacts. | 53,248 | 35 | 2026-09-20 | 166 |
| Claude Conductor | [GitHub](https://github.com/rbarcante/claude-conductor) | Development tracks with specification, plan, decision and review artifacts. | 56 | 0 | 2026-03-31 | 3 |
| Compound Engineering | [GitHub](https://github.com/EveryInc/compound-engineering-plugin) | Development skills covering planning, implementation, review and reusable lesson capture. | 25,161 | 72 | 2026-09-20 | 109 |
| fabriqa.ai | [Website](https://fabriqa.ai/) | Desktop workspace connecting specifications, tasks, agent sessions and reviews. | — | — | — | — |
| GSD Core | [GitHub](https://github.com/open-gsd/gsd-core) | Specification and context workflow spanning research, planning, execution, verification and shipping. | 9,629 | 118 | 2026-09-20 | 185 |
| gstack | [GitHub](https://github.com/garrytan/gstack) | Opinionated skills for product, engineering, testing and review work. | 133,717 | 357 | 2026-09-18 | 137 |
| Kiro | [Website](https://kiro.dev/) | Agentic IDE organized around requirements, design, tasks, hooks and steering documents. | — | — | — | — |
| Liteagents | [GitHub](https://github.com/hamr0/liteagents) | Specialist agents and commands with session handoffs, memory and deferred-fix tracking. | 24 | 0 | 2026-09-18 | 3 |
| OpenSpec (Fission-AI) | [GitHub](https://github.com/Fission-AI/OpenSpec) | Specification workflow for proposing, applying and archiving changes in existing projects. | 69,586 | 124 | 2026-09-18 | 122 |
| OpenSpec Template | [GitHub](https://github.com/arananet/openspec-template) | Specification template linking execution records and verification to the inputs used. | 10 | 1 | 2026-09-12 | 2 |
| Praxis | [GitHub](https://github.com/intoinside/Praxis) | Intent/specification artifact CLI; inspected execution and drift-detection paths include simulations. | 14 | 4 | 2026-02-24 | 1 |
| REAP | [GitHub](https://github.com/c-d-cc/reap) | Slash-command development method moving through specification, implementation and verification. | 56 | 1 | 2026-09-12 | 2 |
| Spec Kit | [GitHub](https://github.com/github/spec-kit) | GitHub toolkit for carrying specifications into planning and implementation tasks. | 137,989 | 137 | 2026-09-18 | 306 |
| Spec Kitty | [GitHub](https://github.com/spec-kitty/spec-kitty) | Specification workflow with work packages, worktrees and review/acceptance stages. | 1,636 | 801 | 2026-09-20 | 87 |
| SpecPilot | [GitHub](https://github.com/girishr/SpecPilot) | CLI scaffolding development specifications, commands and records; validation is primarily structural. | 38 | 0 | 2026-09-13 | 4 |
| SpecPulse | [GitHub](https://github.com/specpulse/specpulse) | CLI scaffolding specifications, plans and tasks before optional model enrichment. | 394 | 2 | 2025-11-30 | 2 |
| specs.md | [GitHub](https://github.com/fabriqaai/specs.md) | Development workflow packages ranging from lightweight planning to full lifecycle methods. | 214 | 9 | 2026-09-09 | 7 |
| Superpowers | [GitHub](https://github.com/obra/superpowers) | Coding-agent skills for disciplined planning, implementation and review. | 288,870 | 134 | 2026-09-19 | 51 |
| Tessl | [Website](https://tessl.io/) | Platform for coding-agent skills, context management and evaluation. | — | — | — | — |
| UCAI | [GitHub](https://github.com/Joncik91/ucai) | Claude Code commands, agents and hooks for specification-to-pull-request development. | 28 | 0 | 2026-08-26 | 3 |
| VibeScaffold | [GitHub](https://github.com/benjaminshoemaker/vibecode_spec_generator) | Requirements wizard generating project briefs, specifications and agent instructions. | 78 | 0 | 2025-12-29 | 1 |

## 3. Coding workflow orchestration

Packages that coordinate coding roles, task dependencies, handoffs and review cycles.

| Name | Link | Description | Stars | Issues | Last updated | Contributors |
| --- | --- | --- | ---: | ---: | --- | ---: |
| Agent-Team | [GitHub](https://github.com/thebpandey/agent-team) | Coordinates coding agents using bounded assignments, worktrees, independent review and serialized integration. | 0 | 0 | 2026-09-16 | 2 |
| Agentic Orchestration Control | [GitHub](https://github.com/ZypherHQ/agent-orchestration-skill) | Codex orchestration skill, CLI and local dashboard with run records and usage imports. | 71 | 1 | 2026-05-25 | 1 |
| Apra Fleet | [GitHub](https://github.com/Apra-Labs/apra-fleet) | Agent fleet workflows with member allocation, provider routing, watchdogs and execution logs. | 92 | 42 | 2026-09-19 | 13 |
| BAD (BMAD Autonomous Development) | [GitHub](https://github.com/stephenleo/bmad-autonomous-development) | BMAD automation skill describing story implementation, review and pull-request/CI workflows. | 107 | 0 | 2026-04-19 | 2 |
| bmad-loop | [GitHub](https://github.com/bmad-code-org/bmad-loop) | Development loop built around BMAD planning artifacts and coding-agent execution. | 137 | 128 | 2026-09-20 | 20 |
| Cheasee Pi | [GitHub](https://github.com/SchneiderDaniel/cheasee-pi) | Staged development workflow on Pi, Docker and GitHub Projects. | 62 | 8 | 2026-09-19 | 4 |
| Claude MPM | [GitHub](https://github.com/bobmatnyc/claude-mpm) | Claude Code project manager with specialist agents, skills and session management. | 153 | 0 | 2026-08-31 | 15 |
| Claude Octopus | [GitHub](https://github.com/nyldn/claude-octopus) | Claude Code plugin coordinating research, implementation, multiple providers and independent review. | 4,090 | 0 | 2026-09-20 | 30 |
| claude-codex | [GitHub](https://github.com/Z-M-Huang/claude-codex) | **Archived.** Claude Code plugin with sequential review and a Codex final gate. | 26 | 2 | 2026-02-22 | 1 |
| claude-codex-gemini | [GitHub](https://github.com/Z-M-Huang/claude-codex-gemini) | Artifact-based pipeline assigning planning, execution and review to different coding CLIs. | 18 | 0 | 2026-02-06 | 1 |
| Codex Astra/Luna Orchestrator | [GitHub](https://github.com/donvito/codex-astra-luna-orchestrator) | Codex configuration bundle assigning models to coordinator, worker and reviewer roles. | 1,499 | 2 | 2026-09-17 | 5 |
| codex_workflow | [GitHub](https://github.com/viettran-edgeAI/codex_workflow) | Codex workflow configuration with scoped roles, handoff documents and usage reporting. | 485 | 0 | 2026-09-19 | 2 |
| Consort | [GitHub](https://github.com/siimvene/consort) | Claude Code workflow plugin with planning, delegated implementation and independent reviews. | 7 | 0 | 2026-09-07 | 2 |
| Crewplane | [GitHub](https://github.com/crewplaneai/crewplane) | Markdown workflow graphs around coding CLIs, with dependencies, artifacts and bounded review loops. | 38 | 1 | 2026-09-19 | 4 |
| Firstmate | [GitHub](https://github.com/kunchenguid/firstmate) | Agent instructions and scripts for a liaison coordinating workers in sessions and worktrees. | 6,754 | 532 | 2026-09-20 | 77 |
| Harness Console | [GitHub](https://github.com/gammawolfe/harness-console) | BMAD-oriented runner with retries and evidence tracking; inspected gate does not execute tests. | 2 | 0 | 2026-06-28 | 1 |
| Hedgehog | [GitHub](https://github.com/skyf0xx/hedgehog) | BMAD-based development workflow with a SQLite task graph, scopes and verification commands. | 40 | 26 | 2026-09-20 | 6 |
| Liza | [GitHub](https://github.com/liza-mas/liza) | Coding workflow with task decomposition, implementer/reviewer roles and worktrees. | 394 | 16 | 2026-09-19 | 9 |
| LoopTroop | [GitHub](https://github.com/looptroop-ai/LoopTroop) | OpenCode-based planning and implementation app with small tasks and test/fix loops. | 149 | 2 | 2026-09-19 | 5 |
| myclaude | [GitHub](https://github.com/stellarlinkco/myclaude) | Claude-oriented development workflow package with specialized agents and reusable methods. | 2,751 | 4 | 2026-05-04 | 15 |
| Oh My OpenAgent | [GitHub](https://github.com/code-yeongyu/oh-my-openagent) | Agent workflow package combining role routing, delegation and model orchestration. | 69,201 | 597 | 2026-09-19 | 327 |
| oh-my-claudecode | [GitHub](https://github.com/Yeachan-Heo/oh-my-claudecode) | Claude Code workflow package with planning, execution, verification and repair stages. | 39,260 | 2 | 2026-09-18 | 151 |
| Pied Piper | [GitHub](https://github.com/sathish316/pied-piper) | Generates agent teams from configurable roles and repeatable development playbooks. | 80 | 12 | 2026-08-05 | 3 |
| Ralph Orchestrator | [GitHub](https://github.com/mikeyobrien/ralph-orchestrator) | Coding-agent orchestration with event-driven roles and configurable test, lint and type-check gates. | 3,150 | 1 | 2026-09-10 | 42 |
| RoboCo | [GitHub](https://github.com/rennf93/roboco) | Experimental software-company workflow with management, implementation, QA and reviewer agents. | 172 | 0 | 2026-09-20 | 6 |
| Ruflo | [GitHub](https://github.com/ruvnet/ruflo) | Broad agent coordination package combining delegation, memory, hooks and provider routing. | 72,872 | 679 | 2026-09-19 | 40 |
| Stageflow | [GitHub](https://github.com/tejasghutukade/stageflow) | YAML development pipelines with dependencies, artifacts, checks, human gates and stored run state. | 11 | 0 | 2026-09-20 | 3 |
| Tagteam | [GitHub](https://github.com/cephalopod-ai/tagteam) | Go orchestrator driving coding CLIs through supervisor, relay, solo and adversarial review loops. | 1 | 0 | 2026-09-16 | 4 |
| YOLO-starter | [GitHub](https://github.com/ivasuy/YOLO-starter) | Experimental Codex workflow with role agents and file state; retry exhaustion can report success. | 1 | 0 | 2026-05-19 | 2 |

## 4. Dashboards, sessions and workspaces

Interfaces for supervising agents, switching sessions and organizing parallel work.

| Name | Link | Description | Stars | Issues | Last updated | Contributors |
| --- | --- | --- | ---: | ---: | --- | ---: |
| Agent Orchestrator (Untrivial) | [GitHub](https://github.com/Untrivial-ai/agent-orchestrator) | Worker workspaces linking tasks, conversations, branches, pull requests and review state. | 12,194 | 379 | 2026-09-20 | 122 |
| AI Maestro | [GitHub](https://github.com/23blocks-OS/ai-maestro) | Persistent-agent dashboard with messaging, memory and multi-machine coordination. | 789 | 10 | 2026-09-20 | 10 |
| Aperant (Auto-Claude) | [GitHub](https://github.com/AndyMik90/Aperant) | Autonomous multi-session coding workspace, formerly Auto-Claude. | 14,562 | 46 | 2026-06-14 | 73 |
| Appoly Multiagent Chat | [GitHub](https://github.com/appoly/multiagent-chat) | Electron interface coordinating local coding CLIs through terminals and message files. | 8 | 0 | 2026-09-08 | 3 |
| Atrium | [Website](https://getatrium.dev/docs) | macOS interface supervising coding CLIs through local or remote daemons. | — | — | — | — |
| Buzz | [GitHub](https://github.com/block/buzz) | Shared workspace for human, agent and workflow events, with coding-agent integration. | 33,703 | 1,565 | 2026-09-20 | 122 |
| Castforge | [Website](https://castforge.ai) | Desktop task board coordinating coding CLIs across planning, implementation, testing and review. | — | — | — | — |
| Claude Code Bridge (CCB) | [GitHub](https://github.com/SeemSeam/claude_codex_bridge) | Multi-provider terminal bridge with a background daemon, shared context and human takeover. | 3,511 | 69 | 2026-09-19 | 49 |
| Claw Orchestrator | [GitHub](https://github.com/Enderfga/claw-orchestrator) | Multiple coding CLIs behind persistent sessions and API, MCP and ACP interfaces. | 578 | 0 | 2026-09-17 | 13 |
| Echorb | [Website](https://virtual-life.dev/echorb) | Desktop workspace organizing coding agents and iterative development loops. | — | — | — | — |
| GitKraken Kepler | [Website](https://gitkraken.com/kepler) | GitKraken interface for visualizing agent work and following tasks through pull requests. | — | — | — | — |
| golutra | [GitHub](https://github.com/golutra/golutra) | Desktop console coordinating parallel coding-agent sessions and workspaces. | 3,841 | 48 | 2026-08-06 | 1 |
| Goodboy | [GitHub](https://github.com/akhayam99/goodboy) | Desktop task workspace retaining decisions and summaries across sequential agent handoffs. | 107 | 18 | 2026-09-19 | 4 |
| intentic | [GitHub](https://github.com/intentic/intentic) | Browser workspace for user-hosted agent environments, worktrees and diff review. | 44 | 0 | 2026-09-19 | 2 |
| Maestro | [GitHub](https://github.com/RunMaestro/Maestro) | Desktop agent cockpit with worktrees, Markdown playbooks and a standalone execution CLI. | 3,351 | 55 | 2026-09-20 | 59 |
| OpenSwarm | [GitHub](https://github.com/openswarm-ai/openswarm) | Agent workspace with a headless backend; reviewed execution uses the Claude SDK. | 818 | 10 | 2026-09-18 | 8 |
| Orca | [GitHub](https://github.com/stablyai/orca) | Coding-agent console with worktrees, remote sessions, browser tools and diff annotation. | 72,738 | 3,021 | 2026-09-20 | 442 |
| Paseo | [GitHub](https://github.com/getpaseo/paseo) | Daemon and remote interface for managing coding-agent sessions across providers. | 17,720 | 508 | 2026-09-18 | 195 |
| Runner | [GitHub](https://github.com/yicheng47/runner) | Desktop terminal for coding-agent roles and missions; reviewed builds cover macOS and Windows. | 117 | 27 | 2026-09-20 | 2 |
| Superset | [GitHub](https://github.com/superset-sh/superset) | Agent workspaces with terminals, worktrees and CLI/SDK/MCP automation interfaces. | 14,402 | 359 | 2026-09-20 | 132 |
| Thurbox | [GitHub](https://github.com/Thurbeen/thurbox) | Terminal workspace with worktrees, remote sessions, headless control and agent mailboxes. | 72 | 7 | 2026-09-19 | 9 |
| Traycer | [GitHub](https://github.com/traycerai/traycer) | Desktop planning boards and task workflows around existing coding agents. | 1,501 | 181 | 2026-09-19 | 16 |
| Vibe Kanban | [GitHub](https://github.com/BloopAI/vibe-kanban) | Coding-agent task board and worktrees; site announces sunsetting and community maintenance. | 28,134 | 384 | 2026-09-19 | 71 |
| Vibeyard | [GitHub](https://github.com/elirantutia/vibeyard) | Coding-agent workspace with terminal sessions, task boards and usage inspection. | 1,379 | 19 | 2026-09-03 | 16 |
| Warp / Warp Factories | [GitHub](https://github.com/warpdotdev/warp) | Terminal-based development environment with agent sessions and workflow automation. | 65,104 | 3,872 | 2026-09-20 | 181 |

## 5. Workflow runtimes and agent frameworks

Building blocks for custom agent applications, workflow execution and recovery.

| Name | Link | Description | Stars | Issues | Last updated | Contributors |
| --- | --- | --- | ---: | ---: | --- | ---: |
| AgentGPT | [GitHub](https://github.com/reworkd/AgentGPT) | **Archived.** Browser application for configuring autonomous agents. | 36,288 | 132 | 2025-04-29 | 73 |
| Anima SDK | [GitHub](https://github.com/Rai220/anima_sdk) | Experimental agent runtime using short harness runs, file state and an outer restart loop. | 41 | 0 | 2026-09-08 | 2 |
| AutoGPT | [GitHub](https://github.com/Significant-Gravitas/AutoGPT) | Platform for building and running reusable agent automations. | 187,448 | 313 | 2026-09-20 | 849 |
| AxonFlow | [GitHub](https://github.com/getaxonflow/axonflow) | Runtime control layer for policies, workflow state, approval/resume and audit records. | 71 | 2 | 2026-09-17 | 4 |
| Cersei | [GitHub](https://github.com/pacifio/cersei) | Embeddable Rust agent harness with serializable workflow graphs and a visual editor. | 457 | 6 | 2026-08-06 | 13 |
| CrewAI | [GitHub](https://github.com/crewAIInc/crewAI) | Python framework for role-based agent teams and event-driven workflows. | 58,789 | 159 | 2026-09-19 | 360 |
| Flyte | [GitHub](https://github.com/flyteorg/flyte) | Workflow platform for Python, ML and agents; backend availability depends on the version. | 7,532 | 106 | 2026-09-18 | 349 |
| Hatchet | [GitHub](https://github.com/hatchet-dev/hatchet) | Durable task engine with retries, scheduling, concurrency controls and worker queues. | 7,972 | 73 | 2026-09-19 | 99 |
| Inngest | [GitHub](https://github.com/inngest/inngest) | Event-driven durable functions with retries, event waits, cancellation and flow control. | 5,853 | 55 | 2026-09-19 | 58 |
| LangGraph | [GitHub](https://github.com/langchain-ai/langgraph) | Build stateful agent workflows with branching, persistence and human intervention. | 41,968 | 556 | 2026-09-20 | 301 |
| n8n | [GitHub](https://github.com/n8n-io/n8n) | Visual automation for integrations, triggers, API calls and agent steps. | 205,396 | 406 | 2026-09-20 | 845 |
| NimbleBrain | [GitHub](https://github.com/NimbleBrainInc/nimblebrain) | Self-hosted agent and MCP-app platform with skills, scoped workspaces and scheduled automation. | 22 | 212 | 2026-09-18 | 14 |
| Omnigent | [GitHub](https://github.com/omnigent-ai/omnigent) | Python wrapper around agent harnesses with YAML definitions, subagents, sessions and policy hooks. | 10,106 | 517 | 2026-09-20 | 289 |
| Pi Dynamic Workflows | [GitHub](https://github.com/QuintinShaw/pi-dynamic-workflows) | JavaScript workflows on Pi with parallel agents, structured outputs and replay journals. | 531 | 9 | 2026-09-14 | 31 |
| Sagent | [GitHub](https://github.com/rekursiv-ai/sagent) | Python agent runtime with delegation, peer messaging, sessions and model switching. | 55 | 1 | 2026-09-19 | 7 |
| Shannon | [GitHub](https://github.com/Kocoro-lab/Shannon) | Multi-agent backend combining Go orchestration, Temporal workflows and Python execution. | 2,256 | 1 | 2026-09-05 | 15 |
| Synapse AI | [GitHub](https://github.com/synapseorch-ai/synapse-ai) | Agent workflow graphs with per-step models, human review and checkpoint recovery. | 326 | 0 | 2026-09-01 | 5 |
| Team | [GitHub](https://github.com/cumbof/team) | Experimental Python agent teams with local/OpenAI-compatible models and persistent memory. | 7 | 0 | 2026-06-23 | 3 |
| Temporal | [GitHub](https://github.com/temporalio/temporal) | Durable workflow engine for retries, recovery, timers and long-running processes. | 23,180 | 576 | 2026-09-20 | 303 |
| Twemp | [GitHub](https://github.com/whitedwarf7/Twemp) | Experimental incident-response command center with agent roles, human approval and simulated remediation. | 0 | 0 | 2026-08-25 | 1 |
| Weft | [GitHub](https://github.com/WeaveMindAI/weft) | Experimental typed workflow language and Rust framework with persistent execution journals. | 1,971 | 4 | 2026-09-19 | 4 |

## 6. Memory, tasks and coordination

Tools for retaining context, tracking work and exchanging information between agents.

| Name | Link | Description | Stars | Issues | Last updated | Contributors |
| --- | --- | --- | ---: | ---: | --- | ---: |
| aimee | [GitHub](https://github.com/RakuenSoftware/aimee) | Local service combining persistent knowledge, code intelligence, agent delegation and workflows. | 184 | 0 | 2026-09-19 | 3 |
| AIPass | [GitHub](https://github.com/AIOSAI/AIPass) | CLI scaffold for agent mailboxes, memory, planning and shared-workspace collaboration. | 277 | 1 | 2026-09-20 | 6 |
| Backlog.md | [GitHub](https://github.com/MrLesk/Backlog.md) | Git-local Markdown tasks with dependencies, acceptance criteria, CLI/MCP access and boards. | 6,786 | 49 | 2026-09-18 | 61 |
| Cabinet | [Website](https://runcabinet.com/) | Markdown/Git knowledge workspace with agent-assisted team workflows. | — | — | — | — |
| Emergent Learning Framework (ELF) | [GitHub](https://github.com/Spacehunterz/Emergent-Learning-Framework_ELF) | **Archived.** Claude Code memory and learning framework with pattern tracking and coordination. | 208 | 2 | 2026-01-29 | 4 |
| links-issue-tracker (lit) | [GitHub](https://github.com/promptctl/links-issue-tracker) | Git-local issue tracker backed by Dolt SQL, designed for agent-driven updates. | 2 | Disabled | 2026-09-19 | 6 |
| LLM Memory | [GitHub](https://github.com/jeffdafoe/llm-memory-api) | Editable agent knowledge through MCP, with shared discussion and voting features. | 13 | 0 | 2026-09-15 | 3 |
| Memspec | [GitHub](https://github.com/siimvene/memspec) | Versioned Markdown memory with provenance, code anchors and searchable claims. | 8 | 0 | 2026-09-16 | 2 |
| Mimir | [GitHub](https://github.com/orneryd/Mimir) | Graph-based persistent agent memory connecting architectural knowledge, tasks and code. | 286 | 5 | 2025-12-25 | 2 |
| MUON | [GitHub](https://github.com/Sweetdevil144/muon) | Human-confirmed memory and code graphs supporting change-impact checks around coding CLIs. | 6 | 0 | 2026-09-19 | 1 |
| MyVibe | [GitHub](https://github.com/davidMcM84/my-vibe) | SQLite-backed BMAD context store with tasks, invariants, logs and a dashboard. | 2 | 0 | 2026-08-09 | 3 |
| Orbit | [GitHub](https://github.com/itsamruth/orbit) | Local coding-session history, checkpoints and bounded handoffs between agent providers. | 1 | 0 | 2026-09-15 | 1 |
| pi-agenticoding / Pi Schematic | [GitHub](https://github.com/chunkhound/pi-schematic) | Pi extension using persistent workstream notebooks and fresh contexts for delegated tasks. | 52 | 13 | 2026-09-18 | 2 |
| Swarm Tools | [GitHub](https://github.com/joelhooks/swarm-tools) | Agent coordination tools for task storage, file reservations, messaging and checkpoints. | 740 | 30 | 2026-07-30 | 12 |
| Task Master | [GitHub](https://github.com/eyaltoledano/claude-task-master) | AI-assisted task decomposition and tracking for coding projects. | 28,085 | 163 | 2026-04-28 | 72 |

## 7. Testing, code understanding and infrastructure

Supporting tools for evaluation, repository exploration, routing and execution environments.

| Name | Link | Description | Stars | Issues | Last updated | Contributors |
| --- | --- | --- | ---: | ---: | --- | ---: |
| Agentic Coding Flywheel Setup | [GitHub](https://github.com/Dicklesworthstone/agentic_coding_flywheel_setup) | Ubuntu environment bootstrap for coding agents, sessions and coordination tools. | 1,647 | 7 | 2026-09-19 | 3 |
| Bernstein | [GitHub](https://github.com/sipyourdrink-ltd/bernstein) | Framework for declarative execution rules and verifiable workflow records. | 1,209 | 262 | 2026-09-20 | 112 |
| Claworc | [GitHub](https://github.com/gluk-w/claworc) | OpenClaw instance management with fleet supervision and credential controls. | 242 | 3 | 2026-09-18 | 11 |
| CodeGraph | [GitHub](https://github.com/colbymchenry/codegraph) | Repository code graph for navigating relationships and supplying coding context. | 71,509 | 179 | 2026-09-16 | 59 |
| GitNébula | [GitHub](https://github.com/jundymek/gitnebula) | Offline repository maps from imports, file size, Git history and co-change. | 0 | 0 | 2026-09-10 | 2 |
| harness-bench-fast | [GitHub](https://github.com/ai-forever/harness-bench-fast) | Benchmark project for comparing agent harness and model configurations. | 53 | 5 | 2026-09-08 | 12 |
| Hedgehog PROSE Engineering | [GitHub](https://github.com/skyf0xx/hedgehog-core-copywriting-prose-engineering) | Copywriting workflow combining agent drafts with executable checks and revision loops. | 11 | 0 | 2026-09-19 | 2 |
| i-have-audhd | [GitHub](https://github.com/H-Freax/i-have-audhd) | Portable review skill separating verified outcomes from assumptions and untested claims. | 0 | 0 | 2026-09-14 | 1 |
| local-benchmark-runner-public | [GitHub](https://github.com/raydeStar/local-benchmark-runner-public) | Local-model evaluation runner with public task banks and campaign artifacts. | 0 | 0 | 2026-07-25 | 1 |
| Mac MCP | [GitHub](https://github.com/bulutarkan/mac-mcp) | MCP tools for agent interaction with a macOS desktop. | 70 | 0 | 2026-09-18 | 2 |
| Multi-MCP | [GitHub](https://github.com/religa/multi_mcp) | MCP server for multi-model answers, critique, analysis and code review. | 35 | 1 | 2026-09-05 | 4 |
| Multree | [GitHub](https://github.com/gileze33/multree) | Manages coordinated Git worktrees and environment setup across multiple repositories. | 2 | 8 | 2026-09-13 | 6 |
| Octocode | [GitHub](https://github.com/Muvon/octocode) | Code exploration and search tools for agent-assisted repository understanding. | 475 | 4 | 2026-09-19 | 8 |
| OrbiqD BriefKit | [GitHub](https://github.com/orbiqd/orbiqd-briefkit) | CLI/MCP adapter for invoking coding agents, continuing conversations and recording executions. | 26 | 0 | 2026-05-12 | 3 |
| pi-vs-claude-code | [GitHub](https://github.com/disler/pi-vs-claude-code) | Collection of Pi extensions demonstrating hooks, tools and coding-agent workflow patterns. | 1,690 | 11 | 2026-07-10 | 2 |
| Plano | [GitHub](https://github.com/katanemo/plano) | AI proxy handling model/agent routing, filters and telemetry outside application code. | 7,057 | 110 | 2026-08-19 | 45 |
| Rill | [Website](https://userill.dev) | Browser evidence-capture tool described in discussion; product page could not be verified. | — | — | — | — |
