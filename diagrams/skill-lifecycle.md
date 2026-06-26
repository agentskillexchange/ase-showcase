# Diagram · Skill Trust Lifecycle

A skill's states from discovery to the public `security_reviewed` trust tier — including the
fail-closed and rejection branches. See [docs/04](../docs/04-human-in-the-loop.md) and
[docs/05](../docs/05-quality-and-trust.md).

```mermaid
stateDiagram-v2
  [*] --> Reservoir
  Reservoir --> Candidate: Intake handoff
  Candidate --> Rejected: duplicate or weak
  Candidate --> Approved: passes review
  Approved --> Held: fails closed (security/provenance)
  Approved --> Listed: publishing gates pass
  Held --> Listed: human approves
  Listed --> SecurityReviewed: verification confirms trust
  SecurityReviewed --> Listed: trust regresses, re-review
  Rejected --> [*]
  note right of SecurityReviewed
    Public trust tier.
    Never applied to boilerplate.
  end note
```
