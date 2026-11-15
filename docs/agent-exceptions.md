# Agent Exceptions

A log of every approved change to a protected file (the list is in `AGENTS.md`). Add a line before the commit, and mention it in the commit message.

Format:

- Date | file | what changed and why | approved by

## Entries

- 2026-11-16 | AGENTS.md | Added the approved dependency list and PyMuPDF import rule (ADR-028) | Owner
- 2026-11-16 | pyproject.toml | Added approved dependencies and changed requires-python from >=3.13 to >=3.12 for the approved Python pin (ADR-028) | Owner
- 2026-11-16 | uv.lock | Locked the approved dependency versions for Python 3.12 (ADR-028) | Owner
- 2026-11-14 | AGENTS.md | Added the ADR-027 unrecognised-patterns design rule as requested | Owner
