# ADR-020: Order of retrieval improvements: cheap fixes first, fine-tuning later

- Date: 2026-11-07
- Status: proposed
- Context: Options considered were hybrid search, reranking, routing, small-to-big, Deep Memory (a Deep Lake feature that needs the Deep Lake vector store and labelled query-chunk pairs) and embedding fine-tuning (including an adapter on top of a black-box embedding model).
- Options considered: Adopt all at once, or add them one at a time and measure.
- Decision: Start with the baseline: structure-based chunks, metadata filters and hybrid search. Measure. Then add a reranker and small-to-big tuning, then routing. Compare a few embedding models on the test questions. Use abbreviation expansion from the glossary. Fine-tuning and Deep Memory only if the measurements justify them.
- Why: The likely failures are exact terms (drug names, abbreviations, ICD codes, 'HC3'), which cheaper fixes handle. Fine-tuning needs labelled pairs and vendor lock-in is a risk.
- Consequences: A gold test set comes first, built with a clinician, with a held-out part that is never used for training. Final choices are made in Stage 3.
