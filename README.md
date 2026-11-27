# Rastrix

**Open source AI agent that finds the root cause of your incidents.**

Connect Rastrix to your Grafana and Slack. When something breaks, ask it to look at a time window: it reads your metrics, traces and logs, compares them with similar past incidents and replies with the probable cause, the evidence behind it and a suggested fix.

Rastrix is read-only. It explains, you decide.

> 🚧 **Work in progress.** Rastrix is in early development and not ready to use yet.

## Planned features

- Investigates every alert in a time window and returns one report
- Reads metrics, traces and logs through the Grafana MCP server
- Learns from your post-mortems and runbooks (RAG with Postgres + pgvector)
- Works with any model on OpenRouter, using your own API key
- Runs locally with Docker Compose
- Includes a demo environment that breaks a sample API on purpose, so you can see the agent in action

## Built with

TypeScript · LangGraph.js · OpenTelemetry · Grafana LGTM · Postgres + pgvector · Docker

## Contributing

Ideas and feedback are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
