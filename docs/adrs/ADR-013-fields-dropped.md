# ADR-013: Fields dropped from the chunk metadata, with reasons

- Date: 2026-11-07
- Status: accepted
- Context: Several fields were proposed and then removed after testing them against how the system will be used.
- Options considered: Keep as fields, or keep the information in the chunk text, or drop.
- Decision: Dropped: drug_name (and an alias list), scenario, line_order, loc, redirects_to. Not stored as fields either: first-line or alternative labels, pregnancy flags, numeric dose fields. The information that matters stays in the chunk text, for example 'When: In severely affected patients' and 'LOC: HC3'.
- Why: drug_name: retrieval is condition-first and the drug is already in the text and the embedding; names are messy to extract from lines with several drugs. scenario: the sub-headings are free wording nothing would filter on. line_order: order_in_condition and the parent table already give the order, and '-Or' stays in the text. loc: the text already carries it, and no expert question asked about facility level. redirects_to: only the PID entry is a confirmed stub, and the link lives in the condition list. First-line labels: the book uses the words inconsistently. Pregnancy flags: a wrong flag is a safety risk. Numeric doses: a later phase.
- Consequences: A script can add any of these later by reading the chunk text, without re-chunking. If tests show spelling differences cause real misses, drug_name comes back.
