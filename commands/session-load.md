Load an existing development session by switching to a session directory and updating the current session pointer.

## Session Loading Process

### 1. Session Resolution

Take the input argument `$ARGUMENT` and resolve the session directory:

**Direct directory name match:**
- Check if directory exists: `.claude/claude_sessions/$ARGUMENT/`
- Example: `user-auth-system` → `.claude/claude_sessions/2025-07-20-1445-user-auth-system/`

**Flexible matching patterns:**
- **Full directory name**: `2025-07-20-1445-user-auth-system`
- **Session name only**: `user-auth-system` (find latest matching session)
- **Partial timestamp**: `2025-07-20` (list sessions from that date)
- **Short name**: `user-auth` (find best match)

### 2. Session Discovery

If exact match not found, perform intelligent search:

1. **Search by session name**: Find directories ending with `-$ARGUMENT`
2. **Search by partial match**: Find directories containing `$ARGUMENT`
3. **Search by date**: If argument looks like date, find sessions from that day
4. **Fuzzy search**: Find closest matching session names

### 3. Session Validation

Before loading, verify session integrity:

```markdown
✅ Session Validation:
- Directory exists: ✅ .claude/claude_sessions/2025-07-20-1445-user-auth-system/
- Session file exists: ✅ user-auth-session.md
- Session readable: ✅ Valid session format
- Session status: 🔄 Implementation (67% complete)
```

### 4. Multiple Matches Handling

If multiple sessions match the argument:

```markdown
🔍 Multiple sessions found for "user-auth":

1. 2025-07-20-1445-user-auth-system/        (Active - 67% complete)
   📋 User Authentication System Implementation
   
2. 2025-07-18-0900-user-auth-refactor/      (Completed)
   📋 User Authentication Code Refactoring
   
3. 2025-07-15-1400-user-auth-testing/       (Paused - 90% complete)
   📋 User Authentication Testing Suite

Please specify which session to load:
- `/project:session-load user-auth-system`
- `/project:session-load user-auth-refactor` 
- `/project:session-load user-auth-testing`
```

### 5. Session Not Found

If no matching sessions found:

```markdown
❌ Session not found: "$ARGUMENT"

📁 Available sessions:
- user-auth-system     (Active - Implementation phase)
- frontend-guide       (Completed)
- api-redesign         (Paused - 75% complete)

Load a session:
/project:session-load [session-name]

Or list all sessions:
/project:session-list
```

## Loading Confirmation

### Successful Load

```markdown
✅ Session loaded successfully!

📁 Active Session: user-auth-system
📂 Directory: .claude/claude_sessions/2025-07-20-1445-user-auth-system/
📋 Title: User Authentication System Implementation
⏱️  Started: July 20, 2025 at 2:45 PM
📊 Status: Implementation (67% complete)

📋 Current Focus:
- Working on: Task 2.2 - Implement session management
- Next up: Task 2.3 - Add password reset functionality

🚀 Ready to continue! Use these commands:
- View status: /project:session-view-status
- Continue tasks: /project:session-execute-tasks
- Update progress: /project:session-update
```

### Session Switch

If switching from another active session:

```markdown
🔄 Switching sessions...

Previous: frontend-guide (saving current state)
New: user-auth-system

✅ Session switched successfully!
[... session details as above ...]
```

## Current Session Update

After successful load:
1. **Update `.current-session`**: Write directory name to `.claude/claude_sessions/.current-session`
2. **Add session entry**: Append load event to `[session-name]-progress.md`
3. **Display session context**: Show current status and suggested next actions

## Backward Compatibility

### Legacy Session Support

During transition period, support old `.md` session files:

```markdown
⚠️  Legacy session format detected: $ARGUMENT.md

This session uses the old single-file format. 
Would you like to:
1. Load as-is (limited functionality)
2. Migrate to new directory structure
3. Cancel and choose a different session

Recommended: Migrate to unlock full session features
```

### Migration Assistance

Offer migration for old sessions:
```markdown
🔄 Migrating session to new format...

Created: .claude/claude_sessions/2025-07-20-1445-legacy-session/
├── legacy-session-session.md     (migrated from old file)
├── legacy-session-progress.md    (empty, ready for updates)
└── legacy-session-artifacts/     (empty directory)

✅ Migration complete! Session ready with full functionality.
```

## Error Recovery

### Corrupted Sessions
- **Missing session file**: Offer to recreate session structure
- **Unreadable files**: Show which files are problematic
- **Partial sessions**: Allow loading with warnings about missing components

### Permission Issues
- **Access denied**: Check file permissions and suggest fixes
- **Directory locked**: Handle cases where directory is in use by another process
