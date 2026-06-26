# Diagram · Cron Orchestration

The ten scheduled agents over a day, grouped by model lane. Schedules and models are the live values;
see [docs/02](../docs/02-autonomous-pipeline.md) and [docs/03](../docs/03-model-strategy.md).

```mermaid
flowchart TB
  subgraph J["Judgment lane · gpt-5.5"]
    Scout["Discovery Scout<br/>20 3 * * *"]
    Intake["Intake + Approval<br/>10 */6 * * *"]
    Cos["Chief of Staff<br/>15 14 * * *"]
    Blog["Blog Publisher<br/>45 11 * * *"]
  end
  subgraph M["Mid lane · gpt-5.4"]
    Enrich["Data Enrichment Sweep<br/>40 2 * * *"]
    Weekly["Weekly Quality + Repo Norm<br/>45 13 * * 0"]
  end
  subgraph Mini["Mechanical lane · gpt-5.4-mini"]
    Publish["Publishing<br/>55 */6 * * *"]
    Sync["GitHub Sync<br/>25 1,7,13,19 * * *"]
    Verify["Verification + Signals<br/>45 7 * * *"]
    Smoke["Smoke Test<br/>0 5 * * *"]
  end

  Scout --> Intake --> Publish --> Sync
  Enrich --> Publish
  Verify --> Publish
  Verify --> Sync
  Cos -.reviews.-> Scout
```
