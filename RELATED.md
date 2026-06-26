# How this repo fits the ASE family

ASE is spread across several repositories with deliberately separate jobs. This showcase is the
**engineering narrative**; it links out to the public ones rather than duplicating them.

| Repo | Job | This repo's relationship |
|------|-----|--------------------------|
| [`agentskillexchange/skills`](https://github.com/agentskillexchange/skills) | **Canonical catalog** — `SKILL.md` per skill, generated `CATALOG.md` / `TOP-STARS.md` / `TOP-DOWNLOADS.md`, and the machine-readable `skills.json` / `openclaw.json` / `codex.json`. | The *output* this case study explains. |
| `agent-skills-resources` | **Educational companion** — guides, cookbook, framework comparisons, ecosystem maps. | Adjacent reader resource; we link, we don't overlap. |
| `verification-security` | **Security review records** backing the public `security_reviewed` trust tier. | Cited from [docs/05](docs/05-quality-and-trust.md) as the auditable basis for the trust signal. |
| **this repo** (`ase-showcase`) | **Engineering case study** — what was built, why, and how the autonomous loop works. | Portfolio-grade systems narrative; public-safe. |

### Where to go for what

- *"How does the system work conceptually?"* → you're in the right place.
- *"I want to install or browse a skill."* → [`agentskillexchange/skills`](https://github.com/agentskillexchange/skills) / [agentskillexchange.com](https://agentskillexchange.com/).
- *"How do I learn to write good agent skills?"* → `agent-skills-resources`.

### Boundary rule

This repo is about *the design and the story*. Anything about *operating or recovering* the live
system — exact hosts, recovery procedures, day-2 runbooks, live state — is kept in **separate,
private operations docs** and is intentionally not included or linked here, so this repo stays
public-safe.
