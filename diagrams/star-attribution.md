# Diagram · Star-Attribution Bug (before → after)

How a monorepo's star count wrongly propagated to every sub-skill, and how the source-side fix stops
it. Full story in [docs/06](../docs/06-case-study-star-bug.md).

```mermaid
flowchart TB
  subgraph Before["Before — repo-level count inherited"]
    direction TB
    S1["source: github.com/openclaw/openclaw /tree/main/skills/audit-openclaw"]
    R1["enrichment resolves owner/repo<br/>(strips the /tree/branch/subpath suffix)"]
    P1["owner/repo = openclaw/openclaw"]
    G1["GitHub API → 356.8k stars (whole monorepo)"]
    W1["stored: audit-openclaw.github_stars = 356.8k"]
    Sib["every sibling sub-skill inherits the same 356.8k"]
    B1["TOP-STARS skewed toward monorepo sub-skills"]
    S1 --> R1 --> P1 --> G1 --> W1 --> Sib --> B1
  end
  subgraph After["After — source-side fix"]
    direction TB
    S2["same monorepo-subdir source"]
    D2["enrichment detects: source points INTO a subdir"]
    X2["drop github_stars — no inheritance"]
    W2["audit-openclaw has no github_stars field"]
    B2["TOP-STARS ranks real single-repo tools"]
    S2 --> D2 --> X2 --> W2 --> B2
  end
```
