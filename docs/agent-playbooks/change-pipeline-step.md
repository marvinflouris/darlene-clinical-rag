# Playbook: change a pipeline step

The pipeline has 11 steps. Each reads the previous step's file and writes its own. The files and their shapes are in `docs/schemas/pipeline-files.md`. The design is in `docs/design/data-and-chunking.md` and ADR-025.

## Before writing code

1. Read the step's entry in `docs/schemas/pipeline-files.md` and the ADRs it cites.
2. Write a short plan in plain words: what the step reads, what it writes, how it decides things. Wait for the owner's approval.
3. If the plan changes a design decision, a file shape or a chunk field, it needs an ADR first (see `adr.md`).

## Rules for the code

- Rules only: no LLM calls and no network calls (ADR-004).
- Facts about the book (page offset, heading fonts, pages to drop, label variants) live in `config/*.yaml`, not in the code.
- A step reads its input file and writes its own output file. It never edits earlier files.
- The same input must always give the same output.
- A problem the code cannot resolve goes to a review report in `data/reports/`. Do not silently choose. Corrections come only from `config/corrections.yaml`.
- Never turn a dash that means "no dose" into 0.
- Keep the code plain and commented in simple language.

## Testing

- Use the golden pages listed in `tests/README.md`. Expected outputs are confirmed by the owner by eye, so do not invent them.
- Once the tests exist, run `uv run pytest`. Adding a test dependency needs the owner's approval.
- Show the owner a sample of the real output. For step 6 (matching LOC values to drug lines by position), prototype on about 10 pages and show the result before running on the whole book.

## After the change

Update `docs/schemas/pipeline-files.md` if a file or shape changed, update `docs/status.md`, then follow `commit-and-handoff.md`.
