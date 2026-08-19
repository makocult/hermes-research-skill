# Research Skill v2 — Design Provenance

This file documents which external research-skill designs were reviewed before producing `SKILL.md`. It is intentionally kept outside the runtime skill so the skill itself stays compact.

## 1. moonlight-lupin / agent-skills — deep-research v1.5.0

Reviewed:
- `research/deep-research/SKILL.md`

Ideas retained:
- adaptive maximum rounds rather than fixed-depth research
- gap-driven subsequent queries
- explicit counter-evidence / refute-polarity search
- empty-search refinement and eventual stop
- source-quality classification
- separation of Verified / Sourced / Reasoned / Estimated evidence basis
- explicit stopping checks
- important-source full extraction instead of snippet-only reasoning
- do not delegate final synthesis

Ideas deliberately removed or softened:
- 800-word minimum report
- visible research statistics
- evidence.json requirement
- fixed source-quality percentages/weights
- report-first formatting
- large token-budget machinery

Why: those are useful for deep research reports but too heavy for ordinary day-to-day investigation.

## 2. ByteDance / deer-flow — deep-research skill

Reviewed:
- `skills/public/deep-research/SKILL.md`

Ideas retained:
- broad exploration before narrow deep dives
- derive research dimensions from initial landscape
- explicitly seek different information types and opposing/challenging views
- fetch/read important sources in full
- iterative gap identification
- current-date precision in search
- research quality check before synthesis
- warning against stopping after only one superficial search

Adaptation:
- DeerFlow's generic "3–5 angles / examples / expert views / trends" checklist was converted into dynamic investigation dimensions, because technical/product investigations do not always need market trends or expert opinion.

## 3. Weizhena / Deep-Research-skills

Reviewed:
- repository workflow and `/research`, `/research-add-items`, `/research-add-fields`, `/research-deep`
- `research-deep/SKILL.md`

Ideas retained:
- build an outline before collecting facts
- define fields/dimensions before comparison so coverage is consistent
- make missing/uncertain fields explicit
- validate coverage rather than merely accumulate search results
- human-in-the-loop extensibility as a design principle

Adaptation:
- V2 keeps the outline/fields idea internally as a "scope and coverage frame" rather than requiring YAML files or an explicit multi-step user approval workflow, because this skill targets ordinary investigations rather than batch research projects.

## 4. 199-biotechnologies / claude-deep-research-skill

Reviewed:
- top-level `SKILL.md`

Ideas retained:
- clear decision tree separating lookup vs research
- SCOPE → PLAN → RETRIEVE → TRIANGULATE → SYNTHESIZE logic
- claim-level verification mindset
- evidence persistence concept as inspiration
- "cluster-independent" corroboration: several pages repeating the same underlying source are not independent evidence
- explicit limitations/caveats and recommendation phase

Ideas deliberately removed:
- 10+ source minimum
- 3+ citations per major finding
- 18K-word report support
- JSONL evidence/claim registries
- HTML/PDF packaging
- mandatory critique/refine phases for ordinary research

Why: excellent safeguards for high-stakes comprehensive reports, excessive for the intended everyday `/research` workflow.

## 5. witt3rd / oh-my-hermes — omh-deep-research

Reviewed:
- repository description, workflow architecture, cost envelope and Hermes-specific constraints

Ideas retained:
- decompose research before searching
- separate researcher / synthesis / verification responsibilities conceptually
- verify citations from delegated research
- parallelize only truly independent research branches

Ideas deliberately not adopted as the default:
- 3–5 researcher subagents
- dedicated synthesizer + verifier on every run
- 5–8+ delegate-task calls on the happy path

Why: the user asked for normal research rather than heavyweight multi-agent deep research.

## 6. NousResearch / Hermes Agent — parallel-cli

Reviewed:
- official optional `parallel-cli/SKILL.md`

Ideas retained:
- Hermes native `web_search` / `web_extract` should remain the default for ordinary lookups/research
- vendor-specific or paid research infrastructure should be an escalation, not an implicit dependency

## Resulting design

The final v2 workflow is intentionally a hybrid:

**Scope / coverage frame**
→ **date & version grounding**
→ **source strategy**
→ **adaptive 1–3 round research**
→ **counter-evidence**
→ **claim/evidence discipline**
→ **logic reconstruction**
→ **solution feasibility test**
→ **compact answer**

The important change from v1 is that "coverage" is now a first-class step. The agent must decide what dimensions must be checked before it starts searching, rather than relying on whatever the first search happens to surface.
