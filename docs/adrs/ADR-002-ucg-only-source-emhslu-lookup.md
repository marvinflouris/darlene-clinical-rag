# ADR-002: The UCG is the only source of chunks; the EMHSLU is a separate lookup

- Date: 2026-11-07
- Status: accepted
- Context: The UCG refers to the EMHSLU for drug names and facility levels, and to the WHO AWaRe book for antibiotics. We had to decide whether to ingest those books too.
- Options considered: (a) mix them into the chunks; (b) keep them as separate lookup tables; (c) skip them.
- Decision: Only the UCG makes chunks. The EMHSLU (a PDF full of tables, to be supplied by the project owner) becomes a separate lookup table. The UCG's own abbreviation list (around PDF pages 33-43) is the glossary. The WHO AWaRe book and the dispensing guide are not added now.
- Why: The UCG only mentions the other books in its introduction and does not reproduce their lists. They are exact lookups, not text to search by meaning.
- Consequences: Drug details for citation pop-ups come from the EMHSLU table after the answer is written (ADR-018). The EMHSLU layout must be inspected when it arrives.
