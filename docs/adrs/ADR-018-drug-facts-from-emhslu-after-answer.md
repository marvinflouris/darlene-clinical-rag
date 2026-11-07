# ADR-018: Drug facts come from the EMHSLU table after the answer; no agent loop

- Date: 2026-11-07
- Status: accepted
- Context: Citation pop-ups and 'is this drug on the essential list' checks need drug details.
- Options considered: (a) a drug tag stored in every chunk; (b) an LLM agent that decides when to call a lookup; (c) a fixed lookup step after the answer.
- Decision: (c). The model lists the drugs it relied on as part of its answer, which needs no extra LLM call. Code looks those names up in the EMHSLU table and attaches the result to the citation.
- Why: A table lookup takes milliseconds. Asking an LLM to decide when to look something up costs time and money and varies from run to run, and here the need is predictable. The project owner agreed not to rely on an LLM for this.
- Consequences: No drug_name field in chunks. Agent-style tool calling is kept for unpredictable outside needs such as pharmacy stock or patient records, after this stage. The EMHSLU PDF is still to be supplied.
