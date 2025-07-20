Create a Product Requirements Document (PRD) for the current active session using an interactive process with clarifying questions.

## Prerequisites

1. **Check for active session**: Verify `.claude/claude_sessions/.current-session` exists
2. **If no active session**: Inform user to start one with `/project:session-start`
3. **Extract session name** from current session directory name

## PRD Creation Process

### Phase 1: Initial Analysis
1. **Read initial prompt** from user or session goals
2. **Extract session short name** from current session directory (e.g., "user-auth" from "2025-07-20-1445-user-auth-system")

### Phase 2: Interactive Clarification
**Ask clarifying questions** to gather sufficient detail. Focus on understanding the "what" and "why" of the feature. Provide options in letter/number lists for easy responses.

**Common clarification areas:**
- **Problem/Goal**: "What problem does this feature solve for the user?"
- **Target User**: "Who is the primary user of this feature?"
- **Core Functionality**: "Can you describe the key actions a user should be able to perform?"
- **User Stories**: "Could you provide user stories? (As a [user type], I want to [action] so that [benefit])"
- **Acceptance Criteria**: "How will we know when this feature is successfully implemented?"
- **Scope/Boundaries**: "What should this feature NOT do (non-goals)?"
- **Data Requirements**: "What kind of data does this feature need to display or manipulate?"
- **Design/UI**: "Are there any existing design mockups or UI guidelines to follow?"
- **Edge Cases**: "Any potential edge cases or error conditions to consider?"

### Phase 3: PRD Generation
Generate PRD using this structure and save as `[session-name]-prd.md`:

```markdown
# [Feature Name] - Product Requirements Document

## Introduction/Overview
Brief description of the feature and the problem it solves. State the main goal.

## Goals
List specific, measurable objectives for this feature.

## User Stories
Detail user narratives describing feature usage and benefits.

## Functional Requirements
List specific functionalities the feature must have. Use clear, concise language. Number these requirements.

## Non-Goals (Out of Scope)
Clearly state what this feature will NOT include to manage scope.

## Design Considerations (Optional)
Link to mockups, describe UI/UX requirements, or mention relevant components/styles if applicable.

## Technical Considerations (Optional)
Mention any known technical constraints, dependencies, or suggestions.

## Success Metrics
How will the success of this feature be measured?

## Open Questions
List any remaining questions or areas needing further clarification.
```

## Output Location
- **File**: `[session-name]-prd.md` in current session directory
- **Update**: Add reference to PRD in `[session-name]-session.md`

## Next Steps
After PRD creation, remind user they can:
- Generate tasks with `/project:session-generate-tasks`
- Review/edit the PRD manually if needed
- Start implementation planning

## Target Audience
Write the PRD for a **junior developer** - be explicit, unambiguous, and avoid jargon where possible.