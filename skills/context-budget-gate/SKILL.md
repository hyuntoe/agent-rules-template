---
name: context-budget-gate
description: Use before sending a broad, expensive, or ambiguous task to Claude, Codex, agy, or another cloud LLM; before asking a cloud agent to inspect large logs, long files, architecture questions, or multi-file changes; and when token quota, context size, prompt caching, model switching, MCP/plugin overhead, or Claude Code usage limits matter. This skill gates cloud LLM calls by narrowing context with rg/git/graphify/local-context-router first.
---

# Context Budget Gate

Use this skill as the cloud LLM call gate. The goal is to send cloud agents only the smallest useful context, not the entire repository, log, or conversation.

## Workflow

1. Classify the request.
   - Direct answer or tiny edit: proceed without this gate.
   - Architecture, module relation, long log, long file, broad review, or multi-file change: continue.

2. Narrow with cheap local tools first.
   - Use `rg`, `git diff`, `git status`, `git log`, or language-native tooling when the target is known.
   - Use graphify for architecture, dependency, module relation, or codebase-map questions.
   - Use local-context-router for 2000+ line inputs, unclear failure causes, or inputs likely to exceed 32768 tokens.

3. Preserve Claude Code prompt caching.
   - Pick model, effort, MCP servers, and plugins at the beginning of a task.
   - Avoid changing model, effort, MCP/plugin state, or tool availability mid-task unless the benefit is worth a cache miss.
   - Use `/clear` when switching to unrelated work.
   - Use `/compact focus on <current task>` at natural long-task boundaries.

4. Prefer local workers before Claude subagents.
   - Use local scripts, graphify, and local-context-router for verbose search, log filtering, and candidate extraction.
   - Use Claude subagents only when a separate Claude context is genuinely useful. Treat them as main-context protection, not quota savings.

5. Prepare the cloud prompt.
   - Include the goal, constraints, exact files or line ranges, relevant command output, and success criteria.
   - Do not include full logs or full files when a filtered original excerpt is enough.

## Escalation

Escalate to a cloud LLM when local narrowing cannot answer the question, when judgment is needed, or when implementation and verification require repository edits.

## Related Skills

- Use `graphify-code-map` for architecture and module relationship narrowing.
- Use `local-context-router` for long logs, long files, and large text inputs.
