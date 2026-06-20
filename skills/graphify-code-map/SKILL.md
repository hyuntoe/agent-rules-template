---
name: graphify-code-map
description: Use before asking a cloud LLM to rediscover codebase architecture, module relationships, dependency paths, core abstractions, or files likely relevant to an implementation. Trigger for architecture questions, "where should I change this?", cross-module behavior, unfamiliar repositories, or when graphify-out exists. Prefer graphify query/path/explain/update before broad file reads.
---

# Graphify Code Map

Use this skill to narrow codebase context before reading many files or calling a cloud LLM. Graphify is a map, not the final source of truth.

## Workflow

1. Check for existing graph output.
   - If `graphify-out/GRAPH_REPORT.md` exists, read it first.
   - If `graphify-out/wiki/index.md` exists, use it before direct broad file reads.

2. Choose the graph query.
   - Architecture overview: `graphify query "<question>"`
   - Relationship between concepts: `graphify path "<A>" "<B>"`
   - A specific abstraction: `graphify explain "<concept>"`
   - Stale or missing graph: `graphify update .`

3. Use graph output to select files and symbols.
   - Convert graph results into a short list of candidate files, concepts, and call paths.
   - Re-read original files for the final evidence.

4. Prepare cloud context.
   - Send the cloud LLM the graph answer, candidate files, and only relevant original excerpts.
   - Avoid asking the cloud LLM to rediscover the whole repository when graphify already narrowed it.

## When Not To Use

- Tiny tasks in known files.
- Pure text or documentation edits with no codebase relationship question.
- Cases where graph output is stale and `graphify update .` cannot be run.

## Verification

After code structure changes, update graphify when the project uses it and the change affects architecture or module relationships.
