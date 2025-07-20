Quick reference for Claude Code session commands.

## Available Commands

### Basic Session Management
- `/project:session-start [name]` - Start new development session
- `/project:session-list` - List all sessions  
- `/project:session-load [name]` - Load existing session
- `/project:session-view-status` - Show current session status
- `/project:session-update [notes]` - Add progress update
- `/project:session-end` - End session with summary

### Structured Development Workflow
- `/project:session-create-prd` - Create Product Requirements Document
- `/project:session-generate-tasks` - Generate task list from PRD
- `/project:session-execute-tasks` - Execute tasks step-by-step

### Session Management
- `/project:session-list-artifacts` - View session files
- `/project:session-help` - Show this help

## Quick Start

```bash
# Start a new feature
/project:session-start user-authentication

# Create requirements (optional)
/project:session-create-prd

# Generate tasks (optional) 
/project:session-generate-tasks

# Work on implementation
/project:session-execute-tasks

# Track progress
/project:session-update "Added login form"

# End when complete
/project:session-end
```

## How It Works

Sessions are stored in `.claude/claude_sessions/` as directories with structured files:
- `[name]-session.md` - Main session overview
- `[name]-prd.md` - Requirements document  
- `[name]-tasks.md` - Task list
- `[name]-progress.md` - Progress log
- `[name]-artifacts/` - Supporting files

For detailed documentation, see: `.claude/SESSION_README.md`
