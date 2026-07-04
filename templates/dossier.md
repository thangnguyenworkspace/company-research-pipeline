# Dossier Template

Copy this skeleton for every dossier. Replace the `{placeholders}`; keep the block structure and the tag legend byte-identical across all seven dossiers so readers learn it once.

---

```markdown
---
type: Dossier
subject: {topic}
company: {company-slug}
created: {YYYY-MM-DD}
updated: {YYYY-MM-DD}
version: 1.0
status: draft | final
primary_source: {the single most load-bearing source URL}
description: '{2-4 sentences: what this dossier owns and its headline findings, each stated with its confidence}'
---

# Dossier, {Topic}

## Owns (single source of truth)

{What facts this file is the home for, in one paragraph.}

**Does NOT own:** {each adjacent slice, with a pointer to its owning dossier, e.g. "company facts and funding (dossier-company); what ships versus what is marketed (dossier-product); ..."}

## How to read the tags

Every load-bearing claim carries `[X/NN%]`: **F** = fact (checked against a primary source), **I** = inference (our reasoning from evidence), **A** = assumption (unproven, but must hold for the read to stand). NN% is our confidence. Tags are our assessment at write time, not the source's framing. Conflicts are surfaced inline, never silently resolved. Every fact carries an in-text citation that resolves to the Reference List.

---

## 1. {Section title}

> Purpose: {the question this section answers}.

{Body: cited, tagged prose. Use tables for comparisons, mermaid for flows (use <br/> for line breaks inside mermaid nodes). Surface conflicts inline: "CONFLICT surfaced: source A says X ([cite]) while source B says Y ([cite]); carried, not resolved."}

### 1.1 {Sub-section}

{...}

## 2. {Section title}

> Purpose: {...}

{...}

---

## Open Questions / Decisions Pending

- {Conflicts carried, not resolved: name both values and both sources.}
- {Genuinely unknowable from outside: questions to ask directly if access ever exists, not gaps to fill by more searching.}
- {The load-bearing tension this dossier hands the final synthesis.}
- {Net-new findings routed to other topics' inbound queues this session, listed by destination.}

## Key Terms

| Term | Plain meaning |
|---|---|
| {term} | {one-line plain-language definition} |

## Reference List

{Alphabetical. One entry per cited source. Format: Author/Org Year, *Title*, Publisher/Site, date, viewed {date}, <URL>.}
```

---

## Conventions

- **Sections are scaffolding, not conclusions.** Fix each section's purpose and dimensions before research; never pre-write the finding.
- **The description field carries the headline findings** with confidence levels, so a reader triaging seven dossiers can rank them without opening each.
- **Purpose lines** (`> Purpose: ...`) keep every section answerable: if you cannot state the question, the section should not exist.
- **One analytical spine per dossier** (see [`playbook/03-topics.md`](../playbook/03-topics.md)): a named lens (moat analysis, jobs-to-be-done, forecast horizons) that earns its place by producing insight the plain sections would miss.
