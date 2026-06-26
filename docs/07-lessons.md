# 07 · Lessons

What generalises from ASE to any autonomous content or data system. These are the load-bearing
design choices — the ones that, removed, would make "operate a public product without a human in the
daily loop" indefensible.

## 1. Separate the planner from the executors

The expensive, occasional, must-be-right thinking (architecture, root-cause, review) runs on a strong
planning model under human supervision. The cheap, continuous, mostly-mechanical work runs on a fleet
of smaller executor agents. Conflating the two either bankrupts you (everything on the big model) or
makes the system dumb where it matters (everything on the small one). **Plan rarely and well; execute
often and cheaply.**

## 2. Separate generation from verification

The agent that *creates* content must never be the agent that *trusts* it. ASE enforces trust tiers,
counts, and structure in passes that are independent of generation — and with deterministic code, not
a second model grading the first. A confident wrong answer can't promote itself when something else
holds the gate.

## 3. Use code for invariants, models for judgment

Coverage, schema, counts, tier integrity, TOC-leak detection, star-provenance — all deterministic, so
plain code checks them perfectly at zero token cost and with a reproducible verdict. Reserve models
for what's genuinely subjective: "is this skill worth cataloguing?", "is this blog post good?". An LLM
judge for deterministic properties is slower, costlier, and non-deterministic — strictly worse.

## 4. Make the catalog a renderer, not a source of truth

Keeping one system of record (WordPress) and treating the public repo as a *rendering* of it gave the
[star bug](06-case-study-star-bug.md) exactly one place to live. Two sources of truth means two places
for data to diverge and twice the debugging surface. One writer, many renderers.

## 5. Fix where data is written, not where it's read

A guard at the read side stops the symptom but must run forever if the bad value keeps arriving. The
durable fix lands at the writer. Ship the read-side workaround if you must — but label it a workaround
and migrate the fix upstream.

## 6. Fail closed, then ask

The default on uncertainty is **stop and surface**, never **push through**. Publishing fails closed on
security/provenance; sync validates before pushing; a rejected run leaves the last good state serving.
Each agent knows the conditions under which it should stop and ask for a human. An autonomous system
that fails *open* is just an unmonitored one.

## 7. Draw the human-approval line narrowly and explicitly

Automation owns the high-volume, reversible decisions; a human owns the few that are broad, public, or
behaviour-altering (merges, production config, model/auth, trust policy, force-publish, collapse
recovery). Writing that list down — and keeping it short — is what makes the autonomy both safe and
useful. A fuzzy line becomes either a bottleneck or a liability.

## 8. Tier your models to where judgment is decided

Within the executor fleet, the strongest model goes where quality is *decided* (discovery approval,
editorial), and the smallest goes where *scripts* enforce the gates (publish, sync). Because judgment
happens upstream, the high-frequency mechanical lanes can run cheaply without lowering quality. Cost
then scales with mechanical volume, not with the price of the smartest model.

## 9. Every run leaves evidence

Decisions logs, publish reports, smoke/weekly reports, a one-command read-only health check, and a
symptom→runbook map. Cheap observability is what lets a human supervise a fleet by *exception* instead
of by *polling* — the difference between oversight that scales and oversight that doesn't.

## 10. Name what a fix doesn't cover

The star guard's own log says it doesn't correct wrong-repo matches or stale counts. Residual issues
get named and scoped, not silently folded in. Honesty about a fix's boundary is what keeps the next
person (or the next agent) from assuming a problem is solved when it isn't.

---

### The through-line

Every lesson is a variation on one theme: **put judgment where it's expensive and rare, put
enforcement where it's cheap and deterministic, and make the boundary between "the machine decides"
and "the human decides" explicit and small.** That's what turns "a bunch of agents on cron" into a
system you can trust with a public product.

---

[← The star-attribution bug](06-case-study-star-bug.md) · [Contents](../README.md#read-it-in-order)
