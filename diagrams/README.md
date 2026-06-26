# Diagrams

Mermaid sources for the [case study](../README.md). Each also appears inline in the doc it supports;
they're collected here so the whole system can be skimmed visually in one place. All are validated to
render on GitHub.

| Diagram | What it shows | Type | Doc |
|---------|---------------|------|-----|
| [system-architecture](system-architecture.md) | Two execution planes + GitHub + human gates | flowchart | [01](../docs/01-system-architecture.md) |
| [publish-sync-sequence](publish-sync-sequence.md) | One publish + one sync cycle as cross-system calls | sequence | [01](../docs/01-system-architecture.md) · [02](../docs/02-autonomous-pipeline.md) |
| [cron-orchestration](cron-orchestration.md) | The 10 crons by model lane + dependencies | flowchart | [02](../docs/02-autonomous-pipeline.md) |
| [cron-schedule](cron-schedule.md) | The same crons across a UTC day (the 6-hour rhythm) | flowchart | [02](../docs/02-autonomous-pipeline.md) |
| [discovery-flow](discovery-flow.md) | Signal → live, mirrored catalog entry | flowchart | [02](../docs/02-autonomous-pipeline.md) |
| [skill-lifecycle](skill-lifecycle.md) | A skill's states to the `security_reviewed` tier | state | [05](../docs/05-quality-and-trust.md) |
| [human-approval-flow](human-approval-flow.md) | Autonomous vs propose-only resolution | flowchart | [04](../docs/04-human-in-the-loop.md) |
| [star-attribution](star-attribution.md) | The star bug, before/after the source-side fix | flowchart | [06](../docs/06-case-study-star-bug.md) |
