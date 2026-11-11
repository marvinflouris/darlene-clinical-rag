# Start Here

A plain-language guide for anyone new to Darlene.

## What Darlene is

Darlene is a project to help a clinician check a proposed prescription against the Uganda Clinical Guidelines 2023 (the UCG), a book of more than a thousand pages. It is at an early design stage. The code is not written yet, and this guide explains the plan.

## The idea in one paragraph

A language model answering from memory can be wrong in ways nobody notices. So Darlene will answer from the guideline's own text, stored in a data bank that we build and check carefully. First we turn the book into small, labelled pieces called chunks. Later, when a clinician asks a question, the system finds the right condition, loads what the book says about it, compares the proposed drug, and answers with a citation to the page.

## The book and why it is hard

The UCG is a PDF made for printing. Conditions have headings, and inside each there are labelled parts: Causes, Clinical features, Management and so on. The Management part is usually a table of drugs with a level-of-care column (LOC) saying where each drug can be used. But the book has many quirks. Some pages are printed sideways. Some tables use colour or dashes to carry meaning. A few sections appear twice, and some numbers are wrong. Cutting the text every 500 characters would split doses from their children's doses, so we cut along the book's own labels instead.

## The key ideas

- **Chunk.** One small piece of the book that is stored and searched on its own.
- **Metadata.** The facts stored with a chunk: its page, condition, section type and so on (17 fields).
- **Parent and child.** A drug line is a small chunk (a child). Its whole table is the big chunk (the parent). Search finds the small one, and the model receives the big one for context.
- **Condition record.** A container holding everything the book says about one condition. We cut chunks out of it.
- **Hard tables.** Tables that rules cannot read reliably. They are prepared separately by vision models and experts. Until then a pointer chunk marks the spot, and Darlene says the table is not loaded yet.
- **Not covered.** If the UCG does not say, Darlene says so instead of guessing.

## How the pipeline builds the data bank

It is a chain of 11 small scripts. Each reads the previous script's file and writes its own, so we can open and check every step. Follow one line, the adrenaline dose for anaphylactic shock:

1. Step 1 reads it from page 68 of the PDF, with its font and position.
2. Step 2 notes that page 68 has a treatment table.
3. Step 3 knows it belongs to condition 1.1.1, Anaphylactic Shock, because that heading came before it.
4. Step 4 removes the sideways page header around it.
5. Step 6 turns it into a chunk with its dose, its child doses and `LOC: HC2`.
6. Step 9 gives the chunk its position in the condition.
7. Step 10 checks it, and it goes into `data/final/chunks_all.jsonl`.

A prose part such as "Causes" is made by step 5 instead.

## Rules we follow

- No LLM is used to parse the book. Rules only, so results repeat exactly.
- Everything is traceable to a page.
- Decisions are written down as ADRs. Old ADRs are never edited. Open questions go in `docs/status.md`.
- Hand-made, expert-checked data is tracked in Git. Generated data is not.

## Where to read next

1. [docs/01-vision-and-scope.md](01-vision-and-scope.md): what we are building and what we are not.
2. [docs/02-architecture.md](02-architecture.md): how the parts fit.
3. [docs/design/data-and-chunking.md](design/data-and-chunking.md): how the book becomes chunks.
4. [docs/adrs/README.md](adrs/README.md): the decisions and their reasons.
5. [docs/status.md](status.md): where we are now.
6. [docs/glossary.md](glossary.md): any term you do not know.
