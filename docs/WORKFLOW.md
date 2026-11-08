# Workflow and example

## Set up a project

Read existing agent instructions and docs first. Reuse the project's tracker if it has one. Otherwise create `docs/STATUS.md` from the skill's template and add this brief instruction to the project's `AGENTS.md`, preserving its existing contents:

> Before coding, read docs/STATUS.md and claim or create the relevant task. Record plans, milestone progress, verification, and actual agent attribution. Update the record before reporting completion.

Do not assume other agent tools read `AGENTS.md`. Add a pointer to their existing instruction file where appropriate. Installation alone does not turn this into an always-running tracker.

## Task lifecycle

| State | Meaning |
| --- | --- |
| `planned` | Agreed work that has not started |
| `in_progress` | An identified owner is actively working |
| `blocked` | A concrete dependency prevents progress |
| `partial` | Some work is complete; remaining work is recorded |
| `done` | Agreed outcome and required checks are complete |
| `cancelled` | Work was explicitly dropped; reason recorded |

Update at meaningful milestones, scope changes, handoffs, and before the final response. Record timestamps with a timezone. Keep task IDs stable even if ownership or the title changes.

## Fictional example

The following rows illustrate the format; they are not claims about checks performed in this repository.

| Task ID | Objective | Status | Owner | Next step or blocker | Record |
| --- | --- | --- | --- | --- | --- |
| 2026-11-08-chat-retry | Retry transient chat failures | in_progress | opencode/session-a | Add timeout regression check | work/2026-11-08-chat-retry.md |

A completion entry might read:

```markdown
### 2026-11-08T09:30:00+05:45 — 2026-11-08-chat-retry — Retry transient failures

- Status: done
- Change: Retry temporary failures twice; preserve permanent errors.
- Files: `src/chat.ts`, `tests/chat.test.ts`
- Checks: `npm test -- chat` — 6 passed
- Remaining: none
- Implemented by: opencode/session-a
- Reviewed by: codex/session-b
```

If checks were not run, replace the checks line with `not run` and a reason. If a required check is still outstanding, keep the task `partial` rather than claiming it is done.

## Handoff example

```markdown
- From / to: opencode/session-a / unassigned
- Completed: retry behavior implemented in src/chat.ts
- Verification: unit checks passed; desktop behavior not checked
- Remaining: verify retry behavior in the desktop client
- Blocker: no desktop session available
- Next action: launch the client and simulate one transient failure
- Relevant files: src/chat.ts, tests/chat.test.ts
```

A new agent checks the latest code and ownership before resuming, records the ownership change, and credits the previous implementation. The reviewer gets separate attribution.

## Concurrent work

Use separate task files and one existing coordinator for shared-board updates. Reread shared files before editing and preserve unrelated changes. A Markdown owner field cannot prevent simultaneous claims; use existing team coordination to resolve them. The skill does not create agents or a locking service.

## Keep context small

Keep active work and a short recent history in `STATUS.md`. Archive older completed entries only when they make the board difficult to use, and link the archive. Read only task records relevant to the current request. Do not paste conversations, credentials, or full command transcripts into the docs.
