List all development sessions from the directory-based session structure.

## Session Discovery Process

1. **Check directory existence**: Verify `.claude/claude_sessions/` directory exists
2. **Find session directories**: List all directories with format `YYYY-MM-DD-HHMM-*`
3. **Extract session information** from each directory:
   - Parse timestamp and session name from directory name
   - Read `[session-name]-session.md` for session details
   - Check for completion status and artifacts

## Display Format

### Session List Overview
```
📁 Development Sessions (Sorted by most recent):

🔍 Active Session (if any):
✨ 2025-07-20-1445-user-auth-system/
   📋 User Authentication System
   ⏱️  Started: July 20, 2025 at 2:45 PM (2h 30m ago)
   📊 Status: Implementation (67% complete)
   📝 8/12 tasks completed
   
📂 Recent Sessions:

📁 2025-07-20-1130-frontend-guide/
   📋 Complete Frontend Development Guide Generation
   ⏱️  Started: July 20, 2025 at 11:30 AM
   📊 Status: Completed
   ✅ Session ended successfully

📁 2025-07-19-0900-api-redesign/
   📋 API Architecture Redesign
   ⏱️  Started: July 19, 2025 at 9:00 AM  
   📊 Status: Paused (75% complete)
   ⚠️  Incomplete - 3/12 tasks remaining
```

## Session Information Extraction

For each session directory, extract:

### Basic Information
- **Directory name**: Parse timestamp and session name
- **Session title**: From first line of `[session-name]-session.md`
- **Start time**: From session overview section
- **Duration**: Calculate from start time to last update

### Status Assessment
- **Active**: If directory name matches `.current-session` contents
- **Completed**: If session has completion summary in session file
- **Paused**: If session has no recent activity (>24 hours)
- **Failed**: If session ended with error status

### Progress Indicators
- **Task completion**: If `[session-name]-tasks.md` exists, count completed tasks
- **Artifacts created**: Count files in `[session-name]-artifacts/` directory
- **Git activity**: Check for commits during session timeframe
- **Phase reached**: PRD → Tasks → Implementation → Completion

## Error Handling

### Missing or Corrupted Sessions
- **No session.md file**: Mark as "Corrupted - Missing session file"
- **Unreadable files**: Mark as "Corrupted - Cannot read session data"
- **Invalid directory format**: Skip non-conforming directories

### Empty Sessions Directory
```
📭 No development sessions found.

Create your first session with:
/project:session-start [session-description]
```

## Interactive Features

### Quick Actions
After displaying the list, suggest:
```
🚀 Quick Actions:
- Load a session: /project:session-load [session-name]
- Start new session: /project:session-start [description]
- View session details: /project:session-view-status
- Archive old sessions: /project:session-archive [session-name]
```

### Filtering Options
Support optional filtering:
- `--active`: Show only active sessions
- `--completed`: Show only completed sessions  
- `--recent [days]`: Show sessions from last N days
- `--search [keyword]`: Search session names and descriptions

## Display Priority

1. **Active session** (highlighted at top)
2. **Recent sessions** (last 7 days)
3. **Older sessions** (grouped by week/month)
4. **Archived sessions** (if any exist)

## Integration Notes

- Read from `.current-session` to identify active session
- Support both old `.md` files and new directory structure during transition
- Provide migration suggestions for old-format sessions
