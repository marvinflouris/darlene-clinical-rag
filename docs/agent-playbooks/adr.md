# Playbook: add or replace an ADR

An ADR (Architecture Decision Record) records one decision, the options rejected, and why. Old ADRs are never rewritten.

## When an ADR is needed

Any decision that changes the design: choosing between options, adding or removing a metadata field, changing what a pipeline step reads or writes, choosing a dependency or a model. Open questions are not ADRs. They go in `docs/status.md`.

## Steps

1. Ask the owner to confirm the decision itself. The owner decides. You draft.
2. Open `docs/adrs/README.md` and find the highest ADR number. Use the next one.
3. Copy `docs/adrs/ADR-000-template.md` to `docs/adrs/ADR-NNN-short-title.md`.
4. Fill in every field: Date (today), Status, Context, Options considered, Decision, Why, Consequences. Keep it short and factual. Use facts from the project, and do not invent numbers or reasons.
5. Set the status to `proposed` until the owner says it is accepted. Never set `accepted` yourself.
6. Add a line to the Index in `docs/adrs/README.md`.
7. If the new ADR replaces an older one: edit only the older ADR's status line (for example `partly replaced by ADR-NNN` or `replaced by ADR-NNN`), update that line in the index, and change nothing else in the old ADR.
8. Update the documents the decision affects. If it changes the metadata, follow `change-metadata.md`.
9. Commit using `commit-and-handoff.md`.
