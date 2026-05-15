---
title: bea-rs
category: Projects
tags:
  - rust
  - cli
  - mcp
---

`bea-rs` (binary name `bea`, pronounced "bears" 🐻) is a file-based task tracker for developers
and AI coding agents. Tasks are plain Markdown files with YAML frontmatter stored in a
`.bears/` directory — no database, fully git-friendly, and equally usable from the terminal
or as an [MCP](https://modelcontextprotocol.io) server.

It was inspired by Steve Yegge's [Beads](https://github.com/steveyegge/beads) but reshaped to
fit my own workflow. Like [[aphid]], it's written in Rust.

# Why

Most task trackers live in a database or a SaaS product. That's awkward when an AI agent
needs to read and update tasks in the same repository it's working in. `bea-rs` keeps tasks
next to the code, version-controlled with the rest of the project, and exposes the same
operations to both a human at the terminal and an agent over MCP.

# Task format

Each task is a Markdown file at `.bears/{id}-{slug}.md`:

```markdown
---
id: a1b2
title: Implement OAuth flow
status: open
priority: P1
type: task
created: 2026-03-15T10:30:00Z
updated: 2026-03-15T10:30:00Z
tags: [backend, auth]
depends_on: [f4c9]
parent: x9k2
---

Any Markdown body goes here.
```

- **Statuses** — `open`, `in_progress`, `done`, `blocked`, `cancelled`
- **Types** — `task` (default) or `epic` (groups child tasks via `parent`)
- **Priorities** — `P0` (critical) through `P3` (low). A task inherits the highest priority
  of anything that depends on it, so a P3 blocking a P0 is treated as P0.

# CLI

```sh
bea init                                # create .bears/ and .bears.yml
bea create "Title" --priority P1 --tag backend
bea list                                # hides done/cancelled by default
bea ready                               # tasks with all dependencies satisfied
bea start <id>                          # → in_progress
bea done <id>                           # → done
bea dep add <id> <depends-on-id>        # cycle-safe
bea graph                               # dependency tree
bea search "oauth"
bea edit <id>                           # open in $EDITOR
```

Every command also accepts `--json` for machine-readable output.

# MCP server

`bea mcp` exposes the same operations as MCP tools over stdio, so AI coding agents can list
ready work, create tasks, update statuses, manage dependencies, and search — without needing
to learn the file format. Register it with Claude Code via `claude mcp add`:

```json
{
  "mcpServers": {
    "bears": {
      "command": "bea",
      "args": ["mcp"]
    }
  }
}
```

# Install

```sh
cargo install bea-rs
```

Or grab a pre-built binary:

```sh
curl -fsSL https://raw.githubusercontent.com/LHelge/bea-rs/main/install.sh | sh
```

# Links

- [Source code](https://github.com/LHelge/bea-rs)
- [crates.io](https://crates.io/crates/bea-rs)
