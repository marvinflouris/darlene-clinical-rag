# AGENTS.md: rules for coding agents working on Darlene

Read this file first, every session. It is short on purpose. Details are in the docs and playbooks it links to.

## What this project is

Darlene is a clinical-guideline RAG project for the Uganda Clinical Guidelines 2023 (UCG). It is in an early design stage: the documents come first and the pipeline code is mostly placeholders. Wrong clinical text can harm patients, so accuracy, traceability and honesty about what is not covered matter more than speed.

Start every session by reading:
1. `docs/status.md` (where we are and what is open)
2. `docs/agent-handoff.md` (what the last session did)
3. `docs/adrs/README.md` and the ADRs that touch your task
4. `docs/00-start-here.md` if you are new to the project

## Folder map and who owns what

- `docs/`: documentation. ADRs are append-only.
- `config/`: YAML settings and the owner's corrections. The owner decides the values.
- `curated/`: expert-checked tables and the hard-table registry. Controlled by people.
- `data/` and `db/`: generated, ignored by Git. `data/raw/` holds the source PDF.
- `evaluation/`: question sets from medical experts.
- `src/darlene/pipeline/` and `src/darlene/rag/`: the code.
- `tests/`: tests and golden pages.
- `pyproject.toml` and `uv.lock`: dependencies, managed with uv.

## Protected: stop and ask first

Do not change any of these unless the owner clearly says yes in the current session:

- Existing ADRs. The only allowed edit to an old ADR is its status line, when a newer ADR replaces it.
- Anything in `curated/`.
- Anything in `data/raw/`. Never modify or delete the source PDF.
- `.env`. Never read, print or commit it.
- The expert fields in `evaluation/questions/*.csv`: question text, expected verdict, evidence columns, reviewer, notes.
- `config/corrections.yaml`. These are the owner's decisions. You may suggest entries but do not add them unasked.
- `docs/schemas/chunk-metadata.md` and the chunk shape. A change needs an ADR first (see the playbook).
- `pyproject.toml` and `uv.lock`. Dependency changes need approval.
- `AGENTS.md` and `docs/agent-playbooks/`. You may suggest changes but do not make them unasked.

Never:
- Invent or "correct" clinical content (a dose, an LOC value, an ICD code, a page number) by your own judgement. Flag it to the owner instead.
- Mark an ADR as "accepted" yourself. Draft it as "proposed" until the owner agrees.
- Run `git push`, force-push, rewrite history or use `--no-verify`.
- Commit on `main`.

## The stop-and-ask rule

If a task needs a protected file, if two documents disagree, or if you are not sure: stop, then tell the owner which file, what change and why. Wait for an explicit yes. After approval, make the change, add a line to `docs/agent-exceptions.md`, and mention it in the commit message. If you changed something protected by mistake, say so at once, revert it, and tell the owner.

## How every task goes

1. Read the files listed above.
2. Write a short plan in plain words and wait for the owner's approval before changing files. For a tiny document fix, state the change first.
3. Work on a branch named `agent/<short-task>`, never on `main`.
4. Make the smallest change that does the job. Do not touch unrelated files or reformat.
5. Update every document the change affects. Use the playbook for the type of change. A design decision needs an ADR.
6. Once code exists, run the tests with `uv run pytest`.
7. Commit using `docs/agent-playbooks/commit-and-handoff.md`, then update `docs/agent-handoff.md`, and `docs/status.md` if the state changed.
8. Report to the owner: what changed, which files, whether any protected file was touched, what you did not do, and any open questions.

## Code style

The owner is still learning Python. Write simple, readable code: plain syntax, simple comments, loops instead of nested comprehensions, small functions, clear names. Each pipeline step is one file that reads one file and writes one file (see `docs/schemas/pipeline-files.md`).

## Design rules that must not be broken

- No LLM calls and no network calls in the parsing pipeline (ADR-004).
- A chunk is `chunk_id`, `text` and 17 metadata fields. Adding or removing a field needs an ADR (ADR-012, ADR-013, ADR-026).
- One uniform record format for table rows (ADR-008). Hard tables become pointer chunks until prepared (ADR-011).
- Each pipeline step reads the previous step's file and writes its own. Steps do not edit earlier files (ADR-025).
- A dash that means "no dose" is never turned into 0.
- Unresolved problems go to a review report. Do not silently pick one version of a duplicate section (ADR-021).
- "Not covered" is a valid answer. Never guess (ADR-005).

## Secrets and data

Never commit `.env`, the UCG PDF, other source documents or any patient data.

## Playbooks

- `docs/agent-playbooks/adr.md`: add or replace a decision record
- `docs/agent-playbooks/change-metadata.md`: change the chunk metadata
- `docs/agent-playbooks/change-pipeline-step.md`: change a pipeline step
- `docs/agent-playbooks/hard-table-registry.md`: work with hard tables
- `docs/agent-playbooks/commit-and-handoff.md`: commit and hand off

If your tool looks for a different instruction filename, make that file a one-line pointer to this one.
