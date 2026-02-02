# Tenx MCP Setup — Assessment Submission

**10 Academy MCP Setup Challenge** — Configure your coding environment with MCP tools, rules, and documentation.

- **IDE used:** Cursor  
- **Tenx MCP:** Connected and active (`tenxfeedbackanalytics`)

---

## What’s in this repository

| Artifact | Description |
|----------|-------------|
| **[agent.mdc](agent.mdc)** | Final Cursor rules file (`.cursor/rules/agent.mdc`) — plan-first, verify work, Tenx MCP, learn from corrections. |
| **[docs/DOCUMENTATION.md](docs/DOCUMENTATION.md)** | Task 3 report: What you did, What worked, What didn’t work, Insights gained. |
| **[docs/mcp-config-example.json](docs/mcp-config-example.json)** | Example MCP config used for Tenx (Cursor: `.cursor/mcp.json`). |
| **[SUBMISSION.md](SUBMISSION.md)** | How to submit: create public GitHub repo, push this folder, submit repo link. |
| **README.md** | This file — overview and how to use the artifacts. |

---

## How to use the rules in Cursor

1. Copy the rules file into your Cursor rules directory:
   - **Windows:** `%USERPROFILE%\.cursor\rules\agent.mdc`
   - Or in a project: `<your-project>\.cursor\rules\agent.mdc`
2. Replace or merge with your existing `agent.mdc`.
3. Reload Cursor (or restart) so the rule is applied. The rule uses `alwaysApply: true`.

---

## Tasks completed

- **Task 1: Setup** — Tenx MCP configured in Cursor; server connected; tools available.
- **Task 2: Research & Configure** — Rules file updated using Boris Cherny’s workflow, Cursor docs, and community best practices.
- **Task 3: Documentation** — Report in `docs/DOCUMENTATION.md` with what you did, what worked, what didn’t, and insights gained.

---

## Tenx MCP connection

The Tenx MCP connection was active throughout the assessment so that interactions with the coding agent could be logged. Configuration used:

- **URL:** `https://mcppulse.10academy.org/proxy`
- **Headers:** `X-Device: "windows"`, `X-Coding-Tool: "cursor"`
- **Server name in Cursor:** `tenxfeedbackanalytics`

---

*Submission for 10 Academy MCP Setup Challenge.*
