---
name: research
description: Structured, evidence-first research for establishing current facts, reconstructing logic, resolving contradictions, and recommending a practical next action. Use when a question needs more than a quick lookup but does not require exhaustive deep research.
version: 2.0.0
license: MIT
metadata:
  hermes:
    tags: [research, investigation, verification, analysis, decision-support]
    related_skills: [plan]
---

# Research

A lightweight research workflow for ordinary investigations.

The objective is not to maximize search depth or source count. The objective is to make a decision-safe answer: establish the current state, cover the important dimensions, test the leading explanation, expose material uncertainty, and recommend one practical next step.

## Use this skill when

Use when the user asks to investigate, research, verify, compare, understand the current state of something, reconstruct why it works this way, diagnose whether behavior is intended or broken, or recommend a solution after checking evidence.

Do not use for:
- a fact answerable reliably with one authoritative lookup
- exhaustive academic literature review
- large market reports or full due diligence
- recurring monitoring
- implementation-only work where the facts and plan are already established

Research is read-only unless the user separately asks for execution.

## Research contract

1. Do not decide the answer first and search only for support.
2. Establish the current date/version/state before using older evidence.
3. Prefer primary sources, but use independent secondary/community sources where they add real-world behavior, criticism, or counter-evidence.
4. Read important sources in full; do not reason from search snippets alone.
5. Separate documented fact, corroborated fact, inference, and unknown.
6. Actively look for evidence that would weaken the leading explanation.
7. Treat multiple articles repeating the same underlying source as one evidence cluster, not independent confirmation.
8. Stop when remaining uncertainty would not change the recommendation.
9. Recommend one path by default; mention alternatives only when they represent a meaningful fallback or different tradeoff.

## Step 1 — Scope and coverage frame

Translate the user's request into a compact internal research frame before searching.

Define:

- **Decision/question:** What must be resolved?
- **Current state:** What is true now?
- **Mechanism/history:** Why is it this way, or how did it change?
- **Uncertainty:** What is disputed, missing, or easy to misread?
- **Constraint:** What must a practical recommendation respect?

Then create **2–6 investigation dimensions**. Dimensions are not fixed; derive them from the topic.

For technical/product investigations, common dimensions include:
- official documented behavior
- current implementation/source
- version/release history
- issues/PRs/commits/maintainer intent
- platform/config/environment differences
- user-visible behavior and reproducible reports
- alternatives/workarounds and their constraints

For comparisons, define the comparison fields before collecting facts so all candidates are judged on the same dimensions.

Do not show this frame unless the user asks for the plan or the scope is genuinely ambiguous.

### Coverage rule

Before searching, ask internally:

> If I answer only the obvious part of this question, what important dimension could make the conclusion wrong?

Add that dimension to the frame.

## Step 2 — Ground time, version, and terminology

For anything that can change:

- establish the actual current date
- identify the relevant product/software/model/version/branch/platform
- distinguish publication date from the date a change actually happened
- resolve ambiguous names and renamed features
- check whether apparently conflicting sources describe different versions, editions, environments, or feature flags

Never mix historical behavior with current behavior without saying so.

## Step 3 — Source strategy

Use a source hierarchy, but choose sources by evidentiary value rather than prestige alone.

### Tier A — Primary evidence
Official docs, source code, specifications, release notes, changelogs, original papers, model cards, official policy/pricing/status pages, issues/PRs/commits and maintainer comments.

### Tier B — Independent strong evidence
Reputable technical reporting, independent tests, well-documented benchmarks, expert analysis with transparent methodology.

### Tier C — Community / anecdotal evidence
Forums, Reddit, Discord excerpts, blog posts, social posts, user reports.

Use Tier C for symptoms, edge cases, terminology, counterexamples, and real-world friction. Do not use repeated anecdotes as proof of intended design.

For software/product investigations, prefer triangulation such as:

**docs → implementation → change history → issues/PRs → observed behavior**

Do not assume documentation proves implementation, or that implementation alone proves product intent.

## Step 4 — Adaptive research loop

Research in rounds. A round is:

**Map gaps → Search → Open/extract → Compare → Update evidence → Check stop**

### Quick
1 round. Narrow question, clear source trail.

### Normal
Up to 2 rounds. Default for ordinary research.

### Extended
Up to 3 rounds. Only when a material contradiction, missing dependency, causal question, or version mismatch could change the conclusion.

These are ceilings, not targets.

### Round 1 — Map the territory

Start broad enough to identify the important dimensions and strongest sources, then move quickly to primary evidence.

Use focused queries. When one source points to a relevant issue, PR, spec, paper, commit, or release note, follow that reference.

Read the most important pages in full.

Do not fetch every search result.

### Round 2 — Fill gaps and challenge the leading explanation

Target only what Round 1 did not establish.

Include at least one **disconfirmation search** aimed at finding:
- an official statement that the behavior is intentional
- code contradicting the docs
- a release that changed the behavior
- a rejected fix with a documented reason
- a different platform/version where the behavior differs
- evidence that the apparent cause is only correlation

If no counter-evidence appears, do not interpret that alone as proof.

### Round 3 — Resolve decision-changing uncertainty only

Use only if the unresolved point can materially change the recommendation.

If a gap is interesting but decision-irrelevant, stop and report it.

### Empty-search rule

If a search produces nothing useful:
1. change wording/synonyms or broaden slightly
2. change angle, source type, domain, language, or terminology
3. after repeated failure, record the item as unknown and move on

Do not burn rounds repeatedly searching the same dead end.

## Step 5 — Evidence discipline

Maintain a lightweight internal evidence ledger for material claims.

A material claim is one that affects the answer, diagnosis, or recommendation.

Classify each material claim as:

- **Verified** — corroborated by at least two genuinely independent credible evidence clusters
- **Sourced** — directly supported by one credible source
- **Inferred** — analytical conclusion drawn from evidence but not explicitly stated by a source
- **Unknown** — not established

Independence matters. Three news articles quoting the same vendor announcement are one evidence cluster.

Also track source strength:
- primary
- strong secondary
- community/anecdotal

Do not mechanically require two sources for facts where one authoritative primary source is the source of truth (for example, an official API price or current documented setting). In that case mark it as Sourced and treat its authority appropriately.

When sources conflict:
1. check date/version/platform mismatch
2. prefer direct evidence over summaries
3. prefer current evidence for current-state claims
4. distinguish intended behavior from observed behavior
5. present unresolved conflict instead of silently choosing a side

Never invent a missing link in the causal chain.

## Step 6 — Reconstruct the logic

The result must explain how the evidence fits together, not merely list sources.

For technical/product investigations, distinguish when relevant:

- intended design
- documented behavior
- actual implementation
- historical behavior
- regression/bug
- configuration/environment issue
- documentation drift
- UI/UX ambiguity
- deliberate limitation/tradeoff

Use this causal pattern where possible:

**Observed behavior → verified mechanism → historical/contextual reason → practical consequence**

If the reason is not documented, state that it is an inference and explain what evidence makes it plausible.

## Step 7 — Test the recommendation

Before finalizing, evaluate the proposed action against:

- the user's actual objective
- current technical/product constraints
- version/platform compatibility
- operational complexity
- likely failure modes
- reversibility
- whether it fixes the cause or only the symptom

Prefer the smallest intervention that solves the real problem.

If several options exist, rank them internally and give one default recommendation. Surface a fallback only when the default has a meaningful blocker.

## Stop conditions

Stop when:

- the current state is established
- all decision-relevant dimensions are answered or explicitly unknown
- the leading explanation has been tested against plausible counter-evidence
- important sources have been read in full
- new searches mostly repeat existing evidence
- remaining uncertainty would not change the recommendation

Do not keep researching just to increase source count.

## Tool behavior

Use Hermes-native `web_search` and `web_extract` by default.

For repository questions, inspect source files, git history, issues, PRs, commits, and releases where available.

Use local terminal/file tools only in read-only ways during research.

Do not invoke paid external research services merely because they are installed.

Do not use `delegate_task` by default. Escalate to parallel subagents only when the problem splits into genuinely independent branches whose combined value justifies the cost. If subagents are used:
- give each a distinct research dimension
- require source URLs/evidence
- verify important citations yourself
- keep final synthesis with the main agent

## Final answer

Prefer a compact decision-oriented answer.

### Conclusion
Answer the actual question immediately.

### What is established
Only the facts that materially support the conclusion, with citations.

### How it fits together
Explain the relevant mechanism, timeline, dependency, or contradiction. Make inference visibly different from documented fact.

### Recommended action
Give one practical next step and the key prerequisite/risk.

### Remaining uncertainty
Include only if something unresolved could matter.

For simple investigations, merge these sections naturally. Do not force a report template.

Avoid:
- visible research plans unless asked
- long source-by-source summaries
- research statistics
- arbitrary source-count or word-count minimums
- excessive evidence labels in user-facing prose
- equal-weight option dumps

## Final verification

Before answering, silently check:

- Did I cover the important dimensions, not just the obvious one?
- Did I establish the current date/version/state?
- Did I inspect the strongest available primary evidence?
- Did I read important sources beyond snippets?
- Did I check implementation/history when the question depends on them?
- Did I actively search for counter-evidence?
- Are my corroborating sources genuinely independent?
- Did I separate fact from inference?
- Did I resolve or expose material contradictions?
- Would any remaining gap change my recommendation?
- Is the recommended action actually feasible under the user's constraints?

If a material answer is "no", perform one targeted follow-up search or state the limitation.
