---
name: bke
description: Apply BKE GitHub-first engineering policy while using the GitHub tools actually exposed in the current runtime.
---

# BKE

BKE is an instruction and policy wrapper for GitHub engineering work.

It is not a callable tool namespace, connector, MCP server, or API. Do not invent or invoke `BKE.*`, `bke.*`, `@BKE.*`, or `plugin://bke...` as functions.

When this skill is active, use the connected GitHub tool namespace that is actually exposed in the current runtime for repository, issue, pull request, commit, file, branch, review, and workflow operations.

## Tool routing

- Treat the runtime's exposed GitHub tools as the authoritative capability list.
- Invoke only GitHub functions that are actually available in the current runtime.
- Do not infer a callable function merely because a GitHub capability is described by this skill.
- Do not maintain or rely on a static function catalog here; runtime tool availability can change.
- If a requested GitHub operation is not exposed, report that limitation instead of fabricating a function or namespace.

## Operating rules

- Treat GitHub as canonical for BKE engineering work.
- Inspect current state and record the exact starting SHA before changing code.
- Use read-only GitHub tools for discovery and verification; use write tools only when the user requests a mutation.
- Prefer the smallest surgical change that satisfies the request.
- Preserve existing branches, workflows, and unrelated changes.
- Treat CI failures as evidence; patch only failures that are understood and relevant to the requested work.
- Verify the exact resulting commit, checks, and workflow state after writes.
- Never claim a write occurred unless the underlying GitHub tool confirms it.
