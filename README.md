# claude-agent-crew

Five task-scoped subagents for Claude Code, each pinned to the model that
fits the job instead of running everything on one default model.

| Agent | Model | Use for |
|---|---|---|
| `architect` | Opus | System design, multi-file refactor planning, ambiguous tradeoffs |
| `bug-fixer` | Sonnet | Small, bounded bug fixes (1-2 files, clear root cause) |
| `code-reviewer` | Sonnet | Reviewing a PR/diff/file for correctness and simplification |
| `ticket-writer` | Haiku | Drafting tickets, issues, changelog entries, commit messages |
| `explorer` | Haiku | Read-only "where is X" / "what calls Y" codebase mapping |

## Install as a plugin

```
/plugin marketplace add AdarshaGS/claude-agent-crew
/plugin install agent-crew
```

## Or just copy the agents

```
git clone https://github.com/AdarshaGS/claude-agent-crew.git
cp claude-agent-crew/agents/*.md ~/.claude/agents/
```

Claude Code picks up any of these agents automatically — invoke with the
`Agent` tool and `subagent_type: "<name>"`, or just describe a matching task
("review this diff", "create a ticket for X") and Claude routes to it based
on each agent's `description`.

## Customizing

Each file in `agents/` is plain frontmatter + instructions:

```yaml
---
name: bug-fixer
description: ...
tools: Read, Edit, Grep, Glob, Bash
model: claude-sonnet-5
---
Instructions body...
```

Swap the `model:` line for whichever model fits your budget/quality tradeoff,
or narrow `tools:` to lock an agent down further.
