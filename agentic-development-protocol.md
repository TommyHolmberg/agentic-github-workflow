# Agentic Development Protocol (Local-First)

## ⚠️ Safety & Responsibility
- You are an assistant, not the owner of this repository.
- **No Destructive Actions:** Do not delete branches or repositories without confirmation.
- **Verification:** You must always wait for a "LGTM" or "Proceed" after posting a plan.

## Environment & Auth
- You are a local agent with access to the Windows Terminal (PowerShell).
- **Authentication:** You are ALREADY authenticated via the GitHub CLI (`gh`). 
- Use `gh` commands directly for all GitHub interactions.

## WORKFLOW A: Task Creation & Planning (Idea Capture)
Use this flow to document a new requirement and prepare it for the backlog.
1. **Gather Info:** Ask for a title and description.
2. **Create Issue:** Run `gh issue create --title "<title>" --body "<body>"`. Capture the new Issue URL.
3. **Brainstorm:** Immediately create a `PLAN.md` file locally with the proposed logic.
4. **Sync Plan:** Run `gh issue comment <id> --body-file PLAN.md`.
5. **Add to Project:** - Identify your project: `gh project list`
   - Add to Backlog: `gh project item-add <project-number> --url <new-issue-url> --owner "@me"`
6. **Confirm:** Report that the issue is created, planned, and sitting in the **Backlog**.

## WORKFLOW B: Task Execution (The Kanban Flow)
Use this flow when the user wants to implement an existing task.

### Phase 1: Discovery & Start
1. **Discovery:** Run `gh issue list` to see current tasks.
2. **Details & Context Sync:** - Run `gh issue view <id> --comments`. 
   - **CRITICAL:** If no `PLAN.md` content is found in the comments, you MUST execute a brainstorm now. Create a local `PLAN.md`, upload it via `gh issue comment <id> --body-file PLAN.md`, and wait for "LGTM" before moving to Phase 2.
   - If a plan exists, sync it to your local `PLAN.md`.
3. **Board Update:** Move to "In Progress":
   - Find Item ID: `gh project item-list <proj-id> --format json --jq ".items[] | select(.content.number == <issue-id>) | .id"`
   - Move: `gh project item-edit --project-id <proj-id> --id <item-id> --field-id "Status" --project-value "In Progress"`

### Phase 2: Implementation Flow
1. **Branch:** `git checkout -b task/issue-<id>`.
2. **Code:** Implement following the approved `PLAN.md`.
3. **Verify:** Run tests and framework checks (e.g., `npm run check`, `cargo check`).

### Phase 3: Submission
1. **PR & Review:** Open PR: `gh pr create --fill`.
2. **Board Update:** Move the board item to "Review" using the `item-edit` command from Phase 1.
3. **Close Issue:** If the user confirms, run `gh issue close <id>`.
