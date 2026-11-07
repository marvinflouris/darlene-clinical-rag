# ADR-004: No LLM in the parsing pipeline; rules only

- Date: 2026-11-07
- Status: accepted
- Context: Heading detection, cleaning and table cutting could each use an LLM.
- Options considered: (a) LLM-assisted parsing; (b) rule-based scripts using fonts, positions and config files.
- Decision: (b).
- Why: It costs nothing to run, gives the same result every time, and is easy to test and re-run. It also removes any risk of a model inventing text in a medical source. The project owner said an API call to a language model does not suit parsing.
- Consequences: Unusual cases go to review reports and corrections.yaml. The only exception is the offline vision preparation in ADR-003.
