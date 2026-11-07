# ADR-009: The condition record is the unit of work from step 3 onward

- Date: 2026-11-07
- Status: accepted
- Context: Conditions cross pages, and a page can hold the end of one condition and the start of the next.
- Options considered: (a) work page by page; (b) work condition by condition.
- Decision: (b). Step 3 cuts the line stream at each heading and writes one record per condition (one JSONL line) holding its details and all its text lines. Steps 4 to 8 loop over these records. Introduction and appendix material get records of their own, marked by type.
- Why: Follow the content, not the pages. Pages stay only as labels (pdf_page and printed_page).
- Consequences: A condition record is a container, not a chunk. The first chunks appear in step 5.
