# Diagram · Publish + Sync Handshake

One publishing cycle and one GitHub-sync cycle, as the cross-system calls between the OpenClaw cron,
WordPress, GitHub, and CI. Shows where it **fails closed** and where validation gates the push. See
[docs/01](../docs/01-system-architecture.md) and [docs/02](../docs/02-autonomous-pipeline.md).

```mermaid
sequenceDiagram
  autonumber
  participant Cron as OpenClaw cron (GPT-5.x)
  participant WP as WordPress (ase-marketplace-layer)
  participant GH as GitHub (skills)
  participant CI as CI (validate + security-scan)

  Note over Cron: Publishing — every 6h (5.4-mini)
  Cron->>WP: read approved queue
  Cron->>Cron: run quality + security gates
  alt gates pass
    Cron->>WP: publish skill post
    WP-->>Cron: ok, cache purged
  else fails closed
    Cron-->>Cron: hold, surface to human
  end
  Note over Cron: GitHub Sync — 4x/day (5.4-mini)
  Cron->>WP: GET /wp-json/ase-marketplace/v1/browse
  WP-->>Cron: live skill signals
  Cron->>Cron: render SKILL.md + CATALOG + TOP-*
  Cron->>GH: validate, then git push
  GH->>CI: validate.yml + security-scan.yml
  CI-->>GH: pass, catalog updated
```
