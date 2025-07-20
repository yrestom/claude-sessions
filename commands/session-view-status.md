Display a comprehensive overview of the current active session including progress, task status, git changes, and artifacts.

## Prerequisites

1. **Check for active session**: Verify `.claude/claude_sessions/.current-session` exists
2. **If no active session**: Inform user "No active session. Start one with `/project:session-start`"
3. **Extract session name** from current session directory

## Status Display Process

### 1. Session Header Information

Display basic session info:
```
🎯 Active Session: [session-name]
📁 Directory: .claude/claude_sessions/[full-session-directory-name]/
⏱️  Started: [start-time from session file]
⏱️  Duration: [calculated duration]
```

### 2. Session Phase Status

Analyze which files exist and show current phase:
```
📋 Session Progress:
- ✅ Session Started
- [✅/❌] PRD Created ([session-name]-prd.md)
- [✅/❌] Tasks Generated ([session-name]-tasks.md) 
- [🔄/✅/❌] Implementation ([task completion %])
- [⏸️/✅] Testing
- [⏸️/✅] Deployment Ready
```

### 3. Task Progress (if tasks exist)

Read `[session-name]-tasks.md` and display:
```
✅ Task Progress:
- Total Tasks: [X] ([Y] parent tasks, [Z] sub-tasks)
- Completed: [X] ([completion %])
- In Progress: [X] 
- Pending: [X]

📝 Current Focus:
- Working on: [current task description]
- Next up: [next pending task]
```

### 4. Git Status Summary

Run git commands and show:
```
📂 Git Status:
- Current Branch: [branch-name]
- Uncommitted Changes: [X] files
  - Modified: [list of modified files]
  - Added: [list of new files] 
  - Deleted: [list of deleted files]
- Recent Commits: [X] commits since session start
- Last Commit: [commit-hash] - [commit-message]
```

### 5. Session Artifacts

List files in session directory:
```
📦 Session Artifacts:
- Session Overview: [session-name]-session.md
- [✅/❌] PRD Document: [session-name]-prd.md
- [✅/❌] Task List: [session-name]-tasks.md  
- Progress Log: [session-name]-progress.md ([X] updates)
- Additional Files:
  - [session-name]-artifacts/ ([X] files)
    - [list artifact files if any]
```

### 6. Recent Activity

Show last few entries from `[session-name]-progress.md`:
```
📈 Recent Activity:
- [timestamp]: [latest update summary]
- [timestamp]: [previous update summary]
- [timestamp]: [previous update summary]
```

### 7. Next Actions

Based on current state, suggest next steps:
```
🚀 Suggested Next Actions:
- [If no PRD]: Create PRD with `/project:session-create-prd`
- [If PRD but no tasks]: Generate tasks with `/project:session-generate-tasks`
- [If tasks exist]: Continue implementation with `/project:session-execute-tasks`
- [If implementation done]: Run tests and prepare for completion
- Update progress with `/project:session-update [message]`
```

## Status Output Format

### Compact View (Default)
```
🎯 Session: user-auth-system (2h 30m active)
📋 Phase: Implementation (67% complete)
✅ Tasks: 8/12 completed | 🔄 Working on: Session management
📂 Git: feature/user-auth | 3 modified files | 2 commits
🚀 Next: Continue with task 2.3 - Implement password reset
```

### Detailed View (with -v flag or detailed argument)
Show all sections above in full detail.

## Integration with Session Files

This command reads from:
- `[session-name]-session.md` - For session start time and goals
- `[session-name]-prd.md` - For requirements status
- `[session-name]-tasks.md` - For task completion analysis
- `[session-name]-progress.md` - For recent activity
- `[session-name]-artifacts/` - For additional files
- Git status and log - For repository state

## Error Handling

- **No active session**: Clear message with suggestion to start one
- **Corrupted session files**: Report which files are missing/corrupted
- **Git issues**: Handle cases where git is not available or repo is not initialized
- **Permission issues**: Handle cases where session files can't be read

## Performance Considerations

- **Cache git information** to avoid repeated git calls
- **Read only necessary file portions** for status overview
- **Lazy load detailed information** only when requested
- **Handle large progress files** by reading only recent entries

## User Experience

- **Color coding**: Use emojis and formatting for visual clarity
- **Progressive disclosure**: Start with summary, allow drilling down
- **Action-oriented**: Always suggest next steps
- **Context-aware**: Adapt suggestions based on current state