# ADR-010: Our own condition_id, not the book's number and not ICD-10

- Date: 2026-11-07
- Status: accepted
- Context: Section numbers repeat in the book (9.1.1 appears twice; a heading numbered 1.1.1 sits in chapter 12). ICD-10 codes can be shared, given as ranges, or missing: in the first condition list, 291 of 477 entries have their own code, 87 inherit one, and 99 have none.
- Options considered: (a) use the book's section number; (b) use the ICD-10 code; (c) generate our own label.
- Decision: (c). Each condition entry gets a unique label made by the pipeline (for example anaphylactic-shock). The book's number and the ICD-10 codes are kept as data.
- Why: Our label is unique and stable.
- Consequences: Typos in the book do not break links. A wrong number can be corrected in corrections.yaml without changing the label.
