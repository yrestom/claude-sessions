Generate a detailed, step-by-step task list from an existing PRD in the current session directory. The task list guides developers through implementation with a two-phase approach.

## Prerequisites

1. **Check for active session**: Verify `.claude/claude_sessions/.current-session` exists
2. **Check for PRD**: Verify `[session-name]-prd.md` exists in current session directory
3. **Extract session name** from current session directory

## Task Generation Process

### Phase 1: PRD Analysis and Parent Tasks
1. **Read and analyze** the `[session-name]-prd.md` file
2. **Extract functional requirements**, user stories, and technical considerations
3. **Generate 5-7 high-level parent tasks** required to implement the feature
4. **Present parent tasks** to user in the specified format (without sub-tasks yet)
5. **Wait for confirmation**: "I have generated the high-level tasks based on the PRD. Ready to generate the sub-tasks? Respond with 'Go' to proceed."

### Phase 2: Detailed Sub-Task Generation
1. **Wait for user confirmation** (user responds with "Go")
2. **Break down each parent task** into smaller, actionable sub-tasks
3. **Ensure sub-tasks** logically follow from parent task and cover implementation details
4. **Identify relevant files** that will need to be created or modified
5. **Generate final structured output**

## Output Format

Save as `[session-name]-tasks.md` with this structure:

```markdown
# [Feature Name] - Development Tasks

## Relevant Files

- `path/to/file1.ts` - Brief description (e.g., Contains main component for this feature)
- `path/to/file1.test.ts` - Unit tests for file1.ts
- `path/to/another/file.tsx` - Brief description (e.g., API route handler for data submission)
- `path/to/another/file.test.tsx` - Unit tests for another/file.tsx
- `lib/utils/helpers.ts` - Brief description (e.g., Utility functions for calculations)
- `lib/utils/helpers.test.ts` - Unit tests for helpers.ts

### Notes

- Unit tests should be placed alongside code files they are testing
- Use appropriate test command for the project (e.g., `yarn test`, `npm test`, `pytest`)
- Running without a path executes all tests found by configuration

## Tasks

- [ ] 1.0 Parent Task Title
  - [ ] 1.1 [Sub-task description 1.1]
  - [ ] 1.2 [Sub-task description 1.2]
- [ ] 2.0 Parent Task Title
  - [ ] 2.1 [Sub-task description 2.1]
- [ ] 3.0 Parent Task Title (may not require sub-tasks if purely structural/configuration)

## Implementation Notes

- Each sub-task should be completable in 30-60 minutes
- Sub-tasks should include specific files to modify/create
- Consider dependencies between tasks and order accordingly
- Include testing and validation steps for each component
```

## Two-Phase Interaction Model

The process **explicitly requires a pause** after generating parent tasks to get user confirmation before proceeding to detailed sub-tasks. This ensures the high-level plan aligns with user expectations.

### Phase 1 Output Format
```markdown
## High-Level Tasks (Phase 1)

Based on the PRD analysis, here are the main tasks required:

- [ ] 1.0 [Parent Task 1 Title]
- [ ] 2.0 [Parent Task 2 Title] 
- [ ] 3.0 [Parent Task 3 Title]
- [ ] 4.0 [Parent Task 4 Title]
- [ ] 5.0 [Parent Task 5 Title]

Ready to generate detailed sub-tasks? Respond with 'Go' to proceed.
```

## File Updates

1. **Create** `[session-name]-tasks.md` with generated task list
2. **Update** `[session-name]-session.md` to reference the new tasks file
3. **Update** `[session-name]-progress.md` with task generation milestone

## Next Steps

After task generation, remind user they can:
- Execute tasks with `/project:session-execute-tasks`
- Review/edit tasks manually if needed
- Start implementation with controlled execution

## Target Audience

Task lists are written for **junior developers** who will implement the feature. Use clear, specific instructions with explicit file paths and technical details.