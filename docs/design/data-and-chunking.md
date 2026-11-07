# Data and Chunking Design

How the Uganda Clinical Guidelines 2023 (UCG) becomes a checked data bank of chunks. The reasons for each choice are in the ADRs; this document says how it works.

## 1. Purpose

Turn the UCG PDF into chunks and lookup tables that a later retrieval stage can search. The pipeline uses rules only, with no LLM (ADR-004), and runs on the whole book (ADR-001).

## 2. The source

- 1,161 pages with a readable text layer. There are no bookmarks, so structure comes from fonts and layout.
- The front pages use Roman numerals. Printed page = PDF page minus 66.
- The book's own table of contents has mistakes (a repeated section 9.2 and several typos), so we do not build structure from it.
- About 65 pages are printed sideways (for example the antenatal care chart, PDF 760-763, and the ARV dosing tables, PDF 291-294). About 15 pages hold images.
- Conditions are headings with a number, a title and usually an ICD-10 code. In the first condition list, 291 of 477 entries have their own code.

## 3. How a condition is laid out

A condition has an optional definition, then labelled parts: Causes, Clinical features, Differential diagnosis, Investigations, Management, Prevention, and others such as Notes, Caution, Complications. Not every condition has every label. Chapter 15 (family planning) uses different labels, such as Indications and Advantages.

The Management part is usually a table with two columns, TREATMENT and LOC. LOC is the facility level printed beside each drug. One cell can hold several lines with different LOC values. Sub-headings inside the table ("In severely affected patients", "If urticaria/itching") say when a line applies. Child doses sit on indented lines under the adult dose, and "-Or" marks an alternative.

## 4. Problems found and how we handle them

- **Running headers and footers.** The chapter title is printed sideways in the margin and lands inside the text. Step 4 reads the chapter from it, then removes it.
- **Split words.** Words are broken across lines with an invisible soft hyphen ("vac" + "cines"). Step 4 rejoins them. For ordinary hyphens, a word is rejoined only if the joined form appears elsewhere in the book.
- **Odd bullet symbols.** Replaced with plain bullets.
- **Blank and filler pages.** Dropped by `drop_pages.yaml` (page 453 says "This is a blank page").
- **Repeated or wrong numbers.** Section numbers repeat, and one heading numbered 1.1.1 sits in chapter 12. We use our own `condition_id` (ADR-010) and record fixes in `corrections.yaml` (ADR-022).
- **A duplicated section.** Section 9.2 appears twice (PDF 572 and 590). Both copies are kept and flagged (ADR-021).
- **Stubs.** An entry such as 3.2.3 Pelvic Inflammatory Disease only says "See section 14.1.2". The condition list holds that link for the resolver.
- **Management outside the condition.** In malaria, one Management block follows both the uncomplicated and severe entries. Chunks carry `applies_to` (ADR-014).
- **Syndromic organisation.** Some infections are covered inside a syndrome heading (chancroid inside Genital Ulcer Disease). The resolver needs an alias list.
- **Odd LOC values.** Most are HC1 to HC4, H, RR and NR, with a few odd ones (for example HC2V). They go to a review report.

## 5. Chunk types

- **`text`.** One whole labelled part (all of "Clinical features"). A very long part is cut into pieces that point back to it (ADR-006).
- **`drug_line`.** One drug line from a Management table, with its child doses, its sub-heading as `When: ...`, and `LOC: ...` in the text (ADR-007, ADR-013).
- **`table_row`.** One row of a simple grid table, each value paired with its column header (ADR-008).
- **`table`.** A whole table, kept as the parent of its drug lines or rows.
- **`pointer`.** A placeholder for a hard table, with a caption and page numbers (ADR-011).

## 6. Tables

There is one record format for every table row (ADR-008). Four families are read by rules: Management tables with an LOC column, dosing by weight, policy tables (population to regimen), and Y/N matrices. A cell with a dash that means "no dose" is written out and never turned into 0. Table titles come from the nearest heading, because the book rarely uses captions.

Hard tables are not forced through the parser. ARV tables use dashes for empty cells and are sideways. TB tables use dark grey cells for "not applicable" that the text layer does not contain. Flowcharts and image pages have no usable text order. Each gets a pointer chunk now. The real table is prepared separately (vision model draft, expert check), stored in `curated/`, and linked by `curated_id` (ADR-003, ADR-011).

## 7. The pipeline

Eleven steps, each writing its own file: extract lines, flag pages, find conditions, clean, prose chunks, treatment-line chunks, table-row chunks, hard-table pointers, merge and link, check, lookup tables (ADR-025, with files in [pipeline-files.md](../schemas/pipeline-files.md)). From step 3, the unit of work is the condition record (ADR-009).

## 8. Checks

Step 10 checks that every chunk has its required fields, that values are allowed (for example LOC from the known set), that every parent exists, and that no source text was lost: every piece of a condition's text must end up in a chunk or on the deliberate-drop list. Failures go to a report and not into the final file. Tests use golden pages (see `tests/README.md`).

## 9. Not decided yet

The rule for unique `condition_id`s, the exact `chunk_id` format, the final `section_type` list, and everything in Stage 3 (embedding model, vector store, parent storage, retrieval details).
