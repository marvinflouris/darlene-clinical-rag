# Chunk Metadata Specification

Every chunk is one record holding `chunk_id`, `text` and 17 metadata fields in four groups. Every chunk has every field, but some values are empty. A field earns its place only if a pipeline or retrieval step uses it to find, connect, cite or check chunks (see ADR-012). Dropped fields and the reasons are in ADR-013.

## Record basics

- `chunk_id`: a unique ID that stays the same when the pipeline is re-run, for example `anaphylactic-shock--management--04`. The exact format is fixed when step 5 is written.
- `text`: the words of the chunk. For a drug line, the text starts with `When: ...` if the line sits under a sub-heading such as "In severely affected patients", and it ends with `LOC: HC3` where the book prints a level. A leading `-Or` marker is kept.

## Group 1: Address (where in the book)

- `source`: the document, for example `UCG`. Never empty.
- `edition`: the year of that version, for example `2023`. Never empty.
- `chapter`: chapter number and title as printed, for example `1 Emergencies and Trauma`.
- `section_path`: the trail of headings ending with the part's label, for example `1.1 Common Emergencies > 1.1.1 Anaphylactic Shock > Management`. Used for display and citations. Uses the book's numbers after corrections.
- `printed_page`: the page number printed on the page, for example `2`, or a range such as `2-3` if the chunk spans pages.
- `pdf_page`: the page's position in the PDF file, for example `68`, or a range.

## Group 2: Identity (what it is about)

- `condition_id`: our unique label for the condition, for example `anaphylactic-shock`. Empty for introduction and appendix chunks. The rule for keeping labels unique when two entries share a title is set when step 3 is written.
- `condition_title`: the condition's name as printed.
- `parent_condition_id`: the `condition_id` of the bigger entry this one sits under, for example `malaria` for Uncomplicated Malaria. Empty if none.
- `icd10`: a list of the ICD-10 code or codes printed on the heading, ranges kept as printed. A sub-entry with no code inherits the nearest parent's. Empty if none.

- `order_in_condition`: the chunk's position among all chunks of its condition, starting at 1. Filled in step 9.

Patient group (age, pregnancy) is not a chunk field. Where the book splits a condition by group, the group is in `condition_title`. Otherwise it is in the chunk text (age lines, table columns). See ADR-026.

## Group 3: Shape (what role the chunk plays)

- `section_type`: the labelled part the chunk comes from. One of: `definition`, `causes`, `clinical_features`, `differential_diagnosis`, `investigations`, `management`, `prevention`, `notes`, `complications`, `other`. Label variants (Cause/Causes) are mapped in `config/section_labels.yaml`, and the list may grow when step 5 is written.
- `chunk_type`: one of `text`, `drug_line`, `table_row`, `table` (a whole table, used as a parent) or `pointer` (a placeholder for a hard table).
- `table_verification_status`: only for chunks from prepared tables: `pending` or `verified`. Empty otherwise.

## Group 4: Connections (how chunks link)

- `parent_chunk_id`: the ID of the bigger chunk this one was cut from (a drug line points to its whole table). Empty for plain text sections. Set in steps 5 to 8, and checked in step 9.
- `applies_to`: a list of the `condition_id`s the chunk serves. Usually just its own. Filled in step 9.
- `curated_id`: on a pointer chunk, the key of the prepared table in `curated/`. Empty until the table is prepared.

## Example: one drug line

```json
{
  "chunk_id": "anaphylactic-shock--management--04",
  "text": "Adrenaline (epinephrine) injection 1 in 1000 (1 mg/ml) 0.5 mg (0.5 ml) IM immediately, into anterolateral thigh. Repeat every 5-10 minutes according to BP, pulse rate and respiratory function until better. Child <6 years: 150 micrograms (0.15 ml). Child 6-12 years: 300 micrograms (0.3 ml). LOC: HC2",
  "source": "UCG",
  "edition": "2023",
  "chapter": "1 Emergencies and Trauma",
  "section_path": "1.1 Common Emergencies > 1.1.1 Anaphylactic Shock > Management",
  "printed_page": 2,
  "pdf_page": 68,
  "condition_id": "anaphylactic-shock",
  "condition_title": "Anaphylactic Shock",
  "parent_condition_id": null,
  "icd10": ["T78.2"],
  "order_in_condition": 8,
  "section_type": "management",
  "chunk_type": "drug_line",
  "table_verification_status": null,
  "parent_chunk_id": "anaphylactic-shock--management--table",
  "applies_to": ["anaphylactic-shock"],
  "curated_id": null
}
```

## The header line

When chunks are embedded and when they are shown to the model, a header is assembled from the fields, for example `UCG 2023 · Anaphylactic Shock (T78.2) · Management · p.2`. It is not stored in `text` (ADR-015).
