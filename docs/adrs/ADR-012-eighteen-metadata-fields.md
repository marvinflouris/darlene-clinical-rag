# ADR-012: The 18 metadata fields in four groups


- Date: 2026-11-07
- Status: partly replaced by ADR-026 (the population field was dropped; 17 fields remain)
- Context: We needed a metadata design in which every field is used by some step.
- Options considered: Many fields were proposed and tested against the pages and the 30 expert questions. A field stays only if a step uses it to find, connect, cite or check.
- Decision: Each chunk record holds chunk_id, text and 18 fields in four groups. Address: source, edition, chapter, section_path, printed_page, pdf_page. Identity: condition_id, condition_title, parent_condition_id, icd10, population, order_in_condition. Shape: section_type, chunk_type, table_verification_status. Connections: parent_chunk_id, applies_to, curated_id.
- Why: It matches the project owner's four-bucket mental model, and each field has a job.
- Consequences: All chunks share the same fields, but some values are empty (a Causes chunk has no parent_chunk_id). The full specification goes in docs/schemas/chunk-metadata.md. population is read from the condition heading; ages inside lines stay in the text.
