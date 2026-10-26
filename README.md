# Clinical RAG System

A production-grade, domain-specific Retrieval-Augmented Generation (RAG) system designed for clinical document processing, indexing, and retrieval workflows.

This project is configured to use `uv` as the package and environment manager. It keeps the environment lightweight and lets you install only the dependencies you need.

---

## Overview

The system follows a modular pipeline:

- clinical document ingestion
- indexing and vector-store preparation
- retrieval for grounded query answering
- application entry point for running the workflow

---

## Project Structure

```text
.
├── data/
│   └── sample_docs/
├── storage/
├── src/
│   ├── __init__.py
│   ├── ingestion.py
│   ├── index_builder.py
│   └── retriever.py
├── main.py
├── pyproject.toml
├── requirements.txt
├── README.md
├── .env
├── .gitignore
├── config.py
└── .venv/   # generated locally by uv when you initialize the environment
```

---

## Using uv

### 1. Install uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

If `uv` is already installed, skip this step.

### 2. Create the environment

```bash
uv venv
```

This creates a local virtual environment without preinstalled dependencies.

### 3. Install dependencies

Add packages explicitly as needed:

```bash
uv add <package-name>
```

Or install from the project requirements file:

```bash
uv pip install -r requirements.txt
```

### 4. Run the project

```bash
uv run python main.py
```

### 5. Refresh the lockfile

```bash
uv lock
```

---

## Environment Variables

Create a local `.env` file for any API keys or sensitive settings you do not want committed to Git.

Example:

```env
OPENAI_API_KEY=your_key_here
```

---

## Notes

- No local virtual environment is included. The `uv.lock` file records resolved versions but does not install packages by itself.
- This project is intentionally minimal and ready for manual dependency installation with `uv`.
- Do not commit environment files unless you explicitly want to share them.
