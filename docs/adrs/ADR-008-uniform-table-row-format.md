# ADR-008: One uniform record format for table rows

- Date: 2026-11-07
- Status: accepted
- Context: Tables vary: treatment lines with an LOC column, dosing by weight, policy tables, Y/N matrices.
- Options considered: (a) a different method depending on table size; (b) one record format for every table.
- Decision: (b). Every row becomes a record in which each value is paired with its column header, and the whole table is its parent. The table title comes from the nearest heading, because the book rarely uses captions. Hard tables may use a different extraction method but must produce the same format.
- Why: The project owner preferred one format over a method that changes with size. One format means one way to retrieve and to display.
- Consequences: Cells are also stored as structured header-to-value pairs, so the interface can later draw small tables. A dash meaning 'no dose' is written out and is never turned into 0.
