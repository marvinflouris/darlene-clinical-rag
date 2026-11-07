# Architecture Decision Records (ADRs)

One short file per decision, named ADR-NNN-short-title.md, using ADR-000-template.md.

Rules:
- Old ADRs are never edited. If we change our mind, we write a new ADR that says it replaces the old one, and mark the old one as replaced.
- Open questions do not become ADRs. They stay in docs/status.md until they are decided.
- Status 'accepted' means decided. Status 'proposed' means agreed in principle, to be finalised in a later stage.

## Index

- [ADR-001](ADR-001-design-for-the-whole-book.md): Design for the whole book, with no first slice (accepted)
- [ADR-002](ADR-002-ucg-only-source-emhslu-lookup.md): The UCG is the only source of chunks; the EMHSLU is a separate lookup (accepted)
- [ADR-003](ADR-003-text-only-llm-vision-offline.md): The main LLM is text-only; vision models are used only offline (accepted)
- [ADR-004](ADR-004-no-llm-in-parsing.md): No LLM in the parsing pipeline; rules only (accepted)
- [ADR-005](ADR-005-scope-check-not-covered.md): Answers stay within what the UCG covers; "not covered" is a valid answer (accepted)
- [ADR-006](ADR-006-chunk-by-labelled-parts.md): Chunk by the book's labelled parts, not by fixed size (accepted)
- [ADR-007](ADR-007-parent-child-chunks-for-tables.md): Parent-child chunks: drug lines and table rows are small chunks, the whole table is the parent (accepted)
- [ADR-008](ADR-008-uniform-table-row-format.md): One uniform record format for table rows (accepted)
- [ADR-009](ADR-009-condition-record-unit-of-work.md): The condition record is the unit of work from step 3 onward (accepted)
- [ADR-010](ADR-010-own-condition-id.md): Our own condition_id, not the book's number and not ICD-10 (accepted)
- [ADR-011](ADR-011-hard-tables-as-pointers.md): Hard tables are pulled out and left as pointer chunks (accepted)
- [ADR-012](ADR-012-eighteen-metadata-fields.md): The 18 metadata fields in four groups (accepted)
- [ADR-013](ADR-013-fields-dropped.md): Fields dropped from the chunk metadata, with reasons (accepted)
- [ADR-014](ADR-014-applies-to-field.md): applies_to for blocks that serve several conditions (accepted)
- [ADR-015](ADR-015-header-from-metadata.md): The chunk header is built from metadata, not written by an LLM (accepted)
- [ADR-016](ADR-016-icd10-as-list.md): ICD-10 stored as a list, inherited from the parent entry when missing (accepted)
- [ADR-017](ADR-017-condition-first-retrieval.md): Condition-first retrieval (proposed)
- [ADR-018](ADR-018-drug-facts-from-emhslu-after-answer.md): Drug facts come from the EMHSLU table after the answer; no agent loop (accepted)
- [ADR-019](ADR-019-citations-built-by-code.md): Citations are built by code from metadata (proposed)
- [ADR-020](ADR-020-retrieval-improvements-order.md): Order of retrieval improvements: cheap fixes first, fine-tuning later (proposed)
- [ADR-021](ADR-021-duplicate-psychiatric-section.md): Keep both copies of the duplicated psychiatric section, flagged, until decided (accepted)
- [ADR-022](ADR-022-corrections-file-never-blocks.md): Book typos and numbering errors go in corrections.yaml; pending ones never block a run (accepted)
- [ADR-023](ADR-023-docs-as-code-adrs.md): Documentation as Markdown in the repository; one ADR file per decision (accepted)
- [ADR-024](ADR-024-file-types-by-role.md): File types are chosen by who writes and reads them (accepted)
- [ADR-025](ADR-025-eleven-step-pipeline.md): An 11-step pipeline: each script reads the previous file and writes its own (accepted)
