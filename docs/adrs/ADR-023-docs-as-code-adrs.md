# ADR-023: Documentation as Markdown in the repository; one ADR file per decision

- Date: 2026-11-07
- Status: accepted
- Context: The project needs a record of decisions, plans, rejected options and current state, understandable by a newcomer.
- Options considered: (a) Word files or a wiki; (b) Markdown files in the repository, tracked with git.
- Decision: (b). ADR means Architecture Decision Record: a short file per decision, in docs/adrs/. Old ADRs are never edited; a changed decision gets a new ADR that replaces the old one. Open questions stay in docs/status.md. There is a plain-language start-here guide. A snapshot is taken with a git tag at the end of Stage 1. The project owner's own folder plan (docs/adrs, docs/schemas) was adopted.
- Why: Documents and code change together and the history shows who changed what and why.
- Consequences: The set is: README, start-here, vision and scope, architecture, a data and chunking design, schemas, ADRs, status, glossary. Each document gets an approved outline before it is written.
