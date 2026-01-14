---
description: Interview about a spec file to gather detailed requirements
argument-hint: <path to spec file>
allowed-tools: Read, Write, Edit, AskUserQuestion, Glob, Grep
---

# Spec Interview

You are conducting an in-depth interview about a specification file to uncover hidden requirements, edge cases, and potential issues before implementation begins.

## Your Task

1. **Read the spec file**: $ARGUMENTS

2. **Conduct a thorough interview** using the AskUserQuestion tool. Ask about:

### Technical Implementation
- Unclear data flows or state management
- Missing error states or edge cases
- Performance implications of design choices
- Security considerations not explicitly mentioned
- Integration points with existing systems
- Concurrency or race condition scenarios
- Data validation and sanitization requirements
- Caching strategies and invalidation

### Architecture & Design
- Why certain patterns were chosen over alternatives
- Scalability concerns as usage grows
- Dependencies and their failure modes
- Testing strategies for complex scenarios
- Migration paths if requirements change
- Backwards compatibility requirements

### UI/UX
- Loading states and skeleton screens
- Empty states and first-time user experience
- Error recovery flows for users
- Accessibility requirements
- Responsive behavior across devices
- Offline or degraded network behavior
- Undo/redo capabilities
- Confirmation dialogs for destructive actions

### Business Logic
- Edge cases in calculations or state transitions
- Time-based logic (timezones, daylight saving)
- Limits, quotas, or rate limiting
- Audit logging requirements
- Data retention and cleanup policies

### Tradeoffs & Concerns
- Known limitations the user is accepting
- Technical debt being introduced intentionally
- Features explicitly out of scope
- Assumptions that could break

## Interview Rules

1. **Ask non-obvious questions** - Don't ask things that are clearly answered in the spec
2. **Be specific** - Reference exact parts of the spec when asking for clarification
3. **Go deep** - Follow up on answers to uncover more details
4. **Challenge assumptions** - Ask "what if" scenarios
5. **One topic at a time** - Use focused questions, not multi-part questions
6. **Continue until complete** - Keep interviewing until all ambiguities are resolved

## Interview Flow

1. Read and analyze the spec thoroughly
2. Identify gaps, ambiguities, and unstated assumptions
3. Prioritize questions by impact on implementation
4. Ask questions one at a time using AskUserQuestion
5. Incorporate answers and ask follow-up questions
6. When satisfied, update the spec file with all gathered details
7. Inform the user the interview is complete

## Output

After the interview is complete:
1. Update the original spec file with all new information gathered
2. Add any new sections needed (edge cases, error handling, etc.)
3. Mark resolved ambiguities inline
4. Add a "Clarifications" or "Interview Notes" section if appropriate
