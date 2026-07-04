# Gather Report Template

One file per gather agent, written to `research/{company}/{topic}/01-gather/gather-{slice}.md`. Gather agents **organize, never conclude**: no tags, no verdicts, no synthesis. Findings plus sources plus grades.

---

```markdown
---
type: Gather Report
topic: {topic}
slice: {slice-name}
company: {company-slug}
date: {YYYY-MM-DD}
rounds_run: {1-3}
stop_reason: named-gap-exhausted | diminishing-returns | round-cap
---

# Gather: {slice name}

## Scope

Covered: {the sub-questions this slice owns}
Excluded: {the sub-questions explicitly left to sibling slices}

## Findings

### {Sub-question 1}

- {Finding, stated as what the source says, not as a conclusion.} [R2·C1] ({Source Name}, {date}, <URL>)
- {Finding.} [R3·C3, sole source for this figure] ({Source}, <URL>)
- CONFLICT: {source A} says {X} (<URL>) while {source B} says {Y} (<URL>). Recorded, not resolved.

### {Sub-question 2}

- {...}

## Reflection trace

- Round 1: searched {queries}; closed {what}; remaining gap: {what}.
- Round 2: aimed at {gap}; closed {what}; remaining: {what}.
- Round 3 / stop: {why the loop stopped, per the stop rule}.

## Gaps and not-found

- {What was sought and not found. Plain statement of the search, so a later positive-control check is possible.}

## Sources consulted

{Every URL touched, with its [R·C] grade, including the ones that produced nothing.}
```

---

## Rules

- Grade every source `[R·C]` per [`playbook/02-epistemics.md`](../playbook/02-epistemics.md) section 3. Sole-source figures cap at C3.
- Natural-language Exa queries; parameters per [`playbook/04-tools.md`](../playbook/04-tools.md) (crawl `maxCharacters` set, `numResults` explicit, pre-score from result text before crawling).
- Every finding carries an external source URL. "I recall" and "it is known" do not exist.
- Not-found is reported as a search fact, never as evidence of absence.
