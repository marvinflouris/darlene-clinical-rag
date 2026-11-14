# Status

Last updated: 2026-11-14

## Current stage

Stage 1: design and parsing plan. The owner's five stages are:

1. Decide the unit chunk, design the parser, and plan the extra databases and reference books.
2. Build the chunks in splits (one script per kind of content) and seed the lookup tables, so we end with a ready data bank.
3. Plan the RAG pipeline: retrieval, quality strategies, evaluation and tracking (for example RAGAS and logging), the LLM and API choices, and how a frontend reaches the system.
4. Implement it.
5. Design the prompts, then the frontend (prototype first with something simple, such as Gradio).

## Done

- Audited the structure of the UCG PDF: 1,161 pages, a readable text layer, no bookmarks, and printed page = PDF page minus 66.
- Built a first condition list (generated, not yet reviewed): 477 entries and 70 section headings. 291 entries have their own ICD-10 code, 87 inherit one from a parent entry, and 99 have none. 172 entries carry at least one review flag.
- Designed the chunk metadata: 17 fields in four groups ([schemas/chunk-metadata.md](schemas/chunk-metadata.md)). The `population` field was dropped by ADR-026.
- Recorded the decisions as ADR-001 to ADR-027: 24 accepted and 3 proposed (ADR-017, 019, 020). ADR-012 is partly replaced by ADR-026.
- Wrote the config files with checked facts (settings, drop pages, section labels) and ADR-027 (report unrecognised patterns).
- Created the repository skeleton, the README and the config placeholders.
- Received the expert question sets: 30 target questions and 50 baseline questions. The expected answers are not filled in yet.
- Drafted this documentation set.
- Added agent guidance files: AGENTS.md, five playbooks, a handoff file and an exceptions log.

## Open decisions

- Which copy of the duplicated psychiatric section 9.2 is correct (PDF pages 572 and 590). See ADR-021.
- The EMHSLU: the PDF is to be supplied, and its layout is unknown. See ADR-002 and ADR-018.
- Expected verdicts and evidence pages for the 30 target questions (experts).
- Review of the 172 flagged entries in the condition list: repeated numbers, entries with no ICD code, entries whose management table sits in a parent or sibling, and entries on sideways or image pages.
- Whether to apply the heading fix "1.1.1 Common Cancers in Adults" to 12.3.2. It is a typo in the book, but the corrected number is unconfirmed.
- Who prepares and who verifies the hard tables, and which vision model is used for the draft step.
- Stage 3 choices: the LLM, the embedding model, the vector store, where parent chunks are stored, and the details of ADR-017, 019 and 020.
- The frontend.
- The license.
- The dependency list and the Python version (agree the list, research the versions, let uv resolve them).

## Next steps

1. Agree the dependency list and the Python version. Nothing is installed before this.
2. Before parser design, revisit the hard-table plan: pointer chunks with curated_id, the practitioner reads the full table, and any vision-model simplification is done and checked in the preparation stage so the main LLM stays text-only.
3. Write the plan for step 1 and get it approved. Code and tests follow phase by phase, with the review reports read after each step.

## Risks to watch

- Step 6 (matching each LOC value to its drug line by vertical position) is the riskiest step. It will be prototyped on about 10 pages first.
- The two copies of section 9.2 may disagree on treatment. This must be settled before real clinicians use the tool.
- Hard-table preparation depends on expert time.
- Heading detection in the condition list is approximate and must be checked against page images.
- A text style the config does not know about can put text in the wrong part without losing it. Steps 3, 5 and 10 report such cases (ADR-027).
