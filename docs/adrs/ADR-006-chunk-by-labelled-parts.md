# ADR-006: Chunk by the book's labelled parts, not by fixed size

- Date: 2026-11-07
- Status: accepted
- Context: Cutting every N characters splits clinical rules and dosing tables in half. The UCG uses consistent bold labels inside each condition: Causes, Clinical features, Differential diagnosis, Investigations, Management, Prevention and others.
- Options considered: (a) fixed-size chunks; (b) one chunk per labelled part of a condition.
- Decision: (b). A whole labelled part is one chunk (for example all of 'Clinical features'). Only a very long part is cut into pieces that point back to it. Label variants (Cause/Causes, Note/Notes) are mapped to one fixed list in config/section_labels.yaml.
- Why: The labelled part is the unit a clinician reads, and a single bullet means little alone. The parts are short (about 6 to 10 lines in the anaphylaxis example).
- Consequences: Not every condition has every label (anaphylaxis has no Investigations). Chapter 15 (family planning) uses different labels, such as Indications and Advantages.
