# Cron Inventory (sanitized sample)

The live OpenClaw cron registry, with infrastructure abstracted. This is the operational map of the
[autonomous pipeline](../docs/02-autonomous-pipeline.md); the authoritative, un-abstracted version
is maintained separately in private operations docs.

| Cron | Schedule | Model | Writes WP | Writes Repo | Writes Queue |
|------|----------|-------|:---------:|:-----------:|:------------:|
| Discovery Scout Replenish | `20 3 * * *` | `gpt-5.5` | no | no | yes |
| Discovery Intake + Approval | `10 */6 * * *` | `gpt-5.5` | no | no | yes |
| Discovery Publishing | `55 */6 * * *` | `gpt-5.4-mini` | yes | no | yes |
| GitHub Sync | `25 1,7,13,19 * * *` | `gpt-5.4-mini` | yes | yes | no |
| Daily Verification Scan + Signals | `45 7 * * *` | `gpt-5.4-mini` | yes | no | no |
| Data Enrichment Sweep | `40 2 * * *` | `gpt-5.4` | yes | no | no |
| Daily Smoke Test | `0 5 * * *` | `gpt-5.4-mini` | no | no | no |
| Weekly Quality + Repo Normalization | `45 13 * * 0` | `gpt-5.4` | no | yes | no |
| Chief of Staff Improvement Pass | `15 14 * * *` | `gpt-5.5` | no | no | no |
| Daily Blog Publisher | `45 11 * * *` | `gpt-5.5` | yes | no | no |

**Reading the "Writes" columns:** the surfaces a cron may touch define its blast radius. Only four
crons write WordPress, only two write the public repo, and the observation crons (Smoke) write
nothing. The high-frequency writers (Publishing, GitHub Sync — every 6h) run on the smaller model
because the judgment was already made upstream by the `gpt-5.5` discovery agents.

**Model lanes:** judgment → `gpt-5.5`; mid mechanical → `gpt-5.4`; mechanical/script-heavy →
`gpt-5.4-mini`. See [docs/03](../docs/03-model-strategy.md).

> Each cron also carries (in its operating brief) a success signal, common-failure list, a read-only
> verification command, and a human-intervention trigger. Those operational details are kept in
> private operations docs, not here.
