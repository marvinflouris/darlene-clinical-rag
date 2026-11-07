# Vision and Scope

## Vision

Darlene aims to set the standard for clinical decision support in Uganda, with no shortcuts. It is meant to work as a clinical co-pilot, not a chatbot that guesses at treatments. It connects the exact text of the Uganda Clinical Guidelines to a practitioner's day-to-day work through a small-to-big retrieval engine. When a clinician asks about a condition, Darlene's answer comes from stored guideline text, built by rule-based parsing, with the level-of-care tag, the exact drug line and the full parent table that it came from. Every answer shows its source.

Darlene is meant to show that AI infrastructure can be built with industrial-grade rigour: accuracy that is checked, a pipeline that checks it has lost no text, and answers that say clearly where they come from and where they stop.

## What Darlene is for

Checking a proposed outpatient prescription against the UCG before it is finalised, for clinical officers and medical officers in resource-constrained primary care settings, where speed and precision both matter.

## Principles in practice

- No LLM in the parsing pipeline: rules only (ADR-004).
- Every answer traces to a stored guideline line and its page (ADR-019).
- Hard tables are prepared offline and checked by experts before they are used (ADR-011).
- Darlene says "not covered" when the UCG does not say (ADR-005).
- The pipeline checks that no source text is lost (ADR-025).
- Decisions are recorded and old records are never edited (ADR-023).

## In scope

- The whole UCG 2023 as the source of chunks (ADR-001, ADR-002).
- Pre-prescription verification: is this drug, for this patient group, with this condition, supported by the UCG?
- Citations with page numbers.
- A checked data bank, with hard tables prepared separately.

## Out of scope for now

- Guidelines other than the UCG as chunk sources (WHO AWaRe, ICD-10 manual). The EMHSLU is added only as a lookup table.
- Detailed ICD-10 coding. The UCG's codes are coarse.
- Pharmacy stock, prices, and patient records. Allergies and kidney function are inputs to a query, not retrieved from the book.
- Diagnosis. Darlene does not diagnose.
- Image-only pages, such as growth charts.

## What we do not promise

- Darlene cannot remove human error, and it is not a replacement for clinical judgement.
- Nothing has been clinically validated yet.
- The part of the system that writes the answer is a language model, and models can make mistakes. The design limits the risk: guidance comes from stored text, answers carry citations built from stored data, tables are checked, and "not covered" is a valid answer.

## How we will know it works

- Coverage: the pipeline's check shows that no source text was lost.
- Retrieval and answers: the 30 expert questions, with expert-supplied expected verdicts and evidence pages, plus the 50 boundary questions for "not covered" behaviour.
- Citations point to the right page.
- Hard tables are checked by experts before use.

## Stages

1. Design and parsing plan.
2. Build the chunks and seed the lookup tables.
3. Plan the RAG pipeline: retrieval, evaluation, models, frontend access.
4. Implement.
5. Prompts and frontend (a simple prototype first).
