# Diagram · Human Approval Flow

How a run resolves: autonomous when reversible and gated; proposed-only when broad/public/
behaviour-altering. See [docs/04](../docs/04-human-in-the-loop.md).

```mermaid
flowchart TD
  Run["Agent run"] --> Gate{"Passes deterministic<br/>+ security gates?"}
  Gate -- no --> Hold["Hold · keep last good state"] --> Notify["Report + Telegram op"]
  Gate -- yes --> Risky{"Broad / public /<br/>behaviour-altering?"}
  Risky -- no --> Auto["Apply autonomously"]
  Risky -- yes --> Propose["Propose only<br/>(write proposal, no prod write)"]
  Notify --> Human(["Human decides"])
  Propose --> Human
  Human -->|approve| Apply["Apply via single gated path"]
  Human -->|reject| Drop["Drop / revise"]
```

**Always-human changes:** PR merges & broad rewrites · WP/plugin/theme · OpenClaw provider/model/auth
· security/trust policy · discovery-lane expansion · force-publish · count-collapse recovery.
