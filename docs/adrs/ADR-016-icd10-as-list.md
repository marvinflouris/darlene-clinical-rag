# ADR-016: ICD-10 stored as a list, inherited from the parent entry when missing

- Date: 2026-11-07
- Status: accepted
- Context: The code label is spelled 8 different ways. Codes appear as single codes, ranges (about 36), multiple codes (about 24) and odd forms (J09.X2, Z30.018/Z30.49). Sub-entries often have none.
- Options considered: (a) store only exact single codes; (b) store what is printed as a list and inherit from the parent.
- Decision: (b). Ranges are kept as printed. A sub-entry inherits the nearest parent's code, and the condition list records which codes were inherited (icd_source).
- Why: The code is an exact match between a diagnosis and the book's entry, and sub-entries of a coded condition are about the same disease.
- Consequences: The UCG's codes are coarse, so detailed ICD-10 coding is out of scope (ADR-005). The condition list has icd10_raw, icd10_final and icd_source columns.
