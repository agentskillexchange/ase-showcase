# Diagram · System Architecture

Two execution planes (OpenClaw VPS, WordPress host) plus the GitHub canonical catalog, with the human
approval gates. Source for the overview in [docs/01](../docs/01-system-architecture.md).

```mermaid
flowchart TB
  subgraph VPS["OpenClaw VPS — execution engine"]
    Sched["OpenClaw scheduler<br/>cron registry · Telegram ops · gh auth"]
    Agents["GPT-5.x agent runs"]
    Work["Workspace state<br/>reservoir · candidates · approved · decisions"]
    Sched --> Agents --> Work
  end
  subgraph WP["WordPress host — data + product"]
    Layer["ase-marketplace-layer plugin"]
    REST["/wp-json/ase-marketplace/v1/browse"]
    Out["openclaw.json · codex.json<br/>skills.json · llms.txt"]
    Layer --> REST
    Layer --> Out
  end
  subgraph GH["GitHub — canonical catalog"]
    Skills["agentskillexchange/skills"]
    CI["validate.yml · security-scan.yml"]
    Skills --> CI
  end
  Site([agentskillexchange.com])
  Human(["Human approval"])

  Agents -->|publish + enrich| Layer
  REST -->|read live state| Agents
  Agents -->|render + gh push| Skills
  Out --> Site
  Layer --> Site
  Human -.gates.-> Agents
  Human -.gates.-> Skills
```
