# Task 3: Documentation — Tenx MCP Setup & Rules Configuration

This document records the work done for the Tenx MCP assessment: setup (Task 1), rules configuration (Task 2), and documentation (Task 3). It is the **report of activity** as per the Documentation guide, including what was tried and how issues were troubleshooted (especially relevant if MCP connection had issues).

---

## What you did

### Task 1: Setup

- **IDE chosen:** Cursor.
- **Configuration added:**
  - **`.cursor/mcp.json`** — MCP server config for `tenxfeedbackanalytics`:
    - URL: `https://mcppulse.10academy.org/proxy`
    - Headers: `X-Device: "windows"`, `X-Coding-Tool: "cursor"`
  - **`.cursor/rules/`** — Created the rules directory.
  - **`.cursor/rules/agent.mdc`** — Initial version with a single line instructing the agent to use Tenx MCP when available.
- **Verification:** The Tenx MCP server was enabled in Cursor, connected (green indicator), and tools (e.g. `list_managed_servers`, `log_passage_time_trigger`, `log_performance_outlier_trigger`, `tool_usage_guideline_prompt`) were visible and available.

### Task 2: Research & rules file changes

Research drew on:

- **Boris Cherny's workflow (X thread):** Shared rules file in git; team adds mistakes to the rules so the agent "knows not to do it next time"; start complex work in Plan mode then implement; re-plan when things go wrong; "give the agent a way to verify its work" (tests, commands, browser); use MCP and tools.
- **Cursor docs (Rules):** Rules are system-level instructions; keep them focused, actionable, and scoped; under ~500 lines; when the agent makes a mistake, update the rule; check rules into git.
- **Community practice:** One concern per rule; document recurring mistakes; refine based on usage; use frontmatter (`description`, `alwaysApply`) to control when rules apply.

**Changes made to `.cursor/rules/agent.mdc`:**

1. **Frontmatter**
   - `description`: Short summary of the rule's purpose.
   - `alwaysApply: true`: Rule applies to every Agent (chat) session.

2. **Section 1 — Plan before implementing**
   - For non-trivial work: propose or agree on a short plan before making many edits; use Plan mode if the user prefers it.
   - If something goes wrong: re-plan instead of iterating blindly.
   - Include verification steps in the plan (e.g. run tests, run a command, check output).

3. **Section 2 — Verify your work**
   - After code/config changes: run tests, linter, build, or suggest a concrete manual check.
   - Prefer existing tests/scripts; report pass/fail and fix or escalate on failure.

4. **Section 3 — Tenx MCP**
   - Use `tenxfeedbackanalytics` when available and relevant; do not block the user if the MCP is unavailable.

5. **Section 4 — Learning from corrections**
   - Treat user corrections as important feedback; avoid repeating the same mistake in the same session.
   - If the user asks to "add to the rules" or "remember this," offer to update `.cursor/rules/` (e.g. `agent.mdc`) with clear, actionable text.

6. **Section 5 — General behavior**
   - Be concrete (specific instructions, paths, commands).
   - Prefer referencing files over pasting large blocks into rules.
   - Use MCP and other tools when they help; stay focused and prefer small, clear steps.

7. **Closing note**
   - Reminder that the file is maintained over time and that "do"/"don't" items can be added as mistakes or patterns are noticed.

---

## What worked

- **Tenx MCP connection:** Using the exact URL and headers from the Tenx MCP documentation (with `X-Device: "windows"` for this machine) allowed the server to connect and list tools without issues.
- **Single, always-on agent rule:** Putting workflow, verification, Tenx, and "learning from corrections" in one `agent.mdc` with `alwaysApply: true` meant the agent consistently received the same guidance in every chat, without having to remember to @-mention a rule.
- **Plan-first and verify:** Writing explicit "plan before implementing" and "verify your work" instructions aligned the agent with the research (Boris Cherny, Cursor docs) and made it more likely to propose steps and run checks after changes.
- **Concrete, short rules:** Keeping the rule file under ~500 lines, avoiding vague advice, and preferring "reference files instead of copying" kept the rule readable and easier to maintain.
- **Tenx as optional:** Stating that the agent should use Tenx when available but not block if it's unavailable avoided failures or long waits when the MCP was off or unreachable.

---

## What didn't work (and how it was addressed)

- **Initial rule too minimal:** The first version of `agent.mdc` only said "use Tenx MCP when available." The agent had no guidance on planning, verification, or learning from corrections. **Fix:** Expanded the file using the research (Boris Cherny's thread, Cursor docs, community practices) into the five sections above.
- **Unclear where MCP config lives:** Cursor can use user-level or project-level `.cursor`; the instructions said "within your working directory." For a user working from the home directory, placing `mcp.json` under `C:\Users\hp\.cursor\` worked. **Note:** If you use a specific project folder as the "working directory," you may need a project-level `.cursor/mcp.json` there as well; the same config can be copied.
- **No prior use of Plan mode:** The rules ask the agent to "propose or agree on a plan" and to "use Plan mode if the user prefers it." If you don't use Plan mode yet, behavior may still be good from the "propose a short plan" part alone; you can adopt Plan mode (e.g. Shift+Tab in the agent input) later for larger tasks.
- **Verification depends on project:** "Run tests/linter/build" only helps if the project has them. The rule also asks the agent to "suggest a concrete verification step" when no automation exists, which keeps verification possible even in minimal projects.

**Troubleshooting approach (if MCP or rules had failed):** Check Cursor version, confirm `mcp.json` path and JSON syntax, ensure `X-Device` matches your OS (`mac` / `linux` / `windows`), enable the server in Cursor Settings → MCP and use Connect to authenticate with GitHub. For rules: ensure file is in `.cursor/rules/` with `.mdc` extension and valid frontmatter; reload or restart Cursor.

---

## Insights gained

- **Rules are persistent context:** The agent does not remember past chats. Rules files (e.g. `agent.mdc`) are loaded as context at the start of a session. So what you put in the rules directly shapes how the agent behaves: planning, verifying, using Tenx, and responding to corrections.
- **Rules align behavior with your intent:** By encoding "plan first," "verify after changes," and "learn from corrections," the rules nudge the agent toward your preferred workflow (think then act, check then ship, improve over time). Without these instructions, the agent might skip planning or verification, or ignore repeated corrections.
- **Documenting mistakes improves future runs:** Boris Cherny's approach—adding mistakes to a shared rules file so the agent "knows not to do it next time"—translates well to `agent.mdc`. When you add a "don't do X" or "always do Y" after the agent gets something wrong, that guidance is present in the next session and reduces the same error.
- **Verification as a rule multiplies quality:** Making "verify your work" an explicit rule pushes the agent to run tests or suggest checks instead of assuming the change is correct. That matches the insight that giving the agent a feedback loop (tests, commands, manual steps) significantly improves output quality.
- **One rules file can be enough to start:** You can grow into multiple rule files (e.g. by concern or by file pattern) later. Starting with a single, well-structured `agent.mdc` that's updated when you see repeated mistakes or new patterns is a practical way to align the agent with your thought process and expectations without over-optimizing early.

---

## Summary

| Task   | Outcome |
|--------|---------|
| **Task 1** | Tenx MCP configured in Cursor (`mcp.json`), connected and active; `.cursor/rules/agent.mdc` created. |
| **Task 2** | `agent.mdc` improved using Boris Cherny's workflow, Cursor docs, and best practices: plan-first, verify work, Tenx MCP, learn from corrections, general behavior. |
| **Task 3** | This document: what you did, what worked, what didn't and how you fixed it, and how rules change the agent's behavior to match your intent and expectations. |

The Tenx MCP connection was kept active throughout the assessment so that interactions with the coding agent could be logged.
