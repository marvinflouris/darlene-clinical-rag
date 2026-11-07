# ADR-021: Keep both copies of the duplicated psychiatric section, flagged, until decided

- Date: 2026-11-07
- Status: accepted
- Context: Section 9.2 appears twice in the body (PDF pages 572 and 590). The copies are about 82% similar. The second Depression copy has a TREATMENT and LOC table that the first lacks. They have not been compared line by line.
- Options considered: (a) silently keep one copy; (b) keep both, flag them, and never pick silently.
- Decision: (b). Both copies stay in the data and are marked as unresolved duplicates in the condition list. If both are retrieved and differ, the system says the source has two versions and cites both. When the project owner decides, a line in corrections.yaml marks the active copy and the other moves to a superseded list (still stored, not searched).
- Why: Choosing silently could hide a conflict between two treatments.
- Consequences: Which copy is correct is an open question (see docs/status.md). It must be decided before real clinicians use the tool.
