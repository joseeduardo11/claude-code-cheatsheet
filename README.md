# Claude Code Cheatsheet 🚀

A comprehensive reference guide for Claude Code - Anthropic's AI-powered CLI coding assistant. This cheatsheet covers everything from basic commands to advanced workflows, MCP integration, and team collaboration patterns.

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Official-blue)](https://docs.claude.com/en/docs/claude-code/overview)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 📖 What's Inside

This cheatsheet is designed for both beginners and experienced developers looking to master Claude Code. It includes:

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

## 🎯 Who Is This For?

- **New Users**: Get up to speed quickly with clear examples and explanations
- **Daily Users**: Quick reference for commands and configuration options
- **Team Leads**: Set up team-wide standards and workflows
- **SAP Developers**: Leverage MCP servers for CAP, Fiori, UI5, and ABAP development
- **DevOps Engineers**: Integrate Claude Code into CI/CD pipelines

## 📋 Quick Start

1. **View the Cheatsheet**: Open [claude-code-cheatsheet.md](claude-code-cheatsheet.md)
2. **Bookmark for Reference**: Keep it handy while coding
3. **Customize for Your Team**: Fork and adapt to your workflows

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

### Community Resources
- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) - Curated collection of resources
- [Claude Code Discussions](https://github.com/anthropics/anthropic-sdk-typescript/discussions) - Community Q&A

## 🛠️ How to Use This Cheatsheet

### For Individual Developers
1. Clone or download this repository
2. Keep the cheatsheet open in a separate window while coding
3. Customize CLAUDE.md examples for your projects
4. Adapt configuration snippets to your needs

### For Teams
1. Fork this repository
2. Customize with your team's standards and workflows
3. Add your company-specific MCP servers and configurations
4. Share with team members as onboarding material
5. Keep it updated as your practices evolve

### For SAP Developers
The cheatsheet includes specific examples for SAP development:
- MCP server setup for CAP, UI5, and Fiori
- Configuration patterns for ABAP development
- Integration with SAP-specific tooling

See the MCP Server Integration section for details.

## 💡 Pro Tips

1. **Start with CLAUDE.md** - Every project should have one. It saves tokens and ensures consistency.
2. **Use Plan Mode** - Press `Shift+Tab+Tab` for strategic thinking on complex tasks.
3. **Monitor Context** - Use `/context` to check token usage before long operations.
4. **Leverage MCP** - Connect to your tools and services for seamless workflows.
5. **Create Subagents** - Specialized agents maintain better context than general prompts.
6. **Set Permissions** - Protect sensitive files and limit dangerous operations.
7. **Use Hooks** - Automate linting, formatting, and testing as you code.

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

*Last updated: December 2024*
