# research/

Working folders land here, one per company, created by [`/research-company`](../.claude/commands/research-company.md). Nothing in this folder ships with the repository; it is the write surface for your own engagements, and everything the pipeline produces (recon notes, gather reports, verification batches, the seven dossiers, the synthesis) stays inside the company's folder. The layout each engagement gets:

```
research/{company-slug}/
├── 00-scope.md                 why this company, what decision, your stated prior
├── 00-recon.md                 the provisional first pass (never the truth)
├── 00-coverage-map.md          the living solid / needs-verify / missing ledger
├── 00-progress.md              one line per session; the backflow log table
├── dossier-thesis.md           the seven dossiers, written one per session
├── dossier-company.md
├── dossier-product.md
├── dossier-buyers.md
├── dossier-competitive.md
├── dossier-activity.md
├── dossier-people.md
├── synthesis.md                the final answer to the scope question
└── {topic}/                    per-topic working evidence
    ├── 01-gather/              gather agents' reports + the compiled merge
    ├── 02-verification/        adversarial verification batches
    └── inbound-queue/
        ├── pending/            findings routed here by other topics, awaiting absorption
        └── archive/            absorbed findings (the move is the audit trail)
```

Two rules govern this folder. Raw evidence files are immutable once written: when a claim turns out to be wrong, the correction lands in a dossier or a verification report, never by editing the evidence file, so the trail of what was actually retrieved stays intact. And if a company's research is sensitive, add `research/{company-slug}/` to [`.gitignore`](../.gitignore) before committing; the pipeline works identically whether the engagement is committed or kept local.
