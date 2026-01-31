---
name: jules-cli
description: "Use the Jules CLI (@google/jules) via exec to create and manage remote Jules coding sessions: login, list repos/sessions, start new sessions, monitor, and pull results. Use when the user asks to delegate coding tasks to Jules or manage Jules remote sessions from the terminal."
---

# Jules CLI (local via exec)

This skill uses the **Jules Tools CLI** locally via the `exec` tool.

## Prereqs (one-time)

### Install
Run (works on most Node setups):

```bash
npm install -g @google/jules
# or
pnpm add -g @google/jules
```

Verify:
```bash
jules version
```

### Login (interactive)
Jules requires Google auth:

```bash
jules login
```

This usually opens a browser window. If running on a headless server, you may need to:
- open the Control UI + browser tool, or
- run `jules login` on a machine with a browser.

Logout:
```bash
jules logout
```

## Core commands

### List
```bash
# connected repos
jules remote list --repo

# sessions
jules remote list --session
```

### Create a new session (automatic)
Use the current repo when possible:

```bash
# from inside a git repo
jules remote new --repo . --session "<task>"
```

Or specify a repo:
```bash
jules remote new --repo owner/name --session "<task>"
```

Parallel sessions:
```bash
jules remote new --repo . --session "<task>" --parallel 3
```

### Pull results
```bash
jules remote pull --session <id>
```

## Recommended Clawdbot workflow

1) Confirm `jules` exists; if not, install it.
2) Confirm logged in (if not, run `jules login` and ask user to complete auth).
3) Start session:
   - prefer `--repo .` if user’s task is about the current project
   - otherwise ask for `owner/repo`
4) Poll `jules remote list --session` to find the new session id
5) When complete, run `jules remote pull --session <id>`
6) Summarize what changed and ask whether to open a PR / run tests / etc.

## Safety / guardrails
- Always include the **exact task** string provided by the user.
- Prefer running in a clean git repo state (tell user if there are uncommitted changes).
- Avoid exposing secrets in session prompts.

