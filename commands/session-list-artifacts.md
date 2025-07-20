List and display all artifacts and files within the current active session directory with detailed information about each file.

## Prerequisites

1. **Check for active session**: Verify `.claude/claude_sessions/.current-session` exists
2. **If no active session**: Inform user "No active session. Start one with `/project:session-start`"
3. **Extract session name** from current session directory

## Artifact Listing Process

### 1. Session Directory Overview

Display session directory structure:
```
📁 Session: [session-name]
📂 Location: .claude/claude_sessions/[full-session-directory-name]/

📊 Directory Summary:
- Total Files: [X]
- Core Session Files: [X]
- Artifact Files: [X]
- Directory Size: [X KB/MB]
```

### 2. Core Session Files

List and describe standard session files:
```
📋 Core Session Files:

✅ [session-name]-session.md           [file-size] | [last-modified]
   📝 Main session overview and goals
   📅 Created: [creation-time]
   📈 Last Updated: [last-update-time]

[✅/❌] [session-name]-prd.md          [file-size] | [last-modified]
   📋 Product Requirements Document
   📊 Requirements: [X] functional, [Y] non-functional
   
[✅/❌] [session-name]-tasks.md        [file-size] | [last-modified]  
   ✅ Development task list
   📊 Tasks: [X] total ([Y] completed, [Z] pending)

✅ [session-name]-progress.md          [file-size] | [last-modified]
   📈 Progress tracking and updates  
   📊 Updates: [X] entries spanning [Y] hours
```

### 3. Artifact Directory Contents

List files in `[session-name]-artifacts/` directory:
```
📦 Artifacts Directory: [session-name]-artifacts/

[if artifacts exist:]
📄 [filename1.ext]                    [file-size] | [last-modified]
   📝 [brief description based on file type/name]
   
📄 [filename2.ext]                    [file-size] | [last-modified]
   📝 [brief description based on file type/name]

[if no artifacts:]
📭 No additional artifacts created yet
```

### 4. File Type Summary

Categorize artifacts by type:
```
📊 File Types Summary:

📝 Documentation: [X] files
   - README, notes, specifications, etc.

🎨 Design Files: [X] files  
   - Images, mockups, diagrams, wire-frames
   
⚙️  Configuration: [X] files
   - Config files, scripts, environment files
   
📄 Other: [X] files
   - Miscellaneous files and exports
```

### 5. Quick File Access

Provide file paths for easy access:
```
🔗 Quick Access Paths:

Main Session:     .claude/claude_sessions/[dir]/[session-name]-session.md
PRD Document:     .claude/claude_sessions/[dir]/[session-name]-prd.md  
Task List:        .claude/claude_sessions/[dir]/[session-name]-tasks.md
Progress Log:     .claude/claude_sessions/[dir]/[session-name]-progress.md
Artifacts Folder: .claude/claude_sessions/[dir]/[session-name]-artifacts/
```

## Optional Detailed View

### With Content Preview (--preview flag)

Show first few lines of each file:
```
📄 [session-name]-session.md (Preview):
   # User Authentication System - 2025-07-20 14:00
   
   ## Session Overview
   - **Start Time**: 2025-07-20 14:00
   - **Objective**: Implement comprehensive user authentication
   ...

📄 [session-name]-prd.md (Preview):
   # User Authentication - Product Requirements Document
   
   ## Introduction/Overview
   Implement a secure user authentication system...
   ...
```

### With File Statistics (--stats flag)

Show detailed file information:
```
📊 File Statistics:

[session-name]-session.md:
   - Size: 2.4 KB
   - Lines: 156
   - Words: 892  
   - Created: 2025-07-20 14:00:15
   - Modified: 2025-07-20 16:45:23
   - Modifications: 8 times

[session-name]-progress.md:
   - Size: 5.2 KB
   - Updates: 12 entries
   - Time Span: 2h 45m
   - Average Update Interval: 14 minutes
```

## File Type Recognition

Automatically recognize and describe common file types:

- **.md files**: Markdown documentation
- **.png/.jpg/.svg**: Images and diagrams  
- **.json/.yaml/.toml**: Configuration files
- **.txt**: Text notes and logs
- **.pdf**: Documentation exports
- **.html**: Web exports or reports
- **No extension**: Likely text files or scripts

## Integration Features

### Search Functionality

Allow searching within artifacts:
```
🔍 Search in Session Artifacts:
Use: /project:session-list-artifacts --search "keyword"

Example: Find all references to "authentication" across session files
```

### Export Options

Provide export suggestions:
```
📤 Export Options:
- Archive entire session: tar/zip the session directory
- Export specific artifacts: copy artifacts to project documentation
- Generate session report: combine all files into comprehensive document
```

## Error Handling

- **No artifacts directory**: Create it if it doesn't exist
- **Corrupted files**: Report which files can't be read
- **Permission issues**: Handle access denied scenarios  
- **Large files**: Handle gracefully without crashing
- **Binary files**: Detect and handle appropriately

## User Experience Features

- **Visual hierarchy**: Use emojis and formatting for clarity
- **File size formatting**: Human-readable sizes (KB, MB)
- **Relative timestamps**: "2 hours ago", "yesterday"
- **Color coding**: Different types of files visually distinct
- **Interactive elements**: Suggest actions for each file type

## Performance Considerations

- **Lazy loading**: Only read file stats when needed
- **Caching**: Cache file information for repeat calls
- **Pagination**: Handle sessions with many artifacts
- **Memory efficiency**: Don't load large files into memory for preview