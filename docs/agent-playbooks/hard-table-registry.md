# Playbook: hard tables and the registry

Hard tables (sideways ARV tables, TB tables with grey "not applicable" cells, flowcharts, image pages) are not forced through the parser. Each gets a pointer chunk now. The real table is prepared separately, checked by experts, and stored in `curated/` (ADR-003, ADR-011).

## Who owns what

- `curated/registry.csv` and `curated/tables/` are controlled by people. Do not change them unless the owner asks you to.
- Pipeline step 8 only writes a list of candidates to `data/reports/hard_table_candidates.csv`. It never writes into `curated/`.
- You may add a registry row, with status `pending`, only when the owner asks.
- Never set a table's status to `verified` and never fill `verified_by` or `verified_date`. Only people verify.
- A table prepared with a vision model is a draft. Mark it `pending` until an expert has checked it.

## Rules for prepared tables

- Use the same record format as other tables: every value paired with its column header (ADR-008).
- Write out what the picture shows: "not applicable", "no dose". Never leave a meaningful dash or grey cell as an empty value, and never turn it into 0.
- Keep the printed page and PDF page of the source.

## Pointer chunks

A pointer chunk holds a caption, the page numbers, and an empty `curated_id` until the table is ready. Until then Darlene says "this part has a table that is not loaded yet, see page N". Never fill the gap from the surrounding text.
