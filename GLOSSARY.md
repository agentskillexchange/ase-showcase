# Glossary

Terms used throughout this repo.

| Term | Meaning |
|------|---------|
| **ASE** | Agent Skill Exchange — the product ([agentskillexchange.com](https://agentskillexchange.com/)) and its canonical catalog ([`agentskillexchange/skills`](https://github.com/agentskillexchange/skills)). |
| **OpenClaw** | The scheduler/runtime on the VPS that owns the cron registry, runs each scheduled task as a model-backed agent, and authenticates to GitHub via the `gh` CLI. The execution engine of the system. |
| **Codex-style harness** | The agent-execution loop the GPT models run inside (tool use + repo/file operations), driving the recurring work OpenClaw schedules. |
| **Cron / scheduled agent** | One entry in OpenClaw's registry — a fixed schedule, a chosen model, and a defined set of surfaces it may write. There are ten. See [docs/02](docs/02-autonomous-pipeline.md). |
| **Model lane** | The tier a cron's model sits in: *judgment* (`gpt-5.5`), *mid* (`gpt-5.4`), *mechanical* (`gpt-5.4-mini`). See [docs/03](docs/03-model-strategy.md). |
| **Reservoir** | The pool of pending discovery candidates the Scout keeps above a floor, so Intake always has fresh, source-backed skills to review. |
| **Intake / Approval** | The editorial step that vets reservoir candidates, rejects duplicates/weak entries with reasons, and writes the approved queue. Nothing it does is public yet. |
| **Enrichment** | Refreshing a skill's ecosystem signals (GitHub stars, npm downloads, source provenance). The step at the centre of the [star-attribution case study](docs/06-case-study-star-bug.md). |
| **Manifest** | An agent-discovery file served at the site root (`openclaw.json` / `codex.json` / `skills.json`, schema `openclaw-skills/1.0`, plus `llms.txt`) — how external agent runtimes find the catalog. |
| **`security_reviewed`** | The public trust tier. A gated *claim about safety*; boilerplate is never published as `security_reviewed`. See [docs/05](docs/05-quality-and-trust.md). |
| **Renderer, not source of truth** | Design choice: WordPress is the system of record; the public repo *renders* it from the `/browse` API. One writer, many renderers — which localised the [star bug](docs/06-case-study-star-bug.md) to a single fix site. |
| **Fail closed** | On uncertainty, stop and surface rather than push through; the last known-good state keeps serving. The system's default failure mode. |
| **Propose, never publish** | At broad/public/behaviour-altering edges, agents write a proposal and a human applies it — there is exactly one path to production. See [docs/04](docs/04-human-in-the-loop.md). |
| **Blast radius** | The set of production surfaces a given cron may write (WordPress, the repo, the queue, or nothing) — how much a bad run of that agent could affect. |
| **Plane** | One of the two execution environments — the **OpenClaw VPS** (agents) and the **WordPress host** (data + product) — plus GitHub as the canonical catalog. |
