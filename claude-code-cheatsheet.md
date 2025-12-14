# Claude Code Cheatsheet

Complete reference guide for Claude Code - Anthropic's AI-powered CLI coding assistant.

---

## Installation & Setup

```bash
# Install Claude Code
curl -sL https://install.anthropic.com | sh

# Or via npm
npm install -g @anthropic-ai/claude-code

# Authenticate (browser-based flow)
claude auth login

# Check auth status
claude auth status

# Check version
claude --version

# Update to latest
claude update

# Diagnose installation
/doctor
```

---

## Core Commands

### Starting Sessions

```bash
# Start interactive REPL
claude

# Start with initial prompt
claude "summarize this project"

# Execute once and exit (SDK mode)
claude -p "explain this function"

# Process piped content
cat logs.txt | claude -p "find errors"

# Continue most recent conversation
claude -c
claude --continue

# Resume specific session by ID
claude -r <session-id>
claude --resume <session-id>

# List recent sessions (run without ID)
claude --resume
```

### Model Selection

```bash
# Use latest Sonnet (default)
claude --model sonnet

# Use latest Opus
claude --model opus

# Specific version
claude --model claude-sonnet-4-20250514
```

### Output Formats

```bash
# JSON output
claude -p "analyze code" --output-format json

# Stream JSON
claude -p "process data" --output-format stream-json

# Text output (default)
claude -p "explain function" --output-format text
```

---

## Slash Commands (In-Session)

### Session Management
```
/help          # Show all available commands
/clear         # Reset conversation history
/exit          # End session (or Ctrl+D)
/status        # Show version and connectivity
/config        # Open configuration interface
/doctor        # Diagnose installation issues
/cost          # Display token usage statistics
```

### Context Management
```
/context       # Visualize current context usage
/add-dir       # Add additional working directories
/rewind        # Rewind to previous checkpoint
```

### Code Operations
```
/review        # Request code review of changes
/todos         # List all TODO items being tracked
```

### Output Control
```
/output-style      # Configure response formatting
/export [filename] # Export conversation to file
```

### MCP (Model Context Protocol)
```
/mcp               # Select and interact with MCP servers
/mcp list          # List all configured MCP servers
```

---

## Keyboard Shortcuts

```
Tab            # Auto-complete
Up/Down        # Navigate command history
Ctrl+C         # Cancel current operation
Ctrl+D         # Exit Claude Code
Shift+Tab+Tab  # Plan Mode (strategic thinking)
```

---

## Configuration Files

### Hierarchy (from least to most specific)

1. **Global**: `~/.claude/CLAUDE.md` - Applies to all projects
2. **User Settings**: `~/.claude/settings.json` - Global preferences
3. **Project**: `.claude/CLAUDE.md` - Shared with team (Git)
4. **Project Settings**: `.claude/settings.json` - Team shared (Git)
5. **Local**: `.claude/settings.local.json` - Personal (Git ignored)

### CLAUDE.md Example

```markdown
# Project Context

## Overview
Brief description of the project and its goals.

## Coding Standards
- Use TypeScript for all new code
- Follow ESLint configuration
- Write tests with Jest
- Use functional components in React

## Architecture
- Frontend: Next.js with TypeScript
- Backend: Node.js with Express
- Database: PostgreSQL with Prisma
- State: Zustand for client state

## File Organization
- Components: `src/components/`
- Utilities: `src/utils/`
- Tests: alongside source files with `.test.ts`

## Known Issues
- `db.connect()` sometimes times out; retry twice
- For large JSON, use streaming to avoid memory issues

## Preferences
- Ask for clarification if request is ambiguous
- Don't generate new `.md` files unless instructed
- Include `co-authored-by: Claude` in commits
```

### settings.json Example

```json
{
  "model": "claude-sonnet-4-20250514",
  "maxTokens": 4096,
  "permissions": {
    "allowedTools": [
      "Read",
      "Write(src/**)",
      "Bash(git *)",
      "Bash(npm *)"
    ],
    "deny": [
      "Read(.env*)",
      "Write(production.config.*)",
      "Bash(rm *)",
      "Bash(sudo *)"
    ]
  },
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write(*.py)",
        "hooks": [
          {
            "type": "command",
            "command": "python -m black $file"
          }
        ]
      }
    ]
  }
}
```

---

## Custom Commands

### Project Commands (Shared)
Location: `.claude/commands/`
```bash
# Example: .claude/commands/analyze.md
---
description: Perform deep code analysis
model: claude-opus-4-1-20250805
disable-model-invocation: true
---

Perform comprehensive analysis focusing on:
- Architecture patterns
- Scalability issues
- Security vulnerabilities
- Performance bottlenecks
```

### Personal Commands
Location: `~/.claude/commands/`
```bash
# Available across all projects
# Same format as project commands
```

### Using Arguments
```markdown
# In command file
Review the following code: $ARGUMENTS

# Usage
/my-command "code to review"
```

### Bash Execution in Commands
```markdown
# Execute command before processing
!`git status`
Review the current git status above
```

---

## File References

```bash
# Include file contents in prompt
claude "explain this: @filename.py"

# Multiple files
claude "compare @old.js and @new.js"

# In interactive session
> explain @complex_function.py
```

---

## MCP Server Integration

### Add MCP Servers

```bash
# GitHub integration
claude mcp add github -- npx -y @modelcontextprotocol/server-github

# File system operations
claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem /path/to/dir

# PostgreSQL
claude mcp add postgres -- npx -y @modelcontextprotocol/server-postgres postgresql://connection-string

# Puppeteer (browser automation)
claude mcp add puppeteer -- npx -y @modelcontextprotocol/server-puppeteer

# SAP CAP
claude mcp add cap -- npx @cap-js/mcp-server

# Import from Claude Desktop
claude mcp add-from-claude-desktop

# List configured servers
claude mcp list
```

### Using MCP Servers

```bash
# Natural language (in session)
> Show me GitHub issue #123
> Query users table for John
> Take screenshot of https://example.com

# Direct command selection
/mcp  # Then select server
```

---

## Subagents (Specialized AI Helpers)

### Project Subagents
Location: `.claude/agents/` (highest priority, team shared)

### User Subagents
Location: `~/.claude/agents/` (personal, all projects)

### Example Subagent

```markdown
# .claude/agents/code-reviewer.md
---
name: code-reviewer
description: Expert code review specialist. Use immediately after writing code.
tools: Read, Grep, Glob, Bash
model: inherit
---

You are a senior code reviewer ensuring high standards:

## Review Checklist
1. Code organization and structure
2. Error handling
3. Performance considerations
4. Security concerns
5. Test coverage

## Review Process
- Examine code systematically
- Identify improvements
- Suggest best practices
- Check for common pitfalls
```

### Subagent Benefits
- **Context Preservation**: Separate context from main conversation
- **Specialized Expertise**: Fine-tuned prompts for specific tasks
- **Reusable Workflows**: Share across projects and team
- **Tool Control**: Grant specific permissions per subagent
- **Automatic Delegation**: Claude uses appropriate subagents

---

## Skills

### Project Skills
Location: `.claude/skills/`

### Example Skill

```markdown
# .claude/skills/commit-messages/SKILL.md
---
name: generating-commit-messages
description: Generates clear commit messages from git diffs
---

# Generating Commit Messages

## Instructions
1. Run `git diff --staged` to see changes
2. Generate commit message with:
   - Summary under 50 characters
   - Detailed description
   - Affected components

## Best Practices
- Use present tense
- Explain what and why, not how
```

---

## Hooks (Automated Actions)

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write(*.py)",
        "hooks": [
          {
            "type": "command",
            "command": "python -m black $file"
          }
        ]
      },
      {
        "matcher": "Write(*.js)",
        "hooks": [
          {
            "type": "command",
            "command": "npm run lint -- --fix $file"
          }
        ]
      }
    ]
  }
}
```

---

## Advanced Workflows

### Git Worktrees

```bash
# Create worktree for focused task
git worktree add ../myapp-review -b review/cleanup feature-branch
cd ../myapp-review
claude "add docs, tests, and clean up code style"

# Merge when done
git merge review/cleanup
```

### Status Line Customization

```bash
# Add custom status line
/statusline add Model | Git Branch | Tokens | Directory

# Example script-based status
/statusline add $(git rev-parse --abbrev-ref HEAD) | $(pwd | rev | cut -d'/' -f1 | rev)
```

### Batch Processing

```bash
# Analyze multiple files
find . -name "*.js" -exec claude -p "analyze for bugs: {}" \; > report.txt

# Generate documentation
for file in src/*.py; do
  claude -p "generate docstring for $file" >> docs.md
done
```

### CI/CD Integration

```bash
# Pre-commit hook
claude -p "review staged changes" > /dev/null || exit 1

# Automated code review
git diff --name-only | claude -p "review these changes"

# Generate changelog
git log --oneline -10 | claude -p "create changelog"
```

---

## Permissions & Security

### Permission Patterns

```json
{
  "permissions": {
    "allowedTools": [
      "Read",                    // Read any file
      "Write(src/**)",          // Write only in src/
      "Bash(git *)",            // Any git command
      "Bash(npm test)",         // Specific npm command
      "Glob"                    // File pattern matching
    ],
    "deny": [
      "Read(.env*)",            // No env files
      "Read(**/.git/**)",       // No git internals
      "Write(production.*)",    // No production configs
      "Bash(rm *)",             // No deletions
      "Bash(sudo *)"            // No sudo
    ]
  }
}
```

### Security Best Practices

- Review permissions regularly
- Use deny rules for sensitive files
- Limit bash commands to safe operations
- Test in development first
- Use version control for all configs
- Never commit API keys or secrets

---

## Cost Management

### Monitor Usage

```bash
# In session
/cost

# Check status
/status
```

### Optimize Costs

```bash
# Limit conversation length
claude --max-turns 5 "focused review"

# Use appropriate model
claude --model sonnet  # More cost-effective
claude --model opus    # More capable, higher cost
```

### Plan Selection

- **Free**: Limited messages for trying Claude
- **Pro**: Medium-high coding workload
- **Max**: Heavy daily development use
- **API**: Pay-as-you-go for custom rate limits

---

## Common Patterns

### Document & Clear Flow
```bash
> Save your current plan to planning.md
> /clear
> Review @planning.md and continue
```

### Progressive Development
```bash
# 1. Plan
> Shift+Tab+Tab to enter Plan Mode
> Outline approach for feature X

# 2. Implement incrementally
> Implement step 1: database schema
> Implement step 2: API endpoints
> Implement step 3: frontend components

# 3. Review
> /review all changes
```

### Context Management
```bash
# Check context before long task
/context

# If context is high, document and clear
> Document current progress in notes.md
> /clear
> Continue from @notes.md
```

---

## Tips & Best Practices

### Effective Prompting
- Be specific and clear about requirements
- Provide context and constraints upfront
- Reference files with @ syntax
- Use Plan Mode (Shift+Tab+Tab) for complex tasks
- Break large tasks into smaller steps

### Context Management
- Monitor context usage with `/context`
- Document and clear when context fills
- Use CLAUDE.md to reduce repetitive context
- Focus on relevant files with @references

### Team Collaboration
- Use `.claude/` directory for team configs
- Share commands, skills, and agents
- Document in CLAUDE.md
- Use Git to version control configs
- Keep secrets in `.claude/settings.local.json`

### Performance
- Use appropriate model (Sonnet vs Opus)
- Limit conversation turns when appropriate
- Clear context periodically
- Use MCP servers for external integrations
- Leverage hooks for automation

---

## Troubleshooting

```bash
# Installation issues
/doctor

# Check connectivity
claude "test connection"

# Reset configuration
claude config reset

# Clear cache
claude --clear-cache

# Verbose debug mode
claude --verbose --debug

# Logout and re-authenticate
claude auth logout
claude auth login

# Use proxy
claude --proxy http://proxy:8080
```

---

## Resources

- **Official Docs**: https://docs.claude.com/en/docs/claude-code/overview
- **Support**: https://support.claude.com
- **API Docs**: https://docs.claude.com/en/api/overview
- **npm Package**: https://www.npmjs.com/package/@anthropic-ai/claude-code

---

## Quick Reference Card

```
ESSENTIAL COMMANDS
claude                  # Start interactive session
claude -p "query"       # Execute and exit
claude -c               # Continue last session
claude --resume         # List & resume sessions
/help                   # Show all commands
/clear                  # Clear history
/exit                   # Exit (or Ctrl+D)

CONTEXT & FILES
@filename              # Include file in prompt
/add-dir <path>        # Add directory
/context               # Show context usage
Shift+Tab+Tab          # Plan Mode

MCP & TOOLS
/mcp                   # Interact with servers
claude mcp list        # List MCP servers

COST & STATUS
/cost                  # Show token usage
/status                # System info
/doctor                # Diagnose issues

KEYBOARD
Tab                    # Auto-complete
Ctrl+C                 # Cancel
Ctrl+D                 # Exit
↑/↓                    # Command history
```

---

**Pro Tip**: Start every new project with a well-crafted CLAUDE.md file. It saves tokens, reduces repetition, and ensures consistent behavior across sessions.
