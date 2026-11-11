# Darlene

**A clinical-guideline RAG project for the Uganda Clinical Guidelines 2023 (UCG).**

Darlene is being built to help a clinician check a proposed outpatient prescription against the UCG before it is finalised. The target users are clinical officers and medical officers in resource-constrained primary care settings, where speed and precision both matter.

> **Status: early design stage.** The data-parsing and chunking design is recorded in the [decision records](docs/adrs/README.md). The pipeline and RAG modules in `src/` are placeholders and do not process documents or answer questions yet.

---

## How it is meant to work

Darlene has two parts: an offline pipeline that builds a checked data bank from the book, and a runtime engine (planned) that uses it.

```text
OFFLINE: build the data bank
  UCG PDF ──► pipeline (11 steps, rules only, no LLM) ──► chunks + lookup tables
  Hard tables ──► prepared separately (vision models + experts) ──► curated/

RUNTIME: planned, not designed in detail yet
  Clinician question ──► find the condition ──► load its management
                     ──► compare the proposed drug ──► verdict with citations
```

### Design principles

- **The whole book, no first slice.** The pipeline treats every condition the same way. Hard items wait as pointers ([ADR-001](docs/adrs/ADR-001-design-for-the-whole-book.md)).
- **Rules, not an LLM, for parsing.** Extraction uses fonts, positions and config files, so results are repeatable and testable ([ADR-004](docs/adrs/ADR-004-no-llm-in-parsing.md)).
- **Chunk by the book's own labels.** Causes, Clinical features, Management and so on, never fixed-size cuts ([ADR-006](docs/adrs/ADR-006-chunk-by-labelled-parts.md)).
- **Small-to-big.** Each drug line or table row is a small chunk that points to its whole table as the parent ([ADR-007](docs/adrs/ADR-007-parent-child-chunks-for-tables.md)).
- **Hard tables are prepared offline.** Sideways, colour-coded and image-based tables get a pointer chunk now and checked data later ([ADR-011](docs/adrs/ADR-011-hard-tables-as-pointers.md)).
- **"Not covered" is a valid answer.** Darlene must not answer beyond what the UCG says ([ADR-005](docs/adrs/ADR-005-scope-check-not-covered.md)).
- **Text-only main LLM.** Vision models are used only offline, to prepare tables ([ADR-003](docs/adrs/ADR-003-text-only-llm-vision-offline.md)).

## The pipeline

Each step reads the previous step's file and writes its own, so any step can be checked or re-run alone.

1. Extract lines from the PDF
2. Flag pages (blank, sideways, image, table header)
3. Find conditions (one record per condition)
4. Clean (headers, footers, split words) and extract the glossary
5. Prose chunks
6. Treatment-line chunks (Management tables with the LOC column)
7. Table-row chunks (dosing by weight, policy and Y/N tables)
8. Hard-table pointers
9. Merge and link the chunks
10. Check, then write the final chunk file
11. Lookup tables (condition list, glossary, later the EMHSLU)

Details: [ADR-025](docs/adrs/ADR-025-eleven-step-pipeline.md).

## Repository layout

```text
.
├── config/          # YAML settings and corrections (edited by hand)
├── curated/         # Expert-checked data: hard-table registry and prepared tables (tracked in Git)
├── data/            # Local only, ignored by Git
│   ├── raw/         #   source PDFs
│   ├── work/        #   output of each pipeline step
│   ├── final/       #   checked chunks
│   └── reports/     #   review and validation reports
├── db/              # Local databases, ignored by Git
│   └── vector_store/
├── docs/
│   ├── adrs/        # Decision records, one file per decision
│   ├── design/      # Data and chunking design
│   └── schemas/     # Chunk metadata specification
├── evaluation/      # Test questions from medical experts
├── src/darlene/
│   ├── pipeline/    # Offline steps 1 to 11
│   └── rag/         # Runtime modules (later stage)
└── tests/           # Tests and golden pages
```

`pyproject.toml` and `uv.lock` are at the repository root.

## Setup

Install [uv](https://docs.astral.sh/uv/), then:

```bash
uv sync
cp .env.example .env
```

Put your copy of the UCG PDF in `data/raw/`. Never commit `.env`, the PDF or other source documents; Git ignores `data/` and `db/`.

There is nothing to run yet. Commands for the pipeline and for evaluation will be added here when the code exists.

### Continue MCP servers

The workspace includes a GitHub MCP server configuration in `.continue/mcpServers/`. Add a `GITHUB_TOKEN` secret in Continue to enable it; use a fine-grained token limited to the repositories and permissions you need. Continue can start this server with `npx` and Node.js available on your `PATH`.

## Evaluation

`evaluation/questions/` holds two sets supplied by medical experts:

- `target_30.csv`: 30 pre-prescription verification questions about the UCG ("Am I correct in prescribing...?"). Experts still need to fill in the expected verdict and evidence page for each.
- `baseline_50_boundary.csv`: 50 baseline questions. Many test the edges of what the UCG covers, where the right answer is "not covered".

There is no evaluation runner yet.

## Safety and limits

- Darlene is decision support. It does not replace a clinician's judgement.
- The UCG is the only source of guideline text. Other books, such as the EMHSLU, will be added as separate lookups.
- Nothing here has been clinically validated.
- Hard tables are not loaded until they have been prepared and checked by experts. Until then Darlene should say that a table is not loaded yet.
- The UCG PDF is not part of this repository.

## Documentation and working agreement

- Current state and open questions: [docs/status.md](docs/status.md)
- Decisions: [docs/adrs/README.md](docs/adrs/README.md)
- Plain-language guide for newcomers: [docs/00-start-here.md](docs/00-start-here.md)
- Rules for coding agents: [AGENTS.md](AGENTS.md)
- Terms: [docs/glossary.md](docs/glossary.md)

Some documents are placeholders until they are written. Decisions are recorded as ADRs (Architecture Decision Records). Old ADRs are never edited; a changed decision gets a new ADR that replaces the old one.

## License

Not yet chosen.
