# Specification

## Purpose

Hybrid semantic search CLI for Obsidian vaults using Qdrant and OpenAI.

This tool enables fast semantic search across Obsidian notes by embedding content with FastEmbed (local) or OpenAI (remote) and storing vectors in a Qdrant database. It provides a command‑line interface for indexing, searching, and managing a second‑brain knowledge base.

## Inputs

- **Obsidian vault path** (local directory containing markdown files)
- **Qdrant instance** (local or remote; URL and API key via environment variables)
- **OpenAI API key** (optional, for OpenAI embeddings; otherwise uses local FastEmbed)
- **Environment variables** (see `.env.sample`):
  - `SB_QDRANT_URL`
  - `SB_QDRANT_API_KEY`
  - `SB_QDRANT_OPENAI_API_KEY` (optional)
  - `SECOND_BRAIN_FOLDER_PATH` (defaults to environment variable, can be overridden with `--vault`)
  - `SB_QDRANT_HF_TOKEN` (optional, for Hugging Face token)
  - `SB_QDRANT_COLLECTION_NAME`
  - `SB_QDRANT_EMBED_MODEL` (default: `text-embedding-3-small`)
  - `SB_QDRANT_BATCH_SIZE` (default: 64)
  - `SB_CACHE_DIR`, `SB_QDRANT_CACHE_FILE`, `SB_QDRANT_INDEX_CACHE`

## Outputs

- **Qdrant collection** with embedded vectors of note chunks
- **Search results** displayed in the terminal (ranked list of notes with similarity scores)
- **Logs** of indexing and search operations

## Usage

### Installation (development)

```bash
uv sync                # install dependencies
uv run pip install -e .  # install package in editable mode
```

### Environment setup

Copy `.env.sample` to `.env` and fill in the required variables. The vault path is pre‑set to the local second‑brain directory (`/home/janwyl/.openclaw/workspace/second‑brain`). Set `SB_QDRANT_URL` and `SB_QDRANT_API_KEY` to point to a running Qdrant instance (local Docker or cloud). Optionally set `SB_QDRANT_OPENAI_API_KEY` for OpenAI embeddings.

### Indexing

```bash
second-brain embed --vault /path/to/vault   # or rely on SECOND_BRAIN_FOLDER_PATH
```

### Searching

```bash
second-brain search "query text"
```

### Graph‑boosted search

```bash
second-brain search-graph "query text"
```

### Other commands

```bash
second-brain --help
```

## Notes

- The CLI is built with Typer.
- Supports both local (FastEmbed) and remote (OpenAI) embedding models.
- Qdrant can be run locally via Docker or use a cloud instance.
- The project follows the Python Playground conventions (UV, src‑layout, Ruff, pytest).
- **GitHub repository:** https://github.com/jarvisanwyl/second‑brain‑cli
- **Source history:** Migrated from jlad26/second_brain_cli with full commit history preserved.