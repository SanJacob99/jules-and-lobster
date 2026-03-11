# jules-and-lobster

A Claude Code skill for interacting with the **Jules REST API (v1alpha)** — Google's autonomous AI coding agent.

**Install:** [https://clawhub.ai/SanJacob99/jules-and-lobster](https://clawhub.ai/SanJacob99/jules-and-lobster) | **2,000+ installs**

## What it does

This skill lets you delegate coding tasks to Jules programmatically from within Claude Code. You can:

- Create coding sessions with specific prompts
- Monitor session state and activities in real-time
- Approve or review generated plans
- Send follow-up messages to active sessions
- Retrieve PR URLs and code changes from completed sessions

## Quick Start

```bash
# Set your API key (get one at https://jules.google.com/settings#api)
export JULES_API_KEY="your-api-key-here"

# Verify available sources
./scripts/jules_api.sh sources

# Create a session
./scripts/jules_api.sh new-session \
  --source "sources/github/OWNER/REPO" \
  --title "Add unit tests" \
  --prompt "Add comprehensive unit tests for the authentication module" \
  --branch main \
  --require-plan-approval \
  --auto-pr
```

## Requirements

- `curl` — used for all API requests
- `python3` — used for safe JSON string escaping
- `JULES_API_KEY` environment variable ([get one here](https://jules.google.com/settings#api))

## Documentation

See [SKILL.md](SKILL.md) for the full API reference, workflows, error handling, and best practices.
