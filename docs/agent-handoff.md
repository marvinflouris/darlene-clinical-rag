# Agent Handoff

Shared notes between coding sessions, so the next agent knows what the last one did. Newest entry first. Use the entry format in `docs/agent-playbooks/commit-and-handoff.md`. Put nothing sensitive here.

## Entries

### 2026-11-16

- Tool or agent: Copilot SDK
- Task: Add ADR-028 and install the approved dependencies with Python 3.12.
- Files changed: `AGENTS.md`, `docs/adrs/ADR-028-dependencies-and-python-version.md`, `docs/adrs/README.md`, `docs/status.md`, `docs/agent-exceptions.md`, `docs/agent-handoff.md`, `pyproject.toml`, `uv.lock`, and `.python-version`.
- Decisions made: ADR-028.
- Protected files touched: `AGENTS.md`, `pyproject.toml`, and `uv.lock`, with the owner's approval recorded in `docs/agent-exceptions.md`.
- Not done, and what is pending: No parser code or tests were changed; the full test suite was not run.
- Open questions for the owner: None.

### 2026-11-14

- Tool or agent: Copilot SDK
- Task: Add ADR-027, fill the checked config files, and update the related documentation.
- Files changed: `AGENTS.md`, `config/settings.yaml`, `config/drop_pages.yaml`, `config/section_labels.yaml`, `docs/adrs/ADR-027-report-unrecognised-patterns.md`, `docs/adrs/README.md`, `docs/design/data-and-chunking.md`, `docs/schemas/pipeline-files.md`, `docs/status.md`, `docs/agent-exceptions.md`, and `docs/agent-handoff.md`.
- Decisions made: ADR-027.
- Protected files touched: `AGENTS.md`, with the owner's approval recorded in `docs/agent-exceptions.md`.
- Not done, and what is pending: No code or tests were changed; dependencies were not installed.
- Open questions for the owner: None.

### 2026-11-11

- Tool or agent: Codex
- Task: Complete the documentation index and project status updates for the agent guidance files.
- Files changed: `docs/README.md`, `README.md`, `docs/status.md`, and `docs/agent-handoff.md`. The eight guidance files were already present and committed before this task.
- Decisions made: none.
- Protected files touched: none.
- Not done, and what is pending: No guard scripts or hooks, by the owner's choice. The supplied ZIP directory remains as provided.
- Open questions for the owner: none.
