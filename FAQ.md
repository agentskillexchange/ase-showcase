# FAQ

The questions a sharp reader tends to form while reading the [docs](README.md#read-it-in-order).
Short answers here; the full reasoning is in the linked doc.

### What is "OpenClaw"?

The scheduler/runtime on the VPS that owns the cron registry and runs each scheduled task as a
model-backed agent. It is *also* the name of an agent project whose own skills appear **in** the
catalog — so `openclaw/openclaw` shows up in the [star-bug case study](docs/06-case-study-star-bug.md)
as a cataloged monorepo. Same name, two roles; the docs flag this where it could confuse.

### Why is WordPress the source of truth instead of the Git repo?

So there is exactly **one** writer. WordPress holds live skill data and applies enrichment; the
public repo is a *renderer* of it. Two sources of truth means two places to diverge and twice the
debugging surface — the [star bug](docs/06-case-study-star-bug.md) was localised to a single fix site
precisely because the repo only renders. See [docs/01](docs/01-system-architecture.md).

### Why not add an "LLM judge" to grade the agents?

Because the properties that must hold — coverage, schema, counts, tier integrity, TOC-leak
detection, star provenance — are **deterministic**, so plain code checks them perfectly at zero token
cost with a reproducible verdict. A second model would cost more, be non-deterministic, and could
mis-pass. Models generate and judge *taste*; code enforces *invariants*. See
[docs/05](docs/05-quality-and-trust.md).

### How do you keep agents from publishing junk?

Five independent checkpoints, none of which trust the generator: a fail-closed **body-quality gate**,
the **publish gate** (security + provenance), **validate-before-push** on sync, the repo's CI
(`validate.yml` + `security-scan.yml`), and the daily **verification/smoke audits**. Publishing
**fails closed** — a questionable skill simply doesn't go live. See
[docs/05](docs/05-quality-and-trust.md) and [docs/04](docs/04-human-in-the-loop.md).

### Is a human ever strictly required?

Yes — for the changes that are broad, public, or behaviour-altering: PR merges / broad repo rewrites,
WordPress/plugin/theme changes, OpenClaw provider/model/auth changes, security/trust policy,
discovery-lane expansion, force-publish, and recovery from a count collapse. Everything else — the
daily discover → publish → sync → verify loop — runs autonomously. See
[docs/04](docs/04-human-in-the-loop.md).

### What happens when the GPT model versions change?

A model swap is treated as a **production-config change**: human-reviewed, never done casually, and
not changed during an incident unless the model itself is the incident. Quality doesn't hinge on the
mechanical lanes' model because **scripts enforce the gates** — the judgment was already made upstream
by the stronger model. See [docs/03](docs/03-model-strategy.md).

### How is runaway cost prevented?

Frequency × model cost is dominated by the high-frequency *mechanical* lanes (Publishing, GitHub Sync
— every 6h), which run on the smallest model (`gpt-5.4-mini`). The judgment-bearing work is a handful
of runs a day on the stronger model. So running cost scales with mechanical volume, not with the
price of the smartest model. (Actual dollar figures are operational metrics, intentionally not
published here.) See [docs/03](docs/03-model-strategy.md).

### Why two providers — Claude *and* GPT?

They sit at different levels. **Claude Opus** is the *planner/architect* — the occasional,
must-be-right thinking (design, review, root-cause). **GPT-5.x** models are the *execution engine* —
the continuous, mostly-mechanical recurring work, inside the OpenClaw/Codex-style harness. Plan
rarely and well; execute often and cheaply. See [docs/03](docs/03-model-strategy.md).

### Can I verify any of this independently?

Yes — see [How to verify this](README.md#how-to-verify-this): the live `skills.json` / `openclaw.json`
/ `codex.json` / `llms.txt` manifests, the public catalog repo and its CI workflows, and the
`verification-security` records.
