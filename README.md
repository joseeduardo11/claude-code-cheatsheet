# Claude Code Cheatsheet 🚀

A comprehensive reference guide for Claude Code - Anthropic's AI-powered CLI coding assistant. This repository includes command references, automation guides, and best practices for developers and teams.

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Official-blue)](https://docs.claude.com/en/docs/claude-code/overview)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🚀 Quick Navigation

| 📖 Guide | 🎯 Best For | ⏱️ Read Time |
|---------|------------|-------------|
| [**Main Cheatsheet**](claude-code-cheatsheet.md) | Command reference, configuration, MCP setup | 15-20 min |
| [**Git Diff Automation**](git-diff-claude-automation.md) | Automated reviews, CI/CD, scripts | 10-15 min |

**New to Claude Code?** Start with the [Main Cheatsheet](claude-code-cheatsheet.md)  
**Setting up automation?** Jump to [Git Diff Automation](git-diff-claude-automation.md)

## 📖 What's Inside

This repository contains comprehensive guides for mastering Claude Code:

### 📘 [Main Cheatsheet](claude-code-cheatsheet.md)
Complete reference covering:
- **Installation & Setup** - Get started quickly with authentication and configuration
- **Core Commands** - Essential commands for daily development workflows
- **Slash Commands** - In-session commands for context management and navigation
- **Configuration Files** - CLAUDE.md, settings.json, and hierarchical configurations
- **Custom Commands** - Create reusable project and personal commands
- **MCP Integration** - Connect to external services (GitHub, databases, SAP, etc.)
- **Subagents** - Specialized AI helpers for specific tasks
- **Skills** - Reusable workflows and best practices
- **Hooks** - Automated actions triggered by Claude's operations
- **Advanced Workflows** - Git worktrees, CI/CD integration, batch processing
- **Permissions & Security** - Fine-grained control over Claude's capabilities
- **Cost Management** - Optimize token usage and manage expenses
- **Troubleshooting** - Common issues and solutions

### 🔄 [Git Diff + Claude Automation](git-diff-claude-automation.md)
Automated code review guide covering:
- **Automated Reviews** - Security, performance, and quality checks via git diff
- **SDK Mode (`-p`)** - One-shot execution for scripts and CI/CD pipelines
- **SAP Development** - CAP, UI5, Fiori, and ABAP-specific review patterns
- **CI/CD Integration** - GitHub Actions, GitLab CI, and pre-commit hooks
- **Shell Scripts** - Ready-to-use automation scripts
- **Best Practices** - Cost optimization and effective review patterns

## 🎯 Who Is This For?

- **New Users**: Get up to speed quickly with clear examples and explanations
- **Daily Users**: Quick reference for commands and configuration options
- **Team Leads**: Set up team-wide standards and workflows
- **SAP Developers**: Leverage MCP servers for CAP, Fiori, UI5, and ABAP development
- **DevOps Engineers**: Integrate Claude Code into CI/CD pipelines

## 📋 Quick Start

1. **Browse the guides**:
   - [Main Cheatsheet](claude-code-cheatsheet.md) - Complete command reference
   - [Git Diff Automation](git-diff-claude-automation.md) - Automated code reviews
2. **Bookmark for Reference**: Keep them handy while coding
3. **Try the examples**: Start with basic commands and build up
4. **Customize for Your Workflow**: Adapt examples to your needs

## 📂 Repository Structure

```
claude-code-cheatsheet/
├── README.md                           # This file - overview and navigation
├── claude-code-cheatsheet.md          # Complete command reference
├── git-diff-claude-automation.md      # Automated review guide
└── LICENSE                             # MIT License
```

## 🔥 Highlights

### Essential Commands
```bash
# Start interactive session
claude

# Execute and exit (SDK mode)
claude -p "analyze this codebase"

# Continue last conversation
claude -c

# Resume specific session
claude --resume
```

### Configuration Example
```json
{
  "model": "claude-sonnet-4-20250514",
  "permissions": {
    "allowedTools": ["Read", "Write(src/**)", "Bash(git *)"],
    "deny": ["Read(.env*)", "Bash(rm *)"]
  }
}
```

### MCP Integration
```bash
# Add GitHub integration
claude mcp add github -- npx -y @modelcontextprotocol/server-github

# Add SAP CAP server
claude mcp add cap -- npx @cap-js/mcp-server

# List configured servers
claude mcp list
```

### Automated Code Reviews with Git Diff
```bash
# Security review
git diff HEAD~1 | claude -p "review this PR for security issues" > security_review.md

# Performance analysis
git diff HEAD~1 | claude -p "check for performance issues" > performance_review.md

# SAP-specific review
git diff HEAD~1 -- srv/ | claude -p "review CAP services for security and performance" > cap_review.md
```

See the complete [Git Diff Automation Guide](git-diff-claude-automation.md) for CI/CD integration and advanced patterns.

## 🤖 Automation Capabilities

### Automated Code Reviews
Automatically review code changes with Claude before commits, in CI/CD pipelines, or on-demand:

```bash
# Pre-commit review
git diff --staged | claude -p "quick security check" > review.md

# CI/CD integration
git diff HEAD~1 | claude -p "comprehensive review" > ci_review.md

# Branch comparison
git diff main...feature | claude -p "feature review" > feature_review.md
```

### CI/CD Integration
- **GitHub Actions**: Automated PR reviews with comments
- **GitLab CI**: Pipeline integration with artifact storage
- **Pre-commit Hooks**: Catch issues before they're committed
- **Shell Scripts**: Custom automation workflows

**👉 Full automation guide**: [git-diff-claude-automation.md](git-diff-claude-automation.md)

---

## 🎯 Common Use Cases

### For Daily Development
- **Interactive coding**: Use [Main Cheatsheet](claude-code-cheatsheet.md) for `claude` command reference
- **Project setup**: Configure CLAUDE.md, settings.json, and permissions
- **MCP integration**: Connect to GitHub, databases, SAP services

### For Code Quality
- **Automated reviews**: Use [Git Diff Guide](git-diff-claude-automation.md) for security/performance checks
- **Pre-commit validation**: Set up hooks to catch issues early
- **PR reviews**: Automate review comments in GitHub/GitLab

### For SAP Development
- **CAP development**: Review CDS models, services, and configurations
- **UI5/Fiori**: Check controllers, views, and manifest.json
- **Deployment**: Validate mta.yaml and xs-security.json

### For Teams
- **Onboarding**: Share cheatsheets with new team members
- **Standards**: Use as reference for team coding standards
- **CI/CD**: Implement automated quality gates

---

## 📚 Related Resources

### Official Documentation
- [Claude Code Overview](https://docs.claude.com/en/docs/claude-code/overview)
- [Claude API Documentation](https://docs.claude.com/en/api/overview)
- [Claude.ai Support](https://support.claude.com)

### MCP Servers
- [@modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) - Official MCP servers
- [@cap-js/mcp-server](https://www.npmjs.com/package/@cap-js/mcp-server) - SAP CAP development
- [@ui5/mcp-server](https://www.npmjs.com/package/@ui5/mcp-server) - SAP UI5 development
- [@sap-ux/fiori-mcp-server](https://www.npmjs.com/package/@sap-ux/fiori-mcp-server) - SAP Fiori development

### CI/CD & Automation
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitLab CI/CD Documentation](https://docs.gitlab.com/ee/ci/)
- [Git Hooks Documentation](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)

### Community Resources
- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) - Curated collection of resources
- [Claude Code Discussions](https://github.com/anthropics/anthropic-sdk-typescript/discussions) - Community Q&A

## 🛠️ How to Use This Repository

### For Individual Developers
1. Clone or download this repository
2. Start with the [Main Cheatsheet](claude-code-cheatsheet.md) for command reference
3. Read the [Git Diff Automation Guide](git-diff-claude-automation.md) to set up automated reviews
4. Keep these guides open in a separate window while coding
5. Customize CLAUDE.md examples for your projects
6. Adapt configuration snippets to your needs

### For Teams
1. Fork this repository
2. Customize with your team's standards and workflows
3. Add your company-specific MCP servers and configurations
4. Set up CI/CD pipelines using the automation guide
5. Share with team members as onboarding material
6. Keep it updated as your practices evolve

### For SAP Developers
Both guides include specific examples for SAP development:
- **Main Cheatsheet**: MCP server setup for CAP, UI5, and Fiori
- **Git Diff Guide**: CAP service reviews, UI5 controller checks, MTA validation
- **Automation**: Pre-commit hooks for ABAP standards, CDS model validation

See the MCP Server Integration sections and SAP Development Examples for details.

## 💡 Pro Tips

1. **Start with CLAUDE.md** - Every project should have one. It saves tokens and ensures consistency.
2. **Use Plan Mode** - Press `Shift+Tab+Tab` for strategic thinking on complex tasks.
3. **Monitor Context** - Use `/context` to check token usage before long operations.
4. **Leverage MCP** - Connect to your tools and services for seamless workflows.
5. **Create Subagents** - Specialized agents maintain better context than general prompts.
6. **Set Permissions** - Protect sensitive files and limit dangerous operations.
7. **Use Hooks** - Automate linting, formatting, and testing as you code.
8. **Automate Reviews** - Use `git diff | claude -p` for automated code reviews in CI/CD.
9. **Pre-commit Checks** - Catch issues before they're committed with automated reviews.
10. **Parallel Processing** - Run multiple reviews simultaneously to save time.

## 🤝 Contributing

Contributions are welcome! If you have:
- Additional tips and tricks
- Better configuration examples
- New workflow patterns
- Corrections or clarifications
- SAP-specific integrations

Please feel free to:
1. Fork this repository
2. Create a feature branch (`git checkout -b feature/amazing-tip`)
3. Commit your changes (`git commit -m 'Add amazing tip'`)
4. Push to the branch (`git push origin feature/amazing-tip`)
5. Open a Pull Request

## 📝 Changelog

### v1.1.0 (December 2024)
- Added comprehensive Git Diff + Claude Automation guide
- Added CI/CD integration examples (GitHub Actions, GitLab CI)
- Added pre-commit hook examples
- Added shell script templates for automated reviews
- Expanded SAP development examples
- Added parallel review patterns

### v1.0.0 (December 2024)
- Initial release
- Comprehensive command reference
- Configuration examples
- MCP integration guide
- Advanced workflows and patterns
- SAP development integration

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Anthropic** for creating Claude Code and maintaining excellent documentation
- **SAP Community** for MCP server development and integration patterns
- **Contributors** who have shared workflows and best practices

## 📞 Support

- **Issues**: Found a problem? [Open an issue](../../issues)
- **Questions**: Check [Anthropic's Support Center](https://support.claude.com)
- **Updates**: Watch this repo for updates as Claude Code evolves

---

**Made with ❤️ for the Claude Code community**

*Last updated: December 2025*
