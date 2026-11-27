# Contributing to Rastrix

Thanks for your interest. This guide explains how work flows in this repository.

## Workflow

1. **Pick an issue.** Every change starts from an issue. Check the [project board](https://github.com/jaugustodev/rastrix/projects) and the [milestones](https://github.com/jaugustodev/rastrix/milestones). Comment on the issue before you start.
2. **Create a branch** from `main`:
   - `feat/<issue>-short-name` for features
   - `fix/<issue>-short-name` for bug fixes
   - `chore/<issue>-short-name` for tooling, infra and config
   - `docs/<issue>-short-name` for documentation

   Example: `feat/12-otel-traces`
3. **Commit** using [Conventional Commits](https://www.conventionalcommits.org/):
   - `feat(api): add health route`
   - `fix(agent): stop loop after max steps`
   - `chore(infra): add pgvector to compose`
   - `docs(readme): add architecture diagram`
4. **Open a pull request** using the template. Link the issue with `Closes #<issue>`.
5. **CI must pass** (lint, typecheck, tests).
6. **Squash merge** into `main`. Delete the branch.

## Releases

Each milestone (phase) ends with a release following [Semantic Versioning](https://semver.org/):

```bash
gh release create v0.1.0 --generate-notes --title "v0.1.0 - Foundation"
```

## Labels

- `type:*` says what kind of work it is (feature, chore, docs, bug, decision, learning).
- `area:*` says which part of the system it touches (api, infra, telemetry, incidents, alerting, rag, agent, eval, frontend, deploy).

## Code of conduct

Be respectful and constructive. Assume good intent.
