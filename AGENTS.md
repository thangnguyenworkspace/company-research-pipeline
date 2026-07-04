# AGENTS.md

Entry point for an agent operating or ingesting this repository. This is the single canonical agent-instruction file; [CLAUDE.md](CLAUDE.md) imports it, so the two cannot drift. Edit this file, never CLAUDE.md.

## What this is

`company-research-pipeline` is a company-research method packaged for Claude Code: four playbook documents, five slash-command skills, and four output templates that take one company from a scoped question to seven cited, confidence-tagged dossiers plus a synthesis. It is a stable snapshot distilled from one real diligence engagement. There is nothing to build or test; the repository is prose and skills, and the only thing that runs is a research engagement inside Claude Code.

## How to navigate

| Path | Role |
|---|---|
| `.claude/commands/research-company.md` | The orchestrator: start here; it owns scoping, recon, and the seven-topic walk. |
| `.claude/commands/research-topic.md` | One dossier through the eight-step loop (load, gather, compile, verify, attack, supplement, write, distribute). |
| `.claude/commands/exa-crawl.md`, `social-crawl.md`, `repo-recon.md` | The three retrieval motions: Exa crawling, Apify social pulls, GitHub reconnaissance. |
| `playbook/01-pipeline.md` | The macro arc and the eight-step micro pipeline; the method's spine. |
| `playbook/02-epistemics.md` | The `[F/I/A + NN%]` tag system, two-axis source grading, and the honesty rules. |
| `playbook/03-topics.md` | The seven dossier subjects, their ownership boundaries, and the build order. |
| `playbook/04-tools.md` | Verified Exa and Apify parameters, cost traps, and silent failures. Read before any tool call. |
| `templates/` | The exact output shapes for dossiers, gather reports, verification reports, and the coverage map. |
| `research/` | Working folders, one per company; the only surface an engagement writes to. |

## Run it

Requires the Exa MCP server (bulk of the research) and optionally the Apify MCP server (LinkedIn and X). Open the repository in Claude Code and invoke `/research-company <name>`; the skill scaffolds `research/<slug>/` and drives the pipeline from there, one topic dossier per session. Any motion also runs standalone (`/exa-crawl`, `/social-crawl`, `/repo-recon`, `/research-topic`).

## Conventions

- Engagement output lands only under `research/{slug}/`; nothing else in the repository is written during a run.
- No fact without a citation that resolves to an openable URL. Untraceable claims are labeled unverified.
- Final `[F/I/A + NN%]` tags are assigned by the human at write time; agents report evidence and grades, never final tags.
- Every Apify run passes the budget-estimate gate in `/social-crawl` before launching; the actors' own `maxPosts`/`maxItems` are the only functional spend caps.
- Read source files past truncation: file-reading tools cut long files silently, and a half-read file produces findings that look complete and are not.
- Raw evidence files are immutable once written; corrections happen in dossiers and verification reports.

## Status & provenance

Stable snapshot, built with Claude Code; issues and PRs are not actively watched. The method was extracted from a private engagement (seven verified dossiers, 300+ sources); the engagement's findings are not in this repository, only the method. The five commands are plain Claude Code slash commands, deliberately not packaged as versioned skills with evals.
