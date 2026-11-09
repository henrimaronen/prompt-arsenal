---
name: to-linear-issues
description: Break a plan, spec, or PRD into independently-grabbable Linear issues using tracer-bullet vertical slices. Use when user wants to convert a plan into Linear issues, create implementation tickets, or break down work into Linear issues.
---

# To Linear Issues

Break a plan into independently-grabbable Linear issues using vertical slices (tracer bullets).

## Process

### 1. Gather context

Work from whatever is already in the conversation context. If the user passes a Linear issue ID (e.g. `ENG-123`) as an argument, fetch it with `mcp__claude_ai_Linear__get_issue` (with `includeRelations: true`).

### 2. Resolve team and project

Before creating issues, determine:

- **Team**: Ask the user which Linear team to file issues under, or call `mcp__claude_ai_Linear__list_teams` to show available teams and let the user pick.
- **Project** (optional): Ask whether the issues should be linked to a project, or call `mcp__claude_ai_Linear__list_projects` filtered by team to show options.

### 3. Explore the codebase (optional)

If you have not already explored the codebase, do so to understand the current state of the code.

### 4. Draft vertical slices

Break the plan into **tracer bullet** issues. Each issue is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer.

Slices may be 'HITL' or 'AFK'. HITL slices require human interaction, such as an architectural decision or a design review. AFK slices can be implemented and merged without human interaction. Prefer AFK over HITL where possible.

<vertical-slice-rules>
- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests)
- A completed slice is demoable or verifiable on its own
- Prefer many thin slices over few thick ones
</vertical-slice-rules>

### 5. Quiz the user

Present the proposed breakdown as a numbered list. For each slice, show:

- **Title**: short descriptive name
- **Type**: HITL / AFK
- **Blocked by**: which other slices (if any) must complete first
- **User stories covered**: which user stories this addresses (if the source material has them)

Ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the dependency relationships correct?
- Should any slices be merged or split further?
- Are the correct slices marked as HITL and AFK?

Iterate until the user approves the breakdown.

### 6. Create the Linear issues

For each approved slice, create a Linear issue using `mcp__claude_ai_Linear__save_issue`.

Create issues in dependency order (blockers first) so you can reference real issue identifiers (e.g. `ENG-42`) in the `blockedBy` field of later issues.

For each issue, pass:

- `title`: concise slice title
- `team`: the resolved team name or ID
- `project`: the resolved project name or ID (if chosen)
- `description`: use the issue body template below (Markdown, literal newlines — no `\n` escape sequences)
- `blockedBy`: array of identifiers for blocking issues (e.g. `["ENG-42"]`), omit if none
- `parentId`: the source issue identifier if the input was a Linear issue, otherwise omit

<issue-template>
## What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation.

## Acceptance criteria

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Blocked by

- Blocked by <issue-identifier> (if any)

Or "None - can start immediately" if no blockers.
</issue-template>

Do NOT close or modify any parent issue.
