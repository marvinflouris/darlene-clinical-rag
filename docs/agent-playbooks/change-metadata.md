# Playbook: change the chunk metadata

Chunks have `chunk_id`, `text` and 17 metadata fields (see `docs/schemas/chunk-metadata.md`). ADR-026 (dropping `population`) is a good model of a complete change.

## Rules

- The owner must approve any change to the fields.
- A change needs an ADR first. Follow `adr.md`.
- Do the whole change in one commit.

## Update together

1. `docs/schemas/chunk-metadata.md`: the opening count, the field list and groups, and the example record.
2. `docs/00-start-here.md`: the field count.
3. `docs/02-architecture.md`: the field count.
4. `docs/glossary.md`: any entry for the field.
5. `docs/status.md`: the field count and the ADR line.
6. `docs/schemas/pipeline-files.md` and `docs/design/data-and-chunking.md`, if a file shape or a chunk type is affected.
7. `AGENTS.md`: the field count in the design rules.
8. `src/darlene/schema.py`, once it exists.

## Check before committing

- Search `docs/`, `AGENTS.md` and `README.md` for the old count and the old field name. Fix every hit, except text inside old ADRs and the new ADR.
- The example JSON in `docs/schemas/chunk-metadata.md` must be valid JSON, with the right number of metadata keys besides `chunk_id` and `text`.
- Every link in `docs/adrs/README.md` points to a file that exists.
