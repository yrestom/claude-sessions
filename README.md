# Claude Code Session Management Commands

Custom slash commands for Claude Code that provide comprehensive development session tracking and structured workflow management. Based on [Claude Code's custom slash command system](https://docs.anthropic.com/en/docs/claude-code/slash-commands).

## 🎯 Overview

This is an enhanced set of custom slash commands for Claude Code that helps developers maintain continuity across multiple coding sessions with Claude by combining:

- **Documenting Progress**: Capture what was done, how it was done, and why decisions were made
- **Structured Development**: PRD-driven workflow with task management and quality gates
- **Tracking Changes**: Monitor git changes, todo items, and implementation details  
- **Knowledge Transfer**: Enable future sessions to understand past work without re-analyzing the entire codebase
- **Issue Resolution**: Document problems encountered and their solutions for future reference

These commands extend Claude Code's built-in functionality with project-specific session management capabilities that combine the systematic approach of Cursor rules with the flexibility of Claude sessions.

## 🚀 Quick Start

```bash
# Start a new session (with optional name)
/project:session-start authentication-refactor
# Or without a name
/project:session-start

# Create requirements document (optional but recommended)
/project:session-create-prd

# Generate implementation tasks (if PRD exists)
/project:session-generate-tasks

# Execute tasks with quality control
/project:session-execute-tasks

# Update progress during development (with optional notes)
/project:session-update Implemented OAuth with Google
# Or without notes (auto-summarizes recent activity)
/project:session-update

# View current session status
/project:session-view-status

# List all past sessions
/project:session-list

# End session with comprehensive summary
/project:session-end
```

## 📁 File Structure

```
.claude/                           # Claude Code configuration directory
├── commands/                      # Custom command directory
│   ├── session-start.md          # Enhanced session start with PRD workflow
│   ├── session-create-prd.md     # Interactive PRD generation
│   ├── session-generate-tasks.md # Task list creation from PRD
│   ├── session-execute-tasks.md  # Controlled task execution
│   ├── session-update.md         # Progress tracking with task integration
│   ├── session-view-status.md    # Current session overview
│   ├── session-list-artifacts.md # Session artifact management
│   ├── session-load.md           # Enhanced session loading
│   ├── session-list.md           # Directory-based session listing
│   ├── session-end.md            # Comprehensive session summary
│   └── session-help.md           # Quick command reference
├── claude_sessions/               # Session storage directory (directory-based)
│   ├── .current-session          # Tracks the active session directory
│   ├── 2025-07-20-1445-user-auth-system/  # Example session directory
│   │   ├── user-auth-session.md          # Main session overview
│   │   ├── user-auth-prd.md             # Product Requirements Document
│   │   ├── user-auth-tasks.md           # Structured task list
│   │   ├── user-auth-progress.md        # Real-time progress tracking
│   │   └── user-auth-artifacts/         # Supporting files and documentation
│   └── [YYYY-MM-DD-HHMM-name]/           # Session directory naming format
└── SESSION_README.md              # This comprehensive documentation
```

## 🛠️ Installation

1. Clone this repository or copy the folders to your project:
   ```bash
   git clone [repository-url]
   # Or copy the .claude folder to your project root
   ```

2. Create the sessions tracking structure:
   ```bash
   mkdir -p .claude/claude_sessions
   touch .claude/claude_sessions/.current-session
   ```

3. Add to `.gitignore` if you don't want to track sessions:
   ```
   .claude/claude_sessions/
   ```

## 📝 How It Works

This system provides custom slash commands inspired by [Claude Code's custom slash commands](https://docs.anthropic.com/en/docs/claude-code/slash-commands#custom-slash-commands) feature. The system now uses directory-based sessions instead of single files, providing better organization and artifact management.

- **Prefix**: All commands use the `/project:` prefix (for project-specific commands)
- **Arguments**: Commands support arguments using the `$ARGUMENTS` placeholder
- **Execution**: Claude reads the command file and executes the instructions within
- **Structure**: Sessions are organized in directories with meaningful, searchable filenames
- **Note**: These commands are designed to work with Claude but can be adapted for other AI coding assistants

### Enhanced Architecture

This hybrid system combines:

1. **Cursor Rules Structure**: Systematic PRD → Tasks → Implementation workflow
2. **Claude Sessions Flexibility**: Session management, git integration, and real-time tracking

### Meaningful File Naming

All files use the session name as a prefix, making them:
- **Searchable**: Easy to find across the entire project
- **Contextual**: Purpose is clear from the filename
- **Organized**: Related files are grouped by prefix
- **Discoverable**: No need to remember exact locations

## 📋 Command Reference

### Session Lifecycle Commands

#### `/project:session-start [name]`
**Enhanced session startup with PRD workflow initiation**

**Parameters:**
- `[name]` (optional) - A descriptive name for the session. If omitted, creates a session with just the timestamp.

**What it does:**
- Creates a new session directory with timestamp (format: `YYYY-MM-DD-HHMM-name/`)
- Sets up session structure with meaningful file prefixes
- Creates initial files: `[name]-session.md`, `[name]-progress.md`, `[name]-artifacts/`
- Updates `.current-session` to track active session directory
- Prompts for PRD creation for structured development

**Examples:**
```bash
# With a descriptive name
/project:session-start user-authentication-system

# Without a name (just timestamp)
/project:session-start
```

#### `/project:session-create-prd`
**Interactive Product Requirements Document generation**

**What it does:**
- Guides through interactive PRD creation with clarifying questions
- Generates structured requirements suitable for junior developers
- Creates `[session-name]-prd.md` with comprehensive requirements
- Focuses on user stories, functional requirements, and success criteria

#### `/project:session-generate-tasks`
**Generate structured task list from PRD**

**What it does:**
- Analyzes PRD to create implementation tasks
- Two-phase generation: parent tasks → detailed sub-tasks
- Creates `[session-name]-tasks.md` with hierarchical structure
- Identifies relevant files and test requirements
- Requires user approval between phases

#### `/project:session-execute-tasks`
**Controlled task execution with quality gates**

**What it does:**
- Executes one sub-task at a time with user approval
- Implements quality gates: Test → Stage → Clean → Commit
- Updates task completion status in real-time
- Ensures tests pass before marking parent tasks complete
- Integrates with git for automatic commit management

#### `/project:session-update [notes]`
**Enhanced progress tracking with task integration**

**Parameters:**
- `[notes]` (optional) - Custom notes about the update. If omitted, automatically summarizes recent activities.

**What it does:**
- Appends progress notes with timestamp to `[session-name]-progress.md`
- Captures git status and changes
- Tracks task completion progress (if tasks exist)
- Documents issues and solutions
- Records implementation details
- Auto-generates summary if no notes provided

**Examples:**
```bash
# With custom notes
/project:session-update Completed OAuth integration with Google

# Without notes (auto-summarizes)
/project:session-update
```

#### `/project:session-view-status`
**Current session overview and status**

**What it does:**
- Displays comprehensive session overview
- Shows task progress and completion metrics
- Lists git changes and commit status
- Identifies current focus and next actions
- Provides suggestions for next steps

#### `/project:session-list-artifacts`
**View and manage session artifacts**

**What it does:**
- Lists all files in current session directory
- Categorizes artifacts by type (docs, designs, configs, etc.)
- Shows file sizes, modification times, and descriptions
- Provides quick access paths for easy file navigation

#### `/project:session-load [name]`
**Enhanced session loading with flexible matching**

**Parameters:**
- `[name]` - Session name with support for partial matching, dates, and fuzzy search

**What it does:**
- Supports flexible loading patterns (partial names, dates, fuzzy matching)
- Handles multiple matches with clear disambiguation
- Validates session integrity before loading
- Updates current session pointer
- Displays session context and suggested next actions

**Examples:**
```bash
# Load by partial name
/project:session-load user-auth

# Load by date
/project:session-load 2025-07-20

# Load by exact session name
/project:session-load user-authentication-system
```

#### `/project:session-list`
**List all sessions with enhanced information**

**What it does:**
- Shows all session directories with status and progress
- Displays session titles, timestamps, and completion metrics
- Highlights currently active session
- Supports filtering by status, date, or keyword
- Shows brief overview of each session

#### `/project:session-end`
**Comprehensive session completion and archival**

**What it does:**
- Generates complete session summary including:
  - Duration and timing
  - Git changes summary with detailed file list
  - Task completion analysis
  - Key accomplishments and features implemented
  - Problems and solutions documented
  - Dependencies and configuration changes
  - Lessons learned and future recommendations
- Preserves all session artifacts
- Clears `.current-session` file
- Archives session for future reference

#### `/project:session-help`
**Quick command reference**

**What it does:**
- Displays simplified command reference
- Shows basic workflow example
- Points to comprehensive documentation

## 🔄 Development Workflows

### 1. Feature Development Workflow
**Best for**: New features, major functionality additions

```bash
# 1. Start session with descriptive name
/project:session-start user-profile-editing

# 2. Define requirements interactively
/project:session-create-prd
# Answer clarifying questions about:
# - User stories and personas
# - Functional requirements  
# - UI/UX considerations
# - Success criteria

# 3. Plan implementation
/project:session-generate-tasks
# System generates parent tasks, you approve
# System generates detailed sub-tasks

# 4. Execute with quality control
/project:session-execute-tasks
# Work through each sub-task:
# - Code implementation
# - Unit tests
# - Integration tests
# - User approval between tasks
# - Automatic git commits

# 5. Track and document progress
/project:session-update "Added profile image upload"
/project:session-update "Implemented form validation"

# 6. Complete and archive
/project:session-end
```

### 2. Bug Fix Workflow
**Best for**: Bug fixes, small improvements

```bash
# 1. Start session
/project:session-start fix-payment-validation-bug

# 2. Document investigation
/project:session-update "Identified root cause in validation logic"

# 3. Implement fix
/project:session-update "Fixed regex pattern for card numbers"

# 4. Complete
/project:session-end
```

### 3. Research/Investigation Workflow
**Best for**: Technical investigations, proof of concepts

```bash
# 1. Start session
/project:session-start investigate-graphql-performance

# 2. Document findings progressively
/project:session-update "Tested different query optimization strategies"
/project:session-update "Found N+1 query issue in user relations"

# 3. Store artifacts in session-name-artifacts/ directory
# - Performance benchmarks
# - Code samples
# - Documentation links

# 4. Summarize learnings
/project:session-end
```

## 🎯 Best Practices

### Session Naming
**✅ Good Session Names:**
- `user-authentication-system`
- `payment-integration-stripe`
- `dashboard-performance-optimization`
- `api-rate-limiting-implementation`

**❌ Avoid:**
- `feature1`, `task`, `update`
- `fix-bug`, `new-stuff`
- Very long names (>50 characters)

### When to Use PRDs
**Create a PRD for:**
- New features or major functionality
- Complex integrations or refactoring
- When requirements are unclear
- Features requiring stakeholder alignment

**Skip PRD for:**
- Simple bug fixes
- Minor UI adjustments
- Routine maintenance tasks
- Well-defined, small improvements

### Command Usage Best Practices
- These commands work only within Claude Code interactive sessions
- Commands are project-specific and available to all team members
- Arguments are passed directly after the command name
- Use descriptive session names that indicate the main focus
- Start sessions for significant features or bug fixes
- Define clear goals at the beginning

### During Development
- Update regularly when completing significant tasks
- Document unexpected issues and their solutions
- Track breaking changes or important discoveries
- Note any dependencies added or configuration changes
- Complete one sub-task at a time when using task execution
- Run tests before marking parent tasks complete

### Session Management
- Always end sessions with `/project:session-end`
- Review the generated summary for completeness
- Add any missing context before closing
- Use `/project:session-view-status` to check current state
- Load related sessions for context before starting similar work

## 🔧 Advanced Features

### Session Discovery and Loading

#### Flexible Loading Patterns
```bash
# Load by exact session name
/project:session-load payment-integration

# Load by partial name (finds best match)
/project:session-load payment

# Load by date (shows sessions from that date)
/project:session-load 2025-07-20

# Load recent session by index
/project:session-load 1  # Most recent
/project:session-load 2  # Second most recent
```

#### Intelligent Matching
The system uses fuzzy matching to find sessions:
1. **Exact directory name match**
2. **Session name suffix match** (`*-session-name`)
3. **Partial name match** (contains session name)
4. **Date-based matching** (sessions from specific date)
5. **Similarity scoring** (closest match by edit distance)

### Quality Gates Integration

#### Automatic Quality Control
- **Test**: Run full test suite before task completion
- **Stage**: Git add changes only after tests pass
- **Clean**: Remove temporary files and debug code
- **Commit**: Descriptive commit with conventional format

#### Git Integration Features
- Monitor file changes during sessions
- Track commits made during session timeframe
- Calculate lines of code added/modified/deleted
- Identify affected components and modules

### Artifact Management

#### Automatic Artifact Detection
- **Code files**: Source code created/modified during session
- **Test files**: Unit, integration, and e2e tests
- **Documentation**: README updates, API docs, inline comments
- **Configuration**: Environment, build, and deployment configs
- **Design files**: Images, mockups, wire-frames
- **Data files**: Migrations, seeds, sample data

## 💡 Use Cases

### 1. Feature Development
```bash
/project:session-start user-authentication
/project:session-create-prd
/project:session-generate-tasks
/project:session-execute-tasks
# Implement auth logic
/project:session-update Added middleware and login page
# Fix issues
/project:session-update Resolved Next.js 15 async cookie issue
/project:session-end
```

### 2. Bug Fixing
```bash
/project:session-start fix-email-bounce-handling
# Investigate issue
/project:session-update Found AWS SNS webhook misconfiguration
# Implement fix
/project:session-update Updated webhook handler and added logging
/project:session-end
```

### 3. Refactoring
```bash
/project:session-start database-service-refactor
/project:session-create-prd  # For complex refactoring
/project:session-generate-tasks
# Plan refactoring
/project:session-update Created new DB service class architecture
# Execute changes
/project:session-update Migrated all queries to new service
/project:session-end
```

### 4. Performance Optimization
```bash
/project:session-start optimize-api-response-times
/project:session-create-prd
# Define performance goals and metrics
/project:session-generate-tasks
# Break down optimization into measurable tasks
/project:session-execute-tasks
# Implement optimizations with benchmarking
/project:session-end
```

## 🚨 Troubleshooting

### Common Issues

**No active session found**
- Start a new session with `/project:session-start`
- Check `.claude/claude_sessions/.current-session` exists

**Session updates not working**
- Ensure a session is active
- Check file permissions in `.claude/claude_sessions/`

**Session loading problems**
- Use `/project:session-list` to see available sessions
- Try exact session directory name instead of partial match

**Missing git information**
- Verify you're in a git repository
- Check git is properly initialized

**Task execution issues**
- Ensure tests pass before marking parent tasks complete
- Fix any test failures before continuing
- Check that task files exist and are properly formatted

### Recovery Procedures

**Corrupted Session Recovery**
```bash
# 1. Check session integrity
/project:session-view-status

# 2. If files are missing, the system will offer to:
#    - Recreate missing files from templates
#    - Migrate from backup if available
#    - Start fresh with existing content
```

**Lost Session Data**
```bash
# Find sessions in git history
git log --all --full-history -- ".claude/claude_sessions/*"

# Restore deleted session directory
git checkout <commit-hash> -- .claude/claude_sessions/session-name/

# Recreate from partial data
/project:session-start recovered-session-name
# Manually populate files with recovered content
```

## ⚙️ Configuration

### Customizing Commands
Edit the command files in `.claude/commands/` to:
- Change session file format
- Add custom sections
- Modify summary generation
- Adjust git tracking details

### Session Storage
- Default: `.claude/claude_sessions/`
- Can be changed by updating command files
- Consider version control needs

### Project Settings
```json
// .claude/session-config.json
{
  "default_session_type": "structured",  // Use PRD workflow by default
  "auto_create_prd": true,              // Prompt for PRD creation
  "quality_gates_enabled": true,        // Enable test → commit workflow
  "git_integration": true,              // Track git changes
  "artifact_preservation": true,        // Save all session artifacts
  "naming_convention": "session-prefix" // Use session-name prefix
}
```

## 🤖 Benefits for AI Agents

1. **Context Preservation**: Sessions provide rich context about past work
2. **Decision History**: Understand why certain approaches were taken
3. **Issue Awareness**: Know about problems already encountered and solved
4. **Code Evolution**: Track how the codebase has changed over time
5. **Dependency Tracking**: Awareness of what packages and tools are used
6. **Quality Assurance**: Built-in testing and approval gates ensure code quality
7. **Structured Requirements**: PRDs provide clear feature specifications
8. **Task Management**: Hierarchical task breakdown for systematic implementation

## 🔍 Tips and Tricks

1. **Searchable Sessions**: Use consistent terminology in updates for easy searching
2. **Link Issues**: Reference ticket numbers or GitHub issues in updates
3. **Code Snippets**: Include important code changes in session updates
4. **Screenshots**: Reference screenshot paths for UI changes stored in artifacts
5. **Testing Notes**: Document test scenarios and results
6. **Meaningful File Names**: All session files use session-name prefixes for easy discovery
7. **Progressive Documentation**: Update progress files in real-time rather than batching
8. **Quality Gates**: Follow the test → stage → clean → commit workflow religiously

## 📚 References

- [Claude Code Slash Commands Documentation](https://docs.anthropic.com/en/docs/claude-code/slash-commands)
- [Claude Code Memory Management](https://docs.anthropic.com/en/docs/claude-code/memory-management)
- [Claude Code Overview](https://docs.anthropic.com/en/docs/claude-code/overview)

## 📚 Examples

### Complete Feature Implementation Session
```markdown
# Development Session - 2025-07-20 14:45 - user-authentication-system

## Session Overview
- **Start Time**: 2025-07-20 14:45
- **Objective**: Implement comprehensive user authentication
- **Estimated Duration**: 6-8 hours

## Goals
- [x] Create dedicated authentication system
- [x] Add OAuth support with Google and GitHub
- [x] Implement session management
- [x] Add password reset functionality

## Progress
- ✅ **Session Started**: 2025-07-20 14:45
- ✅ **PRD Created**: 2025-07-20 15:00 - [user-authentication-prd.md]
- ✅ **Tasks Generated**: 2025-07-20 15:15 - [user-authentication-tasks.md] (12 tasks)
- ✅ **Implementation**: 12/12 tasks completed (100%)
- ✅ **Testing**: All tests passing
- ✅ **Session Completed**: 2025-07-20 21:30

## Session Summary
Successfully implemented a full-featured authentication system with OAuth support,
session management, and password reset functionality. Resolved Next.js 15 compatibility
issues and added comprehensive error handling. All quality gates passed.
```

## 🤝 Contributing

To improve this system:
1. Enhance command instructions for better AI comprehension
2. Add new commands for specific workflows
3. Improve session file formatting
4. Create utilities for session analysis
5. Extend PRD templates for different project types
6. Add integration with project management tools

## 📄 License

This session management system is open source and available for use in any project.

---

*Remember: Good documentation today saves hours of debugging tomorrow! Use meaningful session names, follow quality gates, and document decisions for future developers.*