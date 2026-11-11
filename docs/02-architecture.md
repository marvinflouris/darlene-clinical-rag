# Architecture

The big picture of Darlene as designed so far. The offline part is designed in detail. The runtime part is a direction and is designed in Stage 3.

## Two parts

```text
OFFLINE: build the data bank (rules only, no LLM)
  UCG PDF ──► 11-step pipeline ──► data/final/chunks_all.jsonl
                              └──► db/lookups.sqlite
  Hard tables ──► prepared separately (vision-model draft + expert check) ──► curated/

RUNTIME: planned (Stage 3)
  Clinician question
     ──► understand the question: condition, drug, patient group, regimen
     ──► resolve the condition (condition list, ICD-10, aliases) and follow stubs
     ──► load the condition's Management and the blocks that apply to it
     ──► the LLM compares the proposed drug and gives a verdict
     ──► scope check: "not covered" is allowed
     ──► code builds the citations; drug details come from the EMHSLU table
```

## Offline: the data bank

- **`chunks_all.jsonl`**: checked chunks with 17 metadata fields, ready to embed in the next stage ([chunk-metadata.md](schemas/chunk-metadata.md)).
- **`lookups.sqlite`**: exact facts looked up by key: the condition list, the glossary, the lab menu, later the EMHSLU.
- **`curated/`**: hand-made, expert-checked tables and the registry of hard tables. Tracked in Git because nothing can regenerate it.
- Pointer chunks mark hard tables until they are ready.

The pipeline is described in [design/data-and-chunking.md](design/data-and-chunking.md) and [schemas/pipeline-files.md](schemas/pipeline-files.md).

## Runtime: the direction

- **Condition first.** The system resolves the condition, loads its Management and the blocks that apply to it, and compares the drug against it. Drug-first search is noisy because common drugs appear in dozens of sections (ADR-017, proposed).
- **Small-to-big.** Small chunks are searched. Their parents give context (ADR-007).
- **Drug facts after the answer.** The model names the drugs it used. Code looks them up in the EMHSLU table, with no agent loop (ADR-018).
- **Citations by code.** The model returns only chunk IDs (ADR-019, proposed).
- **Text-only main LLM.** Vision is used only offline (ADR-003).
- **Retrieval improvements are added in order and measured.** Hybrid search, reranking and routing come before any embedding fine-tuning (ADR-020, proposed).

## What is decided and what is not

- **Decided:** the offline pipeline, the chunk and metadata design, the handling of hard tables and data-quality problems, and the documentation approach.
- **Proposed:** condition-first retrieval, citations by code, and the order of retrieval improvements.
- **Not decided:** the LLM, the embedding model, the vector store, where parent chunks are stored, and the frontend. See [status.md](status.md).
