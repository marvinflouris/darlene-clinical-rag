# ADR-022: Book typos and numbering errors go in corrections.yaml; pending ones never block a run

- Date: 2026-11-07
- Status: accepted
- Context: Examples found: a heading numbered 1.1.1 'Common Cancers in Adults' on a chapter 12 page, confirmed on the page image and in the book's own table of contents (it probably should be 12.3.2, which is unconfirmed); repeated numbers in sections 6.5.4 and 9.1.
- Options considered: (a) stop until every issue is resolved; (b) run with what we know and record corrections when decided.
- Decision: (b). The pipeline runs with an empty corrections file. Unresolved items appear in a review report. Corrections are added later and the run is repeated from step 3. Source text is never edited silently, and every correction has a reason.
- Why: Corrections can arrive late. Our own condition IDs (ADR-010) mean numbering errors do not break anything.
- Consequences: A decision that is risky for clinical use, such as ADR-021, must still be made before release.
