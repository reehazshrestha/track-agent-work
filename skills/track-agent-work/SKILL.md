---
name: track-agent-work
description: Maintain project docs for coding plans, progress, completed changes, verification, and agent ownership. Use when asked to track agent work or maintain a shared project work log.
---

# Track Agent Work

Keep a durable record of what agents will do, are doing, and have actually done. Make the next session able to continue without reading the full conversation.

## Start or resume

1. Find the project root and read applicable agent instructions. Inspect existing documentation. Reuse an existing tracker rather than creating a competing source of truth.
2. Create `docs/` if absent. Use `docs/STATUS.md` as the compact shared board unless an equivalent exists. Start from [assets/STATUS.md](assets/STATUS.md), replacing placeholders with observed facts.
3. Read the board and only the relevant task records. Check the working tree and code before trusting stale status; preserve other contributors' work.
4. Before implementation, record a stable task ID such as `2026-11-08-chat-retry`, objective, acceptance criteria, intended steps, owner, status, and expected files or areas.

Use your actual agent product/name, such as `codex`, `opencode`, or `claude`. Add a session or role suffix when known and useful to distinguish concurrent agents. Never invent model names, session IDs, contributors, or historical attribution. Use `unknown` when evidence is unavailable.

## Maintain the record

- Use `planned`, `in_progress`, `blocked`, `partial`, `done`, or `cancelled`. Separate intended work from actions already performed.
- Update at meaningful milestones, scope changes, blockers, handoffs, and before the final response. Avoid logging every command or repeatedly rewriting docs for trivial steps.
- Record what changed, why, relevant paths, and checks actually run with observed results. Write `not run` when appropriate, explaining material verification gaps. Link useful artifacts instead of copying raw transcripts.
- Mark `done` only when agreed work and required checks are complete. Record unfinished steps when stopping with `partial` or `blocked`.
- Attribute implementation and review separately. Coordinators must credit the implementing agent. Distinguish another agent's reported results from checks you personally ran.
- Track only agents actually involved. This skill does not require spawning agents or authorize delegation.

For a small task, one board row and one signed recent-change entry are enough. For work spanning sessions, involving multiple agents, or needing a longer plan, create `docs/work/<task-id>.md` from [assets/task.md](assets/task.md) and link it from the board. Keep details there rather than duplicating them across documents.

## Ownership and handoffs

Read the latest ownership before claiming a task. Do not silently take over active work. Record explicit ownership changes: previous owner, next owner, completed work, remaining steps, relevant files, verification, blockers, and the next executable action. Say `unassigned` when no next owner exists.

When concurrent agents are already working, prefer separate task records and designate one existing coordinator to update the shared board. Reread shared files immediately before editing, make narrow edits, and preserve unrelated entries. Markdown ownership is not an atomic lock; resolve competing claims through the project's existing coordination mechanism.

## Keep documentation useful

- Keep `STATUS.md` focused on active work, next steps, blockers, and short recent history. Move older completed records into linked `docs/archive/` files when they obscure current work, preserving attribution and evidence.
- Keep secrets, credentials, private conversations, and unnecessary personal data out of docs. Prefer repository-relative paths.
- Add architecture, decision, and specification documents only when needed. Do not create empty folders or copy project-specific release/install rules into unrelated projects.
- When setting up this workflow, add a short instruction to the project's existing `AGENTS.md` (or create it if absent), preserving existing instructions: "Before coding, read docs/STATUS.md and claim or create the relevant task. Record plans, milestone progress, verification, and actual agent attribution. Update the record before reporting completion." Adjust the path for an existing tracker. Update other agent instruction files only if the project already uses them or the user requests them. A skill installation alone does not make every agent load it.

Before finishing, reconcile the board and task record with the actual diff and verification. Link the updated record in the final response and disclose unfinished work.
