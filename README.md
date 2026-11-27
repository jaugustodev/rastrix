# Rastrix

**Rastrix Agent** is an open source AI agent, written in TypeScript, that investigates observability incidents. It reads metrics, logs and traces from Grafana (via MCP), compares them with similar past incidents (RAG over post-mortems) and explains the probable root cause with evidence. It never takes actions: the developer reads the report and decides.

> Status: **work in progress**. Follow the [roadmap](#roadmap) and the [issues](https://github.com/jaugustodev/rastrix/issues).

## How it works

1. A sample TypeScript API emits metrics, logs and traces with OpenTelemetry.
2. The Grafana LGTM stack (Loki, Grafana, Tempo, Mimir) stores everything.
3. k6 generates load and simulates failures on purpose.
4. Grafana alert rules notify Slack (and, for selected alerts, call the agent through a webhook).
5. Someone runs a Slack command with a time window (for example, the last 50 minutes).
6. The agent gathers the alerts in that window, searches similar cases in Postgres + pgvector, investigates metrics, traces and logs through the Grafana MCP, and replies in the alert thread with a single report: probable cause, evidence, confidence, timeline and suggested fix.

```
API (OpenTelemetry) ──> OTel Collector ──> Loki / Tempo / Mimir ──> Grafana
                                                                     │ alerts
                                          Slack <──── report ────── Rastrix agent (LangGraph)
                                                                     │        │
                                                          Grafana MCP ┘        └─> Postgres + pgvector (RAG)
```

*A full architecture diagram will replace this sketch.*

## Stack

| Layer | Technology |
|---|---|
| Language | TypeScript (Node.js) |
| Agent orchestration | LangChain.js + LangGraph.js |
| Model access | OpenRouter |
| Agent tools | Grafana MCP + custom TypeScript tools |
| Database / vectors | Postgres + pgvector |
| Telemetry | OpenTelemetry + OpenTelemetry Collector |
| Observability backend | Grafana LGTM (Loki, Grafana, Tempo, Mimir) |
| Load and failures | k6 |
| Alerts / notification | Grafana Alerting + Slack |
| Agent observability | Langfuse |
| Tests and evaluation | Vitest + simulated scenarios with ground truth |
| Local infra | Docker Compose |
| CI | GitHub Actions |

## Simulated incidents

| Scenario | Symptom |
|---|---|
| 1 | High rate of HTTP 500 errors |
| 2 | Slow API |
| 3 | Database down (timeouts) |

Each scenario has a known root cause, used as ground truth to measure how often the agent gets it right.

## Roadmap

| Phase | Milestone |
|---|---|
| 1 | [Foundation](https://github.com/jaugustodev/rastrix/milestones) |
| 2 | API telemetry |
| 3 | Simulated incidents |
| 4 | Alerting |
| 5 | Knowledge base (RAG) |
| 6 | Agent |
| 7 | Evaluation |
| 8 | Demo and presentation |
| 9 | AWS production |

## Design principles

- **Read-only.** The agent investigates and explains. It never restarts services or changes anything.
- **Evidence first.** Every root cause must point to the metrics, traces or logs that support it.
- **Bounded.** A maximum number of steps per investigation keeps cost and loops under control.
- **Model-agnostic.** Any model available on OpenRouter; bring your own API key.

## Getting started

Coming soon: `docker compose up` will start the whole stack locally.

## Contributing

Contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening an issue or pull request.

## License

[MIT](LICENSE)
