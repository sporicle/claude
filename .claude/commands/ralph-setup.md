---
description: "Setup Ralph workflow: interview, create spec, PRD, and prompt files"
argument-hint: "<description of what you want to build>"
allowed-tools: Read, Write, Edit, AskUserQuestion, Glob, Grep, Bash(mkdir:*)
---

# Ralph Setup Command

**IMPORTANT: This skill is SETUP ONLY. You must NEVER begin executing the Ralph loop or start working on user stories. Your job ends after creating all the setup files and presenting the summary. Do not research, implement, code, or take any action on the PRD stories. Just set up the workflow files and stop.**

You are setting up a complete Ralph workflow for autonomous iterative development. This involves creating several files that will guide an AI agent through implementing a project.

## Input

The user's initial description: $ARGUMENTS

## Your Task

### Step 1: Create Project Directory Structure

First, ensure we have a `.ralph/` directory in the current working directory:

```!
mkdir -p .ralph
```

### Step 2: Interview to Flesh Out Requirements

Using the user's initial description, conduct an in-depth interview to gather comprehensive requirements. Use the AskUserQuestion tool to explore:

**Core Functionality**
- What are the main features/user stories?
- What's the MVP scope vs nice-to-haves?
- What tech stack should be used?

**Technical Details**
- Database/storage requirements?
- API endpoints needed?
- Authentication/authorization requirements?
- External integrations?
- Performance requirements?

**UI/UX (if applicable)**
- Key screens/views?
- Design system or styling approach?
- Responsive requirements?
- Accessibility needs?

**Quality & Testing**
- What tests are required?
- Type checking requirements?
- Linting configuration?
- CI/CD considerations?

**Edge Cases & Constraints**
- Known limitations to accept?
- Error handling approach?
- Data validation requirements?

Ask questions one at a time. Be thorough but efficient - skip areas that clearly don't apply to this project. Follow up on interesting answers to get specifics.

### Step 3: Write RALPH-SPEC.md

After the interview is complete, write a comprehensive specification to `.ralph/RALPH-SPEC.md` that includes:

```markdown
# [Project Name] Specification

## Overview
[Brief description of what this project does]

## Tech Stack
- [List technologies, frameworks, libraries]

## Features

### [Feature 1]
[Detailed description with acceptance criteria]

### [Feature 2]
[...]

## Architecture
[High-level architecture decisions]

## Data Model
[If applicable - schemas, relationships]

## API Endpoints
[If applicable - routes, methods, payloads]

## UI/UX
[If applicable - screens, flows, design notes]

## Error Handling
[Strategy for handling errors]

## Testing Strategy
[What tests are needed and how to run them]

## Out of Scope
[What we're explicitly NOT building]

## Open Questions
[Any remaining uncertainties]

## Interview Notes
[Key decisions made during the interview]
```

### Step 4: Generate PRD (prd.json)

Convert the specification into a prioritized list of user stories. Write to `.ralph/prd.json`:

```json
[
  {
    "id": "US-001",
    "title": "[Short descriptive title]",
    "description": "As a [user type], I need [functionality] so that [benefit].",
    "acceptanceCriteria": [
      "Criterion 1",
      "Criterion 2",
      "..."
    ],
    "priority": 1,
    "passes": false,
    "notes": "",
    "tested": false
  }
]
```

**Prioritization Rules:**
1. Infrastructure/setup stories come first (project init, database setup, etc.)
2. Core functionality before enhancements
3. Dependencies must have lower priority numbers than dependent stories
4. Keep stories small and focused (ideally completable in one iteration)
5. Each story should be independently testable

**User Story Guidelines:**
- `id`: Format "US-XXX" with zero-padded numbers
- `title`: Imperative, action-oriented (e.g., "Setup SQLite database", "Add user authentication")
- `description`: Follow "As a... I need... so that..." format
- `acceptanceCriteria`: Specific, testable conditions
- `priority`: Integer starting at 1 (lower = higher priority)
- `passes`: Always start as `false`
- `notes`: Leave empty initially
- `tested`: Always start as `false`

### Step 5: Create RALPH-PROMPT.md

Write the Ralph loop prompt to `.ralph/RALPH-PROMPT.md`:

```markdown
# Ralph Implementation Loop

You are implementing a project following a PRD. Work through user stories one at a time.

## Workflow

1. **Read the PRD** at `.ralph/prd.json`
2. **Read progress log** at `.ralph/progress.txt` (check Codebase Patterns section first)
3. **Pick the highest priority** user story where `passes: false`
4. **Implement** that single user story
5. **Run quality checks** (typecheck, lint, test - use whatever the project requires)
6. **Update AGENTS.md** files if you discover reusable patterns
7. If checks pass, **commit ALL changes** with message: `feat: [Story ID] - [Story Title]`
8. **Update the PRD** to set `passes: true` for the completed story
9. **Append progress** to `.ralph/progress.txt`

## Progress Report Format

APPEND to `.ralph/progress.txt` (never replace, always append):

```
## [Date/Time] - [Story ID]
- What was implemented
- Files changed
- **Learnings for future iterations:**
  - Patterns discovered (e.g., "this codebase uses X for Y")
  - Gotchas encountered (e.g., "don't forget to update Z when changing W")
  - Useful context (e.g., "the evaluation panel is in component X")
---
```

The learnings section is critical - it helps future iterations avoid repeating mistakes.

## Codebase Patterns

If you discover a reusable pattern, add it to the `## Codebase Patterns` section at the TOP of `.ralph/progress.txt` (create it if it doesn't exist):

```
## Codebase Patterns
- Example: Use `sql<number>` template for aggregations
- Example: Always use `IF NOT EXISTS` for migrations
- Example: Export types from actions.ts for UI components
```

Only add patterns that are general and reusable, not story-specific details.

## Update AGENTS.md Files

Before committing, check if edited files have learnings worth preserving in nearby AGENTS.md files:

1. Identify directories with edited files
2. Check for existing AGENTS.md in those directories or parents
3. Add valuable learnings:
   - API patterns or conventions specific to that module
   - Gotchas or non-obvious requirements
   - Dependencies between files
   - Testing approaches for that area

Do NOT add story-specific details or temporary notes.

## Quality Requirements

- ALL commits must pass quality checks (typecheck, lint, test)
- Do NOT commit broken code
- Keep changes focused and minimal
- Follow existing code patterns

## Stop Condition

After completing a user story, check if ALL stories have `passes: true`.

- If **ALL complete**: Create SUMMARY.txt (see below), then reply with `COMPLETE`
- If **stories remain**: End normally (next iteration will continue)

## Final Summary (SUMMARY.txt)

When ALL user stories pass, create `.ralph/SUMMARY.txt` documenting everything that was built:

```markdown
# [Project Name] Implementation Summary

## Overview
[Brief description of what was implemented]

---

## Data Structures
[Document all structs, types, interfaces created - include code snippets]

## Constants
[List important constants with values and purposes]

---

## Methods/Functions Implemented

### [Category 1 - e.g., "On-Chain Instructions"]
[List each function with signature, purpose, and parameters]

### [Category 2 - e.g., "Frontend Utilities"]
[...]

---

## Error Handling
[List error codes/types added]

---

## Components/Modules Created
[List new files and their purposes]

---

## Usage

### [Use Case 1]
[Code example]

### [Use Case 2]
[Code example]

---

## Testing
[What's covered and how to run tests]

---

## Files Changed
[Complete list organized by directory]
```

This summary serves as documentation for anyone using or maintaining the implemented features.

## Important

- Work on ONE story per iteration
- Commit frequently
- Keep CI green
- Read Codebase Patterns before starting each iteration
```

### Step 6: Initialize progress.txt

Create an empty progress file at `.ralph/progress.txt`:

```markdown
## Codebase Patterns
(Add discovered patterns here as you work)

---

# Progress Log

```

### Step 7: Summary

After creating all files, provide a summary:

1. Confirm all files created:
   - `.ralph/RALPH-SPEC.md`
   - `.ralph/prd.json`
   - `.ralph/RALPH-PROMPT.md`
   - `.ralph/progress.txt`

2. Show the number of user stories created and their priorities

3. Explain how to start the Ralph loop:
   ```
   /ralph-loop ".ralph/RALPH-PROMPT.md" --max-iterations 30 --completion-promise "COMPLETE"
   ```

4. Note that when complete, a `.ralph/SUMMARY.txt` will be created documenting all implemented structures, methods, and usage

## Interview Style

- Be conversational but efficient
- Ask follow-up questions when answers reveal complexity
- Validate assumptions explicitly
- If the user seems unsure, offer concrete options
- Stop interviewing when you have enough detail to write clear user stories
