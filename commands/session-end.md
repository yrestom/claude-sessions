End the current development session with a comprehensive summary across all session files and artifacts.

## Prerequisites

1. **Check for active session**: Verify `.claude/claude_sessions/.current-session` exists
2. **If no active session**: Inform user there's nothing to end
3. **Extract session name** from current session directory

## Session Completion Process

### 1. Generate Comprehensive Summary

Append to `[session-name]-session.md` a final summary including:

#### Session Overview
- **Session duration**: Start time to end time
- **Session name and objective**
- **Final outcome**: Success/Partial/Failed with explanation

#### Artifact Summary
- **PRD Status**: If `[session-name]-prd.md` exists
  - Requirements clarity and completeness
  - Any scope changes during development
- **Task Execution**: If `[session-name]-tasks.md` exists
  - Total tasks planned vs. completed
  - Task completion rate and timeline
  - Any tasks added/removed during execution
- **Artifacts Created**: List all files in `[session-name]-artifacts/`
  - Design files, documentation, notes
  - Configuration files, scripts, etc.

#### Development Summary
- **Git summary**:
  - Total files changed (added/modified/deleted)
  - List all changed files with change type and brief description
  - Number of commits made during session
  - Final git status and branch state
- **Code accomplishments**:
  - All features implemented
  - Components/modules created or modified
  - API endpoints added or changed
  - Database changes or migrations
- **Testing outcomes**:
  - Test coverage added
  - Test failures resolved
  - Manual testing performed

#### Knowledge & Issues
- **Problems encountered and solutions**
- **Breaking changes or important findings**
- **Dependencies added/removed** with reasoning
- **Configuration changes** made
- **Performance improvements** implemented
- **Security considerations** addressed

#### Project Impact
- **Deployment steps taken** or required
- **Documentation updates** needed
- **Integration points** affected
- **Future work** identified

#### Learning & Recommendations
- **Lessons learned** during development
- **What wasn't completed** and why
- **Tips for future developers** working on related features
- **Recommended next steps**

### 2. Update Progress File

Add final entry to `[session-name]-progress.md`:
```markdown
### Session Completed - 2025-07-20 16:30

**Session Duration**: 2 hours 30 minutes
**Final Status**: Successfully completed

**Final Git State**:
- Total files changed: 12 (8 added, 4 modified, 0 deleted)
- Commits made: 5 commits
- Final branch: feature/user-auth (ready for PR)
- All tests passing: ✅

**Task Completion**:
- Planned: 12 tasks
- Completed: 12 tasks (100%)
- Added during session: 2 additional tasks (also completed)

**Key Deliverables**:
- User authentication system implemented
- Login/logout functionality working
- Session management in place
- Unit tests covering 95% of auth code
- Integration tests for auth flow

**Session Artifacts**:
- PRD: user-auth-prd.md (comprehensive requirements)
- Tasks: user-auth-tasks.md (14 total tasks, all completed)
- Progress: user-auth-progress.md (detailed timeline)
- Design: user-auth-artifacts/auth-flow-diagram.png
- Notes: user-auth-artifacts/implementation-notes.md
```

### 3. Archive Session

1. **Clear `.current-session`**: Empty the file contents (don't delete the file)
2. **Preserve session directory**: Keep all files intact for future reference
3. **Update session index**: If a session index exists, mark this session as completed

### 4. Final Report

Provide user with:
- **Session completion confirmation**
- **Path to session directory** for future reference
- **Summary of key accomplishments**
- **Next recommended actions** (e.g., create PR, deploy, continue with related features)

## Summary Quality Standards

The final summary should be thorough enough that:
- **Another developer** can understand exactly what was built and how
- **Future AI sessions** can continue the work without confusion
- **Project stakeholders** can see clear value delivered
- **The user** has a complete record for documentation or reporting

## Example Final Session Structure

```
.claude/claude_sessions/2025-07-20-1445-user-auth-system/
├── user-auth-session.md          # Complete session overview with final summary
├── user-auth-prd.md             # Product requirements (if created)
├── user-auth-tasks.md           # Task list with all items marked complete
├── user-auth-progress.md        # Detailed timeline with final completion entry
└── user-auth-artifacts/         # All supporting files and documentation
    ├── auth-flow-diagram.png
    ├── implementation-notes.md
    └── api-documentation.md
```

## Integration Benefits

This comprehensive ending:
- **Documents the entire development process**
- **Preserves knowledge for future reference**  
- **Provides clear handoff documentation**
- **Creates searchable project history**
- **Enables session-based project management**
