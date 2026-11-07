# ADR-011: Hard tables are pulled out and left as pointer chunks

- Date: 2026-11-07
- Status: accepted
- Context: Some tables cannot be parsed reliably. ARV dosing tables are sideways and use dashes for empty cells. TB tables use dark grey 'not applicable' cells that are not in the text layer. There are also flowcharts and image pages. Candidates found so far: 34 entries touch sideways or image pages.
- Options considered: (a) force the parser to read them; (b) prepare them outside the main pipeline and bring them back.
- Decision: (b). They are prepared separately (vision models plus experts) and return as chunked tables, row records or lookup tables. At each spot the parser leaves a pointer chunk with a caption, page numbers and a curated_id key. Step 8 writes a candidates list; curated/registry.csv is maintained by people.
- Why: Accuracy matters more than speed. The system works without them, and the pointer's caption lets search find the table.
- Consequences: Until a table is prepared, the system says 'this part has a table that is not loaded yet, see page N' and does not guess from the text around it. Vision simplification happens in preparation and is checked (ADR-003). Some candidates may turn out to parse fine and are tested first.
