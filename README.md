# Hermes Research Skill

A lightweight, evidence-first `/research` skill for Hermes Agent.

It is designed for **ordinary investigation**, not heavyweight deep research: establish the current facts, cover the important dimensions, reconcile conflicting evidence, reconstruct the logic, and give one practical recommendation.

## What it does

The skill follows a compact research workflow:

**Scope & coverage frame → date/version grounding → source strategy → adaptive 1–3 round research → counter-evidence → evidence discipline → logic reconstruction → solution feasibility check → concise recommendation**

Key behaviors:

- defines the important investigation dimensions before searching
- prioritizes primary sources such as official docs, source code, releases, issues, PRs, commits, papers, model cards, and first-party statements
- reads important sources in full instead of relying on search snippets
- actively searches for evidence that could weaken the leading explanation
- distinguishes verified facts, single-source facts, inference, and unknowns
- checks version, platform, configuration, and historical differences before treating sources as contradictory
- stops when additional research is unlikely to change the recommendation
- recommends one practical path by default instead of dumping equal-weight options

## Install

Place `SKILL.md` in your Hermes skills directory as:

```text
~/.hermes/skills/research/SKILL.md
```

Once loaded by Hermes, use it as:

```text
/research <your question>
```

Example:

```text
/research Investigate why Hermes Desktop Remote Gateway depends on Profile, verify the current implementation and relevant issues/PRs, then recommend the most practical improvement.
```

## Design goal

This project intentionally sits between a one-shot web lookup and a full multi-agent deep-research system.

The target use case is:

> “I need this checked properly before I act, but I do not need a 20-source research report.”

## Design provenance

The workflow was built by reviewing and selectively combining ideas from several existing research-skill projects, including:

- moonlight-lupin / `agent-skills` — adaptive rounds, counter-evidence search, evidence states, stop conditions
- ByteDance / `deer-flow` — broad exploration, dimension discovery, full-source reading, gap checks
- Weizhena / `Deep-Research-skills` — research outline / fields before collection
- 199-biotechnologies / `claude-deep-research-skill` — claim-level verification and source-cluster independence
- witt3rd / `oh-my-hermes` — decomposition, synthesis, verification, selective delegation
- NousResearch / Hermes Agent `parallel-cli` — keep Hermes-native web tools as the default for ordinary research

See [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) for the detailed design provenance and the parts that were deliberately not adopted.

## Files

- `SKILL.md` — the runtime Hermes skill
- `DESIGN_NOTES.md` — design provenance and rationale
- `LICENSE` — MIT License

## License

MIT
