# Pipeline Files

A data dictionary for the pipeline. Each step reads the previous step's file and writes its own (ADR-025). Shapes below are the plan and may be refined when the code is written.

## Generated files (not tracked by Git)

**`data/work/lines.jsonl`** (step 1). One record per text line of the PDF: `page`, `y` (height; the left-to-right position is added for step 6), `text`, `font`, `size`, `bold`, `rotated`.

**`data/work/page_register.csv`** (step 2). One row per page, a side sheet of flags: `page`, `line_count`, `has_loc_table`, `rotated_share`, `images`, `flags` (for example `sideways` or `blank`). Used by later steps for routing. It is not a step in the main chain of files.

**`data/work/conditions.jsonl`** (step 3). One record per condition: `condition_id`, `number`, `title`, `icd10_raw`, `parent`, `pdf_pages`, `lines` (the condition's line records). Introduction and appendix material have records of their own, marked by type.

**`data/work/conditions_clean.jsonl`** (step 4). The same shape as `conditions.jsonl`, with clean lines: sideways headers and footers removed, split words rejoined, bullets fixed, dropped pages gone.

**`data/work/glossary.jsonl`** (step 4). One record per abbreviation from the UCG list: `abbreviation`, `full_form`.

**`data/work/chunks_prose.jsonl`** (step 5). Chunks of type `text`.

**`data/work/chunks_treatment_lines.jsonl`** (step 6). Chunks of type `drug_line` and `table` from Management tables with an LOC column.

**`data/work/chunks_table_rows.jsonl`** (step 7). Chunks of type `table_row` and `table` from simple grid tables.

**`data/work/chunks_pointers.jsonl`** (step 8). Chunks of type `pointer` for hard tables.

**`data/work/chunks_linked.jsonl`** (step 9). All four chunk files merged, with `order_in_condition` and `applies_to` filled in, and parent IDs checked.

**`data/final/chunks_all.jsonl`** (step 10). The chunks that passed the checks. This is the file the next stage reads. Every chunk has the shape in [chunk-metadata.md](chunk-metadata.md).

**`db/lookups.sqlite`** (step 11). Tables of exact facts: the condition list, the glossary, the lab menu, and later the EMHSLU.

## Review reports (generated, in `data/reports/`)

- `condition_review.csv` (step 3): flagged conditions.
- `removed_report.csv` (step 4): what cleaning removed.
- `hard_table_candidates.csv` (step 8): candidate hard tables for people to review.
- `check_report.csv` (step 10): chunks that failed a check, with the reason.

## Hand-made files (tracked by Git)

- `config/settings.yaml`, `drop_pages.yaml`, `section_labels.yaml`, `corrections.yaml`.
- `curated/registry.csv`: `id`, `pdf_page_start`, `pdf_page_end`, `printed_page_start`, `condition_id`, `table_type`, `caption`, `status`, `prepared_by`, `verified_by`, `verified_date`, `notes`.
- `curated/tables/`: one file per prepared table, named by its `curated_id`.
