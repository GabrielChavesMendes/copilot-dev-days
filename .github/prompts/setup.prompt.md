---
agent: agent
description: Get my development workspace ready
tools: ['execute/runTask', 'execute/runInTerminal', 'read', 'search', 'todo']
---

Your goal is to prepare and verify the workspace for local development.

## Mandatory development checklist
- [ ] lint with `uv run ruff check .`
- [ ] build/sync dependencies with `uv sync`
- [ ] run tests with `uv run pytest`
- [ ] start dev server with `uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000`
- [ ] open the site in a real browser: `$BROWSER http://localhost:8000`

## Important
- Do NOT use VS Code Simple Browser to preview the app; HTMX needs a full browser.
- Use `$BROWSER http://localhost:8000` from the terminal to open the site.