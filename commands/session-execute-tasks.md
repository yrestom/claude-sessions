Execute tasks from the current session's task list using a controlled, step-by-step approach with quality gates and user approval at each step.

## Prerequisites

1. **Check for active session**: Verify `.claude/claude_sessions/.current-session` exists
2. **Check for task list**: Verify `[session-name]-tasks.md` exists in current session directory
3. **Extract session name** from current session directory

## Task Execution Protocol

### Core Principles
- **One sub-task at a time**: Do NOT start the next sub-task until user gives permission
- **Quality gates**: Test → Stage → Clean → Commit after each parent task completion
- **Real-time tracking**: Update task status and progress files immediately

### Sub-Task Execution Process

1. **Before starting work**:
   - Check which sub-task is next in `[session-name]-tasks.md`
   - Analyze all related files and components deeply
   - Understand the functionality and process
   - Ask user for permission: "Ready to start [task description]? (y/n)"

2. **During implementation**:
   - Focus only on the current sub-task
   - Follow existing code patterns and conventions
   - Write clear, maintainable code
   - Add appropriate comments where needed

3. **After completing sub-task**:
   - Mark sub-task as completed: change `[ ]` to `[x]` in `[session-name]-tasks.md`
   - Update `[session-name]-progress.md` with what was accomplished
   - Ask user for permission to continue: "Sub-task completed. Continue to next? (y/n)"

### Parent Task Completion Protocol

When ALL sub-tasks under a parent task are marked `[x]`:

1. **Run full test suite**:
   - Execute appropriate test command for the project
   - Ensure all tests pass before proceeding
   - If tests fail, fix issues before continuing

2. **Stage changes** (only if tests pass):
   ```bash
   git add .
   ```

3. **Clean up**:
   - Remove any temporary files
   - Remove any temporary/debug code
   - Ensure code follows project conventions

4. **Commit with descriptive message**:
   Use conventional commit format with multiple `-m` flags:
   ```bash
   git commit -m "feat: add payment validation logic" -m "- Validates card type and expiry" -m "- Adds unit tests for edge cases" -m "Related to [parent-task-number] in [session-name]"
   ```

5. **Mark parent task complete**:
   - Change parent task `[ ]` to `[x]` in `[session-name]-tasks.md`
   - Update `[session-name]-progress.md` with parent task completion

### Task List Maintenance

Continuously update the task list file:
1. **Mark completed tasks**: Change `[ ]` to `[x]` immediately after completion
2. **Add new tasks**: If new tasks emerge during implementation, add them to the list
3. **Update relevant files**: Keep the "Relevant Files" section accurate and up-to-date
4. **Track progress**: Maintain real-time status in progress file

### File Updates During Execution

1. **`[session-name]-tasks.md`**:
   - Mark tasks as completed `[x]`
   - Add newly discovered tasks
   - Update relevant files section

2. **`[session-name]-progress.md`**:
   - Add timestamp entries for each sub-task completion
   - Record any issues encountered and solutions
   - Track git commits and file changes
   - Note any deviations from original plan

3. **`[session-name]-session.md`**:
   - Update overall progress summary
   - Add links to any new artifacts created

## Error Handling

If issues arise during execution:
1. **Document the problem** in `[session-name]-progress.md`
2. **Do not mark task as complete** until issue is resolved
3. **Create new task** if additional work is needed to resolve the issue
4. **Ask user** for guidance on how to proceed

## User Interaction Points

The AI must pause and wait for user approval at these points:
- Before starting each sub-task
- After completing each sub-task
- When encountering errors or blockers
- When new tasks are discovered that weren't in the original plan

## Quality Assurance

Before marking any parent task as complete:
- All sub-tasks must be `[x]`
- All tests must pass
- Code must follow project conventions
- No temporary/debug code remains
- Git commit must be clean and descriptive

## Session Integration

This command works seamlessly with other session commands:
- Progress updates automatically sync with `/project:session-update`
- Status visible via `/project:session-view-status`
- All artifacts preserved for `/project:session-end` summary