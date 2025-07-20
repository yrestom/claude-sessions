Start a new development session by creating a structured session directory in `.claude/claude_sessions/` with the format `YYYY-MM-DD-HHMM-descriptive-session-name/`.

## Session Directory Structure

Create a session directory with a short, meaningful session name prefix for all files:

```
.claude/claude_sessions/YYYY-MM-DD-HHMM-user-auth-system/
├── user-auth-session.md          # Main session file 
├── user-auth-prd.md             # Product Requirements Document
├── user-auth-tasks.md           # Generated task list
├── user-auth-progress.md        # Real-time progress tracking
└── user-auth-artifacts/         # Additional files (designs, notes, etc.)
```

## Session Initialization Process

1. **Extract short session name** from $ARGUMENTS (e.g., "user authentication system" → "user-auth")
2. **Create session directory** with timestamp and session name
3. **Create [session-name]-session.md** with:
   - Session name and timestamp as title
   - Session overview section with start time
   - Goals section (ask user for goals if not clear)
   - Links to other session files when created
   - Empty progress section ready for updates

4. **Create [session-name]-progress.md** for real-time tracking
5. **Create [session-name]-artifacts/** directory
6. **Update `.current-session`** to track the active session directory name

7. **Ask user about PRD creation**: "Would you like to create a Product Requirements Document (PRD) for this session? This helps structure the development process with clear requirements and tasks."

## File Naming Convention

All files use the short session name as prefix:
- **[session-name]-session.md**: Main session overview and goals
- **[session-name]-prd.md**: Product Requirements Document  
- **[session-name]-tasks.md**: Structured task list with sub-tasks
- **[session-name]-progress.md**: Real-time updates and git changes
- **[session-name]-artifacts/**: Directory for related files

## User Options After Session Start

Remind the user they can:
- Create PRD with `/project:session-create-prd`
- Generate tasks with `/project:session-generate-tasks` 
- Execute tasks with `/project:session-execute-tasks`
- Update progress with `/project:session-update`
- View status with `/project:session-view-status`
- End session with `/project:session-end`
