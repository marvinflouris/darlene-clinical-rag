# ADR-024: File types are chosen by who writes and reads them

- Date: 2026-11-07
- Status: accepted
- Context: The project uses several file types and we needed a clear rule for each.
- Options considered: One format for everything, or a format per role.
- Decision: People write Markdown and YAML. Scripts write JSONL (chunks and conditions, one record per line) and SQLite (lookup tables). People review spreadsheets, which are kept as CSV in git, with xlsx only as a convenience copy. Generated data (data/ and db/) is ignored by git. Human-made material (docs/, config/, curated/, evaluation/) is tracked.
- Why: YAML allows comments beside settings. JSONL copes with commas, line breaks and lists inside chunks, and one bad line does not break the file. SQLite gives fast exact lookups. CSV can be tracked line by line in git, which xlsx cannot.
- Consequences: curated/ must be tracked because nothing can regenerate it. corrections.yaml and the registry are edited by hand.
