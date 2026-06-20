---
name: local-context-router
description: Use when Codex, Claude, or agy needs to inspect a long log, long source file, long markdown document, large command output, or large pasted text before sending context to a cloud LLM. Trigger for 2000+ line inputs, unclear error causes, 32768+ token risk, hermes 64K+ workflows, or requests to reduce token usage with Ollama. Routes locally with Ollama models such as gemma4:e2b-it-q4_K_M and qwen2.5-coder:3b, returning original line ranges and short rationale.
---

# Local Context Router

Use this skill to reduce a large input into original line candidates before a cloud LLM sees it. Do not summarize away the evidence. Return line ranges, surrounding context, and why each range matters.

## Model Choice

- Use `qwen2.5-coder:3b` for inputs likely under 32768 tokens and quick code/log routing.
- Use `gemma4:e2b-it-q4_K_M` for inputs that may exceed 32768 tokens, hermes workflows needing 64K+, or long document routing.

## Workflow

1. Identify the source.
   - File path, command output file, pasted text, or log artifact.
   - Prefer routing files on disk over asking the user to paste large text.

2. Estimate size.
   - Under 500 lines with clear search terms: use direct read or `rg`.
   - 500 to 2000 lines with clear symbols/errors: use `rg` first.
   - 2000+ lines or unclear cause: use this skill.

3. Ask Ollama for line ranges.
   - Keep the prompt strict: return JSON or compact bullets with `start`, `end`, `reason`, and `query_match`.
   - Ask for original line ranges, not a prose summary.
   - Prefer 3 to 10 candidate ranges.

4. Re-read the original ranges.
   - Use file reads or shell commands to inspect the selected line ranges.
   - Include only the useful original excerpts in the cloud LLM prompt.

5. Unload the model if VRAM matters.

```powershell
ollama stop gemma4:e2b-it-q4_K_M
ollama stop qwen2.5-coder:3b
ollama ps
```

## Prompt Shape

Use a prompt like this with the local model.

```text
You are a line router. Return only JSON.
Task: <what the cloud LLM needs to decide>
Input: numbered lines from <path or artifact>
Return 3-10 ranges: [{"start": 1, "end": 12, "reason": "...", "query_match": "..."}]
Do not solve the task. Do not summarize the whole file.
```

## Safety

- Treat local output as candidate selection, not final truth.
- Always inspect the original lines before using them for implementation.
- For security, data loss, or architecture decisions, use routing only to narrow context.
