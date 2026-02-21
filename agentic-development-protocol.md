# Agentic Development Protocol (Local-First)

## Environment & Auth
- You are a local agent with access to the Windows Terminal (PowerShell).
- **Authentication:** You are ALREADY authenticated via the GitHub CLI (`gh`). 
- If you get errors for not being authenticated, help the user authenticate with the right commands.
- Use `gh` commands directly for all GitHub interactions.

## WORKFLOW A: Task Creation (Idea Capture)
Use this flow when the user has a new idea or needs to document a requirement.
1. **Gather Info:** Ask for a title and a brief description if they aren't provided.
2. **Draft:** Propose labels (e.g., `todo`, `bug`, `feature`) but do not apply unless confirmed.
3. **Execute:** Run `gh issue create --title "<title>" --body "<body>"`.
4. **Confirm:** Report the new issue number and URL back to the user.

## WORKFLOW B: Task Execution (The Kanban Flow)
Use this flow when the user wants to implement an existing task.

### Phase 1: Task Discovery & Planning
1. **Discovery:** Run `gh issue list` to see current tasks.
2. **Details:** Use `gh issue view <id>` to get the full requirement.
3. **Brainstorm & Plan:** - Create a `PLAN.md` file locally with your proposed logic.
   - **SYNC TO GITHUB:** Run `gh issue comment <id> --body-file PLAN.md` so the brainstorm is saved to the ticket.
4. **Approval:** Wait for the user to say "LGTM" or "Proceed."

### Phase 2: Implementation Flow
1. **Context Sync:** Even if a local `PLAN.md` exists, check the GitHub issue comments (`gh issue view <id> --comments`) to ensure you have the latest approved design.
2. **Setup:** Update/Overwrite the local `PLAN.md` with the version found on the ticket to ensure local context is fresh.
3. **Branch:** Create and switch to a task-specific branch: `git checkout -b task/issue-<id>`.
4. **Code:** Implement the solution following the logic in `PLAN.md`. Follow project coding standards.
5. **Verify:** Run any existing local tests (npm test, pytest, etc.). Include framework check commands (e.g., `npm run check`, `cargo check`, `tsc`).

### Phase 3: Submission
1. **PR:** Use `gh pr create --fill` to open a pull request.
2. **Status:** Use `gh issue comment <id> --body "Implemented in PR."`.
3. **Close Issue:** If the user confirms, use `gh issue close <id>`.
