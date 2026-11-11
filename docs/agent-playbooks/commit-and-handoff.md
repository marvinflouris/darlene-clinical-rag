# Playbook: commit and hand off

## Before committing

1. Run `git status`. If you are on `main`, stop. Work on a branch named `agent/<short-task>`.
2. Run `git diff --stat`. Confirm that only the files you meant to change appear. If anything else changed, stop and tell the owner.
3. If you touched a protected file with approval, add a line to `docs/agent-exceptions.md` first.

## Commit

- Stage only the intended files. Do not use `git add .` blindly.
- One logical change per commit.
- Message format:
  - Subject line: short and in the imperative, up to about 72 characters (for example `Add ADR-027: <title>`).
  - A blank line.
  - A short bullet list of what changed and why, naming ADR numbers where relevant.
  - If a protected file was changed with approval, a line such as `Protected-Change: <file>, approved by the owner`.
- Never use `--no-verify`. Never push.
- Afterwards show `git log -1 --stat`.

## Hand off

Add an entry at the top of `docs/agent-handoff.md`, newest first:

- Date
- Tool or agent
- Task
- Files changed
- Decisions made (ADR numbers)
- Protected files touched (none, or which and why)
- Not done, and what is pending
- Open questions for the owner

Update `docs/status.md` if the state of the project changed. Put nothing sensitive in either file.
