# ADR-001: Design for the whole book, with no first slice

- Date: 2026-11-07
- Status: accepted
- Context: A first version covering 10 to 15 common outpatient conditions was proposed. The project owner decided to design for the whole book instead.
- Options considered: (a) a first slice of common conditions; (b) the whole book from the start, with hard items deferred.
- Decision: (b). The scripts run on the whole book. Hard tables wait as pointer chunks (ADR-011).
- Why: The pipeline treats every condition the same way, so a slice saves little. Hard tables are isolated as pointers, so they do not block the rest.
- Consequences: The mvp_include column in the condition list is not needed. The 30 expert questions serve as the retrieval test.
