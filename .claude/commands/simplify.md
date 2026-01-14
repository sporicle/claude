---
description: Simplify recently modified code, then commit and push
allowed-tools: Task, Bash(git:*), Glob, Grep, Read, Edit, Write, TodoWrite
---

# Code Review and Simplify

## Context

- Current git status: !`git status --short`
- Current branch: !`git branch --show-current`

## Your Task

Perform the following steps in order:

### Step 1: Identify Recently Modified Files

Look at the git status output above to identify all modified and new files that contain code (ignore config files, markdown, etc. unless they have obvious issues).

### Step 2: Run Code Simplifier

Use the Task tool to launch the `code-simplifier:code-simplifier` agent with a prompt that includes:
- The list of recently modified files from git status
- Instructions to simplify and refine code for clarity, consistency, and maintainability
- Instructions to preserve all functionality
- Context about the project's tech stack if available from CLAUDE.md or similar

Wait for the agent to complete its work.

### Step 3: Verify Changes

After the code-simplifier completes:
- Run any available tests if there's a test command in package.json
- Run type checking if available (e.g., `npm run check` for SvelteKit projects)

If tests or type checking fail, fix the issues before proceeding.

### Step 4: Commit and Push

If the code-simplifier made changes and verification passed:
1. Stage all changes with `git add -A`
2. Create a commit with a descriptive message summarizing what was simplified
3. Push to the remote repository

If no changes were made by the code-simplifier, inform the user that no simplifications were needed.

## Important Notes

- Do NOT commit if tests fail
- Do NOT commit if there are type errors
- Include "Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>" in commit messages
- Use conventional commit format when appropriate
