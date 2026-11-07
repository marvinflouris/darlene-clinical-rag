# ADR-015: The chunk header is built from metadata, not written by an LLM

- Date: 2026-11-07
- Status: accepted
- Context: A chunk such as 'Repeat every 5-10 minutes' means little alone. An LLM-written situating sentence per chunk (contextual retrieval) was considered.
- Options considered: (a) an LLM-written sentence on every chunk; (b) a header built from metadata; (c) both.
- Decision: (b). A header such as 'UCG 2023 · Anaphylactic Shock (T78.2) · Management · p.2' is assembled from the fields when chunks are embedded and when they are shown to the model. It is not stored twice. No LLM sentence for now.
- Why: It is free, cannot invent facts, and is easy to check. In a medical source, a wrong generated sentence would pollute the search.
- Consequences: Revisit after running the 30 questions: if misses cluster on hard-to-read chunks (table rows are the likeliest), add LLM sentences to those chunks only. Table captions are made from templates.
