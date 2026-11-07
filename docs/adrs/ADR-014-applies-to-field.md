# ADR-014: applies_to for blocks that serve several conditions

- Date: 2026-11-07
- Status: accepted
- Context: In malaria, the 'Management of Malaria' block comes after the uncomplicated and severe entries and covers both. In the first condition list, 83 entries have no treatment table of their own while a parent or sibling does (a heuristic flag; some may be false alarms).
- Options considered: (a) tie management to the nearest heading by position; (b) list the conditions each block serves.
- Decision: (b). applies_to is a list of condition IDs. Usually it holds only the chunk's own condition. Loading a condition also loads blocks that list it.
- Why: Position alone would return uncomplicated malaria with symptoms but no treatment.
- Consequences: Step 9 fills applies_to. The flagged entries are reviewed by hand.
