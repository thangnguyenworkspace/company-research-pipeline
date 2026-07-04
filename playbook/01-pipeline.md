# The Pipeline

Two layers. A **macro arc** that takes you from "I want to understand this company" to a complete, integrated picture, and a **micro pipeline** that every individual topic dossier runs through. The macro arc is a sequence of the micro pipeline plus a recon phase in front and an integration phase behind.

## 1. The macro arc

### Phase 0: Scope

Before any search, write down in a few sentences:

- **Why** you are researching this company (a job decision, an investment, a partnership, a sales pursuit). The purpose changes what "done" looks like and which topics deserve the deepest cut.
- **What decision** the research feeds, and by when.
- **Your prior**: what you currently believe about the company, stated plainly. You will test this, not protect it. Writing it down before you start is the cheapest defense against motivated reasoning.

### Phase 1: Recon

One session. Goal: map the surface, not answer questions.

1. Run broad Exa searches across the company's name, products, founders, funding, and press. Use `web_search_advanced_exa` with natural-language queries (see [`playbook/04-tools.md`](04-tools.md)).
2. Crawl the obvious primary surfaces: the company site, the docs site, the blog, the careers page, Crunchbase or equivalent, the GitHub org if one exists.
3. Watch for **name collisions** early. Many company names are shared by unrelated entities (other companies, places, open-source projects). Record the collisions in the coverage map so every later search can exclude them.
4. Produce two artifacts in the company's working folder:
   - `00-recon.md`: what the company appears to be, its products, people, funding, and the obvious open questions. Everything here is provisional and labeled as such.
   - `00-coverage-map.md`: the living ledger of what is solid, what needs verification, and what is missing, organized by topic (template in [`templates/coverage-map.md`](../templates/coverage-map.md)).

Recon findings are a starting baseline, never the truth. The whole point of the later phases is that the first pass is always partly wrong.

### Phase 2: Topic dossiers

The core of the engagement. Seven topics, built **one per session**, in a deliberate order (see [`playbook/03-topics.md`](03-topics.md) for the topics and the rationale):

thesis, then company, then product, then buyers, then competitive, then activity, then people.

Each topic runs the eight-step micro pipeline below and produces one dossier file. Later dossiers load the earlier ones in full, so facts established once are cross-referenced, never re-derived.

### Phase 3: Integration

After the seventh dossier:

1. Drain every dossier's inbound queue (see step 8 below) so all cross-topic findings are absorbed.
2. Reconcile: re-read each dossier's "Open Questions" section; close what later dossiers answered.
3. Write the synthesis your Phase 0 scope asked for: the answer to the actual decision, drawing on all seven dossiers, with the load-bearing tensions each dossier handed forward stated honestly.

## 2. The micro pipeline (eight steps per topic)

Every dossier is built the same way. The steps that require judgment (4, 6, 7) you do yourself in the main conversation; the steps that are parallelizable legwork (2, 3, 5) go to sub-agents.

### Step 1: Load

Read, in full: the coverage map, every previously written dossier, and this topic's inbound queue (`inbound-queue/pending/`, findings other topics routed here). This is the highest-leverage quality step in the pipeline. Skipping it produces dossiers that contradict each other.

One hard rule for sub-agents: **files must be read past truncation**. File-reading tools truncate long files silently; an agent that reports on the first 2,000 lines of a 5,000-line file produces findings that look complete and are not. Spawn prompts must state this explicitly.

### Step 2: Gather

Fan out 2 to 4 parallel research agents, each owning a disjoint slice of the topic's sub-questions. Each agent runs a bounded **reason-search-reflect loop** (up to 3 rounds):

- **Reason**: name the biggest open gap in your slice.
- **Search**: at most 2 Exa searches plus 1 batched crawl aimed at that gap.
- **Reflect**: record what closed, grade every source on the two-axis system ([`playbook/02-epistemics.md`](02-epistemics.md)), and test the stop rule.

Stop when you can no longer name a specific unexplored source or angle (a named-gap test, not a quality floor: thin topics stop honestly at a low grade), when returns are diminishing, or at the 3-round cap. Round 1 is the classic one-shot search; the depth comes from rounds 2 and 3 aimed only at residual gaps.

Gather agents **organize, never conclude**. Their output is sourced findings with grades (template in [`templates/gather-report.md`](../templates/gather-report.md)), not analysis. Every finding carries its external source URL.

### Step 3: Compile

One agent (or you, for small topics) merges the gather reports: dedupe, structure by the dossier's planned sections, preserve every citation. Then update the coverage map: what is now solid, what needs verification, what is still missing.

### Step 4: Verify

The step that separates this pipeline from a summary. Frame it adversarially: the verifier's job is to **refute** claims, not confirm them.

Triage what gets re-checked against primary sources: claims that are load-bearing AND (single-source, old, of unknown origin, or time-sensitive). For each, fan out verification agents that go to the primary record: the regulator's own register, the package registry's JSON API, the live product docs, the official appointment roster, the company's own filings.

Output per claim: a verdict (CONFIRMED / REFUTED / PARTIAL), the confidence, and the primary source (template in [`templates/verification-report.md`](../templates/verification-report.md)). Two patterns worth stealing:

- **Verify against the running system.** A moat claim is not tested against the company's whitepaper; it is tested against what rivals actually ship today. A "we integrate with X" claim is tested by finding the integration in the live docs.
- **Positive controls.** When verifying an absence ("the company is on no standards roster"), also confirm the method can find presence: check that known members DO appear in the roster you are reading. An absence finding without a positive control is a search failure waiting to be published.

### Step 5: Critical attack

You, in the main conversation, never delegated. Attack the assembled argument the way a hostile reviewer would:

- Which load-bearing claims still rest on weak or single sources?
- Which surfaces has nobody looked at?
- Where do two findings quietly contradict each other?
- What would embarrass you if the subject of the research read this dossier?

The attack's output is a target list for step 6. Often the attack surfaces framing problems rather than coverage gaps, in which case step 6 is skipped and you fix the framing at write time.

### Step 6: Supplement

Only the gaps the attack named. Small, targeted agent runs. Resist the urge to broaden; the coverage map already says what is missing, and missing-but-not-load-bearing waits.

### Step 7: Write

You write the dossier once, in the main conversation, from the compiled gather, the verification verdicts, and the inbound queue. Rules:

- Every claim carries an in-text citation and an `[F/I/A + NN%]` tag (the tag system is defined in [`playbook/02-epistemics.md`](02-epistemics.md)). Tags are assigned by you at write time, never inherited from an agent.
- Conflicts are surfaced with both numbers and both sources.
- The dossier follows the template ([`templates/dossier.md`](../templates/dossier.md)): an ownership header saying what this dossier owns and what its neighbors own, the tag legend, purpose-led sections, open questions, key terms, and a full reference list.
- Sections are scaffolding, not conclusions: the section plan fixes the questions each section answers, never the answers.

### Step 8: Distribute

The step everyone skips and should not. After writing, walk **all seven topics by name** and ask, for each: "what did I find that this other topic owns?" The ownership boundaries that keep dossiers clean also hide cross-findings from a lazy self-scan, which is why the walk must be deliberate and name every topic.

Each net-new finding becomes one small file in the destination topic's `inbound-queue/pending/` folder: a headline, one or two sentences, the citation, and a topical home hint. Apply the drop test: if the destination topic's own gather would obviously find this anyway, do not route it.

Unwritten topics absorb their queue at their own step 1. Already-written dossiers get their queue drained at the end of the session that produced the finding: absorb surgically into the owning section, merge the reference list, assign the tag, move the queue file from `pending/` to `archive/`.

## 3. Session pacing

One topic per session is the tested cadence. A dossier written at the tail of a long context window degrades measurably: tags get sloppier, conflicts get resolved instead of surfaced, and the distribute step gets skipped. If a session runs long, stop after step 5 and finish the write fresh.
