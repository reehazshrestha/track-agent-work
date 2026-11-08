# Track Agent Work

A portable coding-agent skill that keeps plans, current work, completed changes, verification, and agent ownership in your repository.

Use it when several coding agents share a project, when work spans sessions, or when you want a clear answer to “who did what, what is happening, and what comes next?” It also works with one agent.

## What it creates

```text
your-project/
├── AGENTS.md                   # Short instruction to maintain the work log
└── docs/
    ├── STATUS.md               # Compact shared board and recent changes
    ├── work/                   # Detailed task records, only when needed
    │   └── <task-id>.md
    └── archive/                # Older completed records, only when needed
```

Existing trackers are reused. Small tasks need only a row and a signed change entry; larger tasks get a linked record. The skill records actual agent identities, separates implementation from review, and never treats an unrun check as passed.

## Install

Clone or download this repository, then run the relevant commands **from its root**. These commands assume a POSIX shell. If a destination already exists, back it up or compare it before copying.

### Freebuff

Install for your user:

```sh
mkdir -p "$HOME/.claude/skills"
cp -R skills/track-agent-work "$HOME/.claude/skills/"
```

Restart Freebuff and invoke:

```text
/skill:track-agent-work
Set up work tracking for this project, then use it while implementing my task.
```

Freebuff's local skill loader supports `.claude/skills` and `.agents/skills`. Global loading depends on the host enabling home skills; if the command is missing in your version or host, use a project installation:

```sh
mkdir -p /path/to/project/.agents/skills
cp -R skills/track-agent-work /path/to/project/.agents/skills/
```

Then restart Freebuff in that project. See the [upstream loader](https://github.com/CodebuffAI/freebuff/blob/main/sdk/src/skills/load-skills.ts) and [Freebuff CLI guide](https://freebuff.com/perspectives/blog/solution-recommendation/freebuff-cli-the-terminal-coding-agent-that-includes-model-access-for-free).

### OpenCode

```sh
mkdir -p "$HOME/.config/opencode/skills"
cp -R skills/track-agent-work "$HOME/.config/opencode/skills/"
```

Restart OpenCode and use:

```text
@track-agent-work set up work tracking for this project
```

See [OpenCode skills](https://opencode.ai/docs/skills/).

### Claude Code

Install for your user (available across your projects):

```sh
mkdir -p "$HOME/.claude/skills"
cp -R skills/track-agent-work "$HOME/.claude/skills/"
```

This is the same location used by the Freebuff installation above; if you already installed it there, no second copy is needed.

Alternatively, install for one project:

```sh
mkdir -p /path/to/project/.claude/skills
cp -R skills/track-agent-work /path/to/project/.claude/skills/
```

Start Claude Code in your project and invoke:

```text
/track-agent-work set up work tracking for this project
```

For continued use, add a brief instruction in the project's `CLAUDE.md` to read `docs/STATUS.md` before coding and update plans, progress, checks, and agent attribution before reporting completion. Preserve existing instructions.

See the [official Claude Code skills documentation](https://code.claude.com/docs/en/skills).

### Codex

```sh
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/track-agent-work "${CODEX_HOME:-$HOME/.codex}/skills/"
```

Start a new session and invoke `$track-agent-work` with your task. These are installation instructions; this repository does not install itself into any agent.

### Other agents

Ask the agent to read `skills/track-agent-work/SKILL.md` and follow it. Keep the `assets/` folder alongside the file so template links resolve. Check your agent's own skill-discovery conventions before installing.

## Everyday use

```text
Use track-agent-work while fixing the chat retry bug. Record the plan first,
update progress at milestones, and record the checks and actual contributor.
```

For a resumed session:

```text
Read docs/STATUS.md and the linked chat-retry task. Check the code against
its recorded state, then continue from the next action.
```

For a handoff:

```text
Record what you completed, checks run, blockers, relevant files, and the next
executable action. Leave the next owner unassigned until someone takes over.
```

See the [workflow and worked example](docs/WORKFLOW.md).

## Design choices and limits

- One compact board is the entry point; detailed history stays in linked records.
- Tasks have stable IDs, explicit states, owners, and concrete next steps.
- Updates happen at milestones and completion, rather than after every command.
- Attribution records what agents actually did, with separate reviewer credit.
- Plans and checks are evidence-based; uncertainty stays visible.
- This is an instruction skill, not a background service, locking system, or enforcement hook. Agents must load and follow it. A short project `AGENTS.md` instruction helps future sessions discover the workflow, but support varies by agent.
- It does not spawn agents, grant permissions, or change release/deployment policy.

## Repository contents

| Path | Purpose |
| --- | --- |
| `skills/track-agent-work/SKILL.md` | Portable agent instructions |
| `skills/track-agent-work/assets/STATUS.md` | Shared board template |
| `skills/track-agent-work/assets/task.md` | Detailed task template |
| `docs/WORKFLOW.md` | Usage, example, and handoff conventions |
| `docs/STATUS.md` | This repository's own work record |
| `CONTRIBUTING.md` | Guidelines for improving the skill |

## Validation

The skill uses YAML frontmatter with a `name` and `description`, Markdown instructions, and relative links to templates. Validate using your agent's skill validator when available. Before publishing changes, check template links, preserve existing-project behavior, and walk through a small task and a handoff.

## Publishing and licensing

This folder is ready to become a GitHub repository. Create a repository in your account, then from this folder:

```sh
git init
git add .
git commit -m "Add agent work tracking skill and documentation"
git branch -M main
# Add the remote URL supplied by GitHub, then push:
# git remote add origin YOUR_REPOSITORY_URL
# git push -u origin main
```

Choose a license before publishing if you want to grant reuse rights. No license has been selected here. Review the files before pushing; no account name or remote URL is assumed.

The workflow was inspired by a project's shared status board; the included templates are generic and contain no private project history.
