# Glossary

Plain meanings of the terms used in this project.

**ADR (Architecture Decision Record).** A short file recording one decision, the options we rejected, and why. Old ADRs are never edited.

**AWaRe.** The WHO classification of antibiotics into Access, Watch and Reserve groups. The UCG refers to it. It is not part of this project's data for now.

**Alias list.** A list of other names for one condition (for example chancroid, which the UCG covers inside Genital Ulcer Disease). The condition resolver uses it.

**Applies to (`applies_to`).** A chunk field listing the conditions a chunk serves. Usually just its own condition. A management block shared by uncomplicated and severe malaria lists both.

**Chunk.** One small piece of the book that is stored and searched on its own. It is a record with an ID, its text and 18 metadata fields.

**Chunk type (`chunk_type`).** The kind of chunk: `text`, `drug_line`, `table_row`, `table` (a whole table) or `pointer`.

**Citation.** The source shown with an answer: section, page and the stored line. Code builds it from metadata, so the model cannot invent it.

**Condition.** One heading in the UCG that describes a disease or problem, for example 1.1.1 Anaphylactic Shock.

**Condition ID (`condition_id`).** Our own unique label for a condition, for example `anaphylactic-shock`. Different from the book's section number and from the ICD-10 code.

**Condition list.** The generated list of all conditions with their numbers, titles, ICD-10 codes, pages and review flags. The resolver reads it.

**Condition record.** One line of `conditions.jsonl`: a condition's details plus all its text lines. It is a container, not a chunk.

**Condition resolver.** The part that turns a clinician's diagnosis (a name or an ICD-10 code) into a `condition_id`.

**Config files.** The YAML files in `config/` that hold facts about this PDF and the owner's corrections.

**Corrections file (`corrections.yaml`).** The owner's fixes to the book, such as a wrong heading number. An empty file is fine.

**Curated table.** A hard table that has been prepared outside the main pipeline and checked by experts. Stored in `curated/`.

**`curated_id`.** The key of a curated table. A pointer chunk carries it once the table is ready.

**Differential diagnosis.** The other conditions that could look similar. One of the labelled parts of a condition.

**Edition.** The year of the guideline version (2023).

**Embedding.** A list of numbers made from a chunk's text, used to compare meaning during search.

**EMHSLU.** The Uganda Essential Medicines and Health Supplies List. A separate document that the UCG refers to. It will be a lookup table.

**Golden page.** A PDF page whose correct output we have confirmed by eye, used as a test.

**Hard table.** A table that rules cannot read reliably, such as sideways ARV tables, TB tables with grey cells, flowcharts and image pages.

**HC1, HC2, HC3, HC4, H, RR, NR.** Facility levels printed in the LOC column: health centres, hospital, and referral levels. (The exact meaning of RR and NR is to be confirmed against the UCG introduction.)

**ICD-10.** The WHO list of disease codes, the same worldwide. The UCG prints a code on most conditions, but the codes are coarse.

**JSONL.** A text file with one complete record per line. The scripts write chunks and conditions in this form.

**Line record.** One line of text from the PDF with its page, font, size, position and whether it is rotated. Step 1 writes them.

**LOC (level of care).** The facility level printed beside a drug in a Management table, where that drug can start to be used.

**Metadata.** The fields stored with each chunk (page, condition, section type and so on).

**Not covered.** A valid answer: the UCG does not say. Darlene must not guess.

**Order in condition (`order_in_condition`).** A chunk's position among all chunks of its condition. It puts chunks back in book order.

**Page flags.** One row per page in `page_register.csv` with simple flags (sideways, image, blank, has a treatment-table header).

**Parent chunk.** The big chunk a small chunk was cut from, for example the whole Management table for a drug line. Fetched by `parent_chunk_id`.

**Parent-child (small-to-big) retrieval.** Search the small chunks for precision, then give the model the parent for context.

**Pointer chunk.** A placeholder chunk left where a hard table sits, with a caption and page numbers. It says the table is not loaded yet, or points to the curated table.

**Population.** Who a condition entry is for, taken from its heading (for example children aged 2 months to 5 years).

**Prose.** Ordinary sentences and bullet lists, as opposed to tables.

**RAG (retrieval-augmented generation).** The model answers using text retrieved from our data bank, instead of from its own memory.

**Registry (`curated/registry.csv`).** The tracker of hard tables: pages, status, who prepared and who verified.

**Rotated (sideways) page.** A page printed turned 90 degrees, such as the antenatal care chart.

**Running header.** The text repeated on every page (the sideways chapter title and the book's name). Step 4 reads it for the chapter and then removes it.

**Scope check.** The step that decides whether the UCG covers the question at all.

**Section path (`section_path`).** The trail of headings leading to a chunk, like a file path.

**Section type (`section_type`).** The labelled part a chunk comes from: causes, clinical features, management and so on.

**Soft hyphen.** An invisible character the printer used to break a word across lines ("vac" + "cines"). Step 4 rejoins such words.

**SQLite.** A small database file. Ours holds exact-fact lookup tables.

**Stub.** An entry with a heading but almost no content that only says to look elsewhere. Example: 3.2.3 Pelvic Inflammatory Disease says only "See section 14.1.2".

**Syndrome.** A group of signs treated as one problem. The UCG covers many infections by syndrome rather than by organism.

**UCG.** The Uganda Clinical Guidelines 2023, our only source of chunks.

**VEN.** Vital, Essential, Necessary: a priority classification for medicines, described in the UCG introduction.

**Verdict.** The answer to "am I right to prescribe this?": supported, not supported (with the book's alternative), differs by patient group, or not covered.

**YAML.** A human-readable settings format that allows comments. Used for config files.
