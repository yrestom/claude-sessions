Update the current development session with comprehensive progress tracking across all session files.

## Prerequisites

1. **Check for active session**: Verify `.claude/claude_sessions/.current-session` exists
2. **If no active session**: Inform user to start one with `/project:session-start`
3. **Extract session name** from current session directory

## Update Process

### 1. Append to `[session-name]-progress.md`

Add timestamped update with:
- **Current timestamp**
- **The update**: $ARGUMENTS (or summarize recent activities if no arguments)
- **Git status summary**:
  - Files added/modified/deleted (from `git status --porcelain`)
  - Current branch and last commit
  - Recent commits since last update
- **Session task progress** (if tasks exist):
  - Read `[session-name]-tasks.md` to analyze task completion
  - Count completed/in-progress/pending tasks
  - List recently completed tasks
  - Identify current active task
- **Issues encountered** and solutions implemented
- **Code changes made** with brief descriptions

### 2. Update `[session-name]-session.md`

Update the progress section with:
- Latest milestone achieved
- Current phase (PRD, Tasks, Implementation, etc.)
- Overall completion percentage
- Links to newly created artifacts

### 3. Session Integration

If session files exist, include:
- **PRD status**: If `[session-name]-prd.md` exists, note any requirements changes
- **Task status**: If `[session-name]-tasks.md` exists, provide task completion summary  
- **Artifacts**: List any new files in `[session-name]-artifacts/` directory

## Update Format

### Progress File Entry (`[session-name]-progress.md`)

```markdown
### Update - 2025-07-20 14:45

**Summary**: [User's update or automatic summary]

**Git Changes**:
- Modified: app/middleware.ts, lib/auth.ts
- Added: app/login/page.tsx
- Deleted: temp/old-auth.js
- Current branch: feature/user-auth (commit: abc123f)
- Recent commits: 2 commits since last update

**Task Progress**: 
- Total: 12 tasks (8 completed, 1 in progress, 3 pending)
- Recently completed:
  - ✓ 1.2 Set up auth middleware
  - ✓ 1.3 Create login page component
  - ✓ 2.1 Add logout functionality
- Currently working on: 2.2 Implement session management

**Session Status**:
- Current phase: Implementation (Task Execution)
- Overall progress: 67% complete
- PRD: ✓ Completed
- Tasks: ✓ Generated (12 tasks)
- Implementation: 🔄 In progress

**Issues Encountered**: 
- TypeScript type conflicts in auth middleware
- Solution: Updated interface definitions in types/auth.ts

**Details**: [Additional context from user or discovered during work]
```

### Session File Update (`[session-name]-session.md`)

Update the progress section:
```markdown
## Progress

- ✅ **Session Started**: 2025-07-20 14:00
- ✅ **PRD Created**: 2025-07-20 14:15 - [user-auth-prd.md]
- ✅ **Tasks Generated**: 2025-07-20 14:30 - [user-auth-tasks.md] (12 tasks)
- 🔄 **Implementation**: 8/12 tasks completed (67%)
- ⏸️ **Testing**: Pending
- ⏸️ **Deployment**: Pending

**Current Focus**: Implementing session management (Task 2.2)
**Last Update**: 2025-07-20 14:45
```

## Automatic Tracking

The update process should automatically:
1. **Detect task completions** by comparing current vs. previous task list state
2. **Track file changes** using git status and diff commands
3. **Monitor session artifacts** for new files or modifications
4. **Calculate progress metrics** based on task completion rates

## Integration with Other Commands

This update mechanism integrates with:
- `/project:session-execute-tasks` - Automatic updates during task execution
- `/project:session-view-status` - Real-time status queries
- `/project:session-end` - Comprehensive final summary
