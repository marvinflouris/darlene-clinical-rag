# ADR-025: An 11-step pipeline: each script reads the previous file and writes its own

- Date: 2026-11-07
- Status: accepted
- Context: Parsing the UCG involves many kinds of complexity, and we wanted every step to be checkable and re-runnable alone.
- Options considered: One large script, or small steps with files between them.
- Decision: Eleven steps. 1 extract lines (lines.jsonl). 2 page flags (page_register.csv, a side sheet of flags per page, not a single type). 3 find conditions (conditions.jsonl). 4 clean, and extract the glossary (conditions_clean.jsonl). 5 prose chunks (chunks_prose.jsonl). 6 treatment-line chunks (chunks_treatment_lines.jsonl). 7 table-row chunks (chunks_table_rows.jsonl). 8 hard-table pointers (chunks_pointers.jsonl). 9 merge and link (chunks_linked.jsonl). 10 check and write the final file (chunks_all.jsonl). 11 lookup tables (lookups.sqlite). Steps 5 to 8 are four separate chunk makers reading the same cleaned file.
- Why: Each step's output can be opened and checked. One step can be re-run without repeating the slow PDF read. The order is deliberate: read everything without changing it, find the structure, then clean, then cut chunks. Structure detection needs things cleaning removes, such as the chapter title in the sideways header.
- Consequences: Golden pages are the tests (see tests/README.md). Step 6, matching LOC values to drug lines by vertical position, is the riskiest and is prototyped on about 10 pages first. Step 10 checks that no source text was lost.
