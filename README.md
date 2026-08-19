# Hermes Research Skill

[![Hermes Agent](https://img.shields.io/badge/Hermes-Agent-111111)](https://hermes-agent.nousresearch.com/)
[![Skill Version](https://img.shields.io/badge/skill-v2.0.0-blue)](./SKILL.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A lightweight, evidence-first `/research` skill for **Hermes Agent**.

It is designed for **ordinary investigation rather than heavyweight deep research**: establish the current facts, cover the important dimensions, reconcile conflicting evidence, reconstruct the logic, and recommend one practical next action.

> **Use it when you need something checked properly before acting, but you do not need a 20-source research report.**

## Why this skill exists

A normal web search can find information, but it does not guarantee that the investigation covered the right dimensions or that the final conclusion follows from the evidence.

This skill adds a repeatable research method around Hermes' existing tools:

**Scope & coverage frame → date/version grounding → source strategy → adaptive 1–3 round research → counter-evidence → evidence discipline → logic reconstruction → solution feasibility check → concise recommendation**

The emphasis is on **coverage and judgment**, not maximum depth.

## Key behaviors

- Defines the important investigation dimensions **before** searching.
- Prioritizes primary evidence: official docs, source code, releases, issues, PRs, commits, papers, model cards, pricing/policy/status pages, and first-party statements.
- Reads important sources in full instead of reasoning from search snippets alone.
- Checks the actual current date, version, branch, platform, configuration, and feature context when they matter.
- Actively searches for evidence that could weaken or contradict the leading explanation.
- Distinguishes **verified facts, sourced facts, inference, and unknowns**.
- Treats multiple articles repeating one original source as one evidence cluster, not independent confirmation.
- Separates intended design, documented behavior, actual implementation, regressions, configuration issues, documentation drift, and UI ambiguity when relevant.
- Stops when further research is unlikely to change the recommendation.
- Recommends **one practical path by default** rather than dumping equal-weight options.

## Install

Hermes supports installing a single-file skill directly from an HTTP(S) `SKILL.md` URL.

```bash
hermes skills install https://raw.githubusercontent.com/makocult/hermes-research-skill/main/SKILL.md
```

Or install it manually:

```bash
mkdir -p ~/.hermes/skills/research
curl -L https://raw.githubusercontent.com/makocult/hermes-research-skill/main/SKILL.md \
  -o ~/.hermes/skills/research/SKILL.md
```

Installed skills become slash commands in Hermes. Start a new session after installing, or refresh the current session according to your Hermes version.

## Usage

```text
/research <your question>
```

Example:

```text
/research Investigate why Hermes Desktop Remote Gateway depends on Profile. Verify the current documented behavior, implementation, relevant issues/PRs, and version history, then recommend the most practical improvement.
```

Another example:

```text
/research Compare the current Q4_K_M and Q4_K_XL quantizations for this model. Prioritize primary benchmark evidence and implementation details, identify conflicting claims, and recommend which one I should deploy.
```

## What the final answer should look like

The skill favors a compact, decision-oriented result:

1. **Conclusion** — the answer first.
2. **What is established** — the facts that materially support it.
3. **How it fits together** — mechanism, timeline, dependency, or contradiction.
4. **Recommended action** — one practical next step.
5. **Remaining uncertainty** — only when something unresolved could matter.

It intentionally avoids arbitrary minimum word counts, giant bibliographies, visible research statistics, and report-length output unless the problem genuinely requires them.

## Research depth

The workflow is adaptive:

- **Quick** — 1 round for narrow questions with a clear source trail.
- **Normal** — up to 2 rounds for most investigations.
- **Extended** — up to 3 rounds only when a material contradiction, version mismatch, or missing causal link could change the recommendation.

These are ceilings, not targets.

## What this is not

This is not intended to replace:

- exhaustive academic literature review
- large-scale due diligence
- multi-agent deep research
- recurring monitoring
- implementation work after the facts and plan are already established

For those tasks, use a more specialized workflow.

## Design provenance

This skill was built by reviewing and selectively combining ideas from several existing research-skill projects rather than inventing the workflow from scratch.

Influences include:

- **moonlight-lupin / agent-skills** — adaptive rounds, counter-evidence search, evidence states, empty-search handling, stop conditions
- **ByteDance / DeerFlow** — broad exploration, dimension discovery, full-source reading, gap checks
- **Weizhena / Deep-Research-skills** — research outline and fields before information collection
- **199-biotechnologies / claude-deep-research-skill** — claim-level verification and source-cluster independence
- **witt3rd / oh-my-hermes** — decomposition, synthesis, verification, selective delegation
- **NousResearch / Hermes Agent parallel-cli** — keep Hermes-native web tools as the default for ordinary research

See [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) for the detailed provenance, what was retained, and what was deliberately left out.

## Repository structure

```text
.
├── SKILL.md          # Runtime Hermes skill
├── DESIGN_NOTES.md   # Design provenance and rationale
├── README.md
└── LICENSE            # MIT
```

## Contributing

Issues and pull requests are welcome, especially for:

- research-process edge cases
- examples where the workflow stops too early or too late
- source-evaluation failures
- Hermes compatibility changes
- improvements backed by real-world research workflows

The guiding principle is simple: **improve research completeness and judgment without turning ordinary research into an expensive deep-research pipeline.**

## License

MIT
