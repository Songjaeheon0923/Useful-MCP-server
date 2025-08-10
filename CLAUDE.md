# CLAUDE.md

This file provides guidance to Claude CLI when working with the Useful MCP Server documentation project.

## Project Overview

**Useful-MCP-server** is a comprehensive documentation and configuration guide for MCP (Model Context Protocol) servers that work with Claude Code. This project contains detailed setup instructions, configuration examples, and troubleshooting guides for 9 verified MCP servers.

### Technology Stack

- **Documentation**: Markdown files with structured examples
- **Configuration**: JSON configuration files and shell scripts
- **Testing**: Manual verification and debugging procedures
- **Platforms**: Cross-platform support (Windows, macOS, Linux)

## Project Structure

```
Useful-MCP-server/
├── README.md                    # Main project overview
├── QUICK_START.md              # Step-by-step installation guide
├── CLAUDE.md                   # This file (project instructions)
├── docs/                       # Detailed documentation
│   ├── servers/                # Individual server documentation
│   │   ├── filesystem.md       # File system operations
│   │   ├── github.md          # GitHub integration
│   │   ├── memory.md          # Knowledge graph and memory
│   │   ├── sequential-thinking.md # Structured problem solving
│   │   ├── context7.md        # Real-time library documentation
│   │   ├── magic.md           # AI-powered UI generation
│   │   ├── figma.md           # Design-to-code conversion
│   │   ├── puppeteer.md       # Browser automation
│   │   └── notion.md          # Notion workspace integration
│   └── experimental-servers.md # Untested/experimental servers
└── scripts/                    # Installation scripts (if any)
    ├── quick-setup.bat         # Windows batch script
    └── quick-setup.sh          # Unix shell script
```

## Documentation Standards

### File Structure
Each MCP server documentation follows this structure:
1. **Header**: Package name, GitHub link, status
2. **Overview**: Brief description and main features
3. **Installation**: Step-by-step setup instructions
4. **Configuration**: Environment variables and settings
5. **Usage Examples**: Practical use cases
6. **Troubleshooting**: Common issues and solutions
7. **References**: Links to official documentation

### Status Indicators
- ✅ **연결됨**: Verified and working
- ⚠️ **테스트 필요**: Needs verification
- ❌ **문제 있음**: Known issues
- 🔄 **실험적**: Experimental/beta

## MCP Server Categories

### Core Servers (Essential)
- **Filesystem**: File operations and management
- **GitHub**: Repository and issue management
- **Memory**: Persistent context and knowledge graphs
- **Sequential Thinking**: Structured problem solving

### Productivity Servers
- **Context7**: Real-time library documentation
- **Magic**: AI-powered UI component generation
- **Figma**: Design-to-code workflow
- **Notion**: Workspace integration

### Automation Servers
- **Puppeteer**: Browser automation and web scraping

## Installation Workflow

### 1. Prerequisites Check
- Node.js v18+ with npm/npx in PATH
- Claude CLI properly installed
- Required API keys for specific servers

### 2. Installation Methods
- **Automated**: Using installation commands from QUICK_START.md
- **Manual**: Individual server setup following docs/servers/
- **Troubleshooting**: Alternative methods for failed installations

### 3. Verification Process
```bash
# Check installation
claude mcp list

# Debug verification
claude --debug
# Then use: /mcp
```

## Development Commands

### Documentation Updates
```bash
# Update server count in README.md when adding new servers
# Update QUICK_START.md with new installation commands
# Create individual server documentation in docs/servers/
```

### Testing New Servers
```bash
# Test installation
claude mcp add <server-name> --scope user <command>

# Verify functionality
claude mcp list
claude --debug

# Document results in appropriate .md file
```

### Configuration Management
```bash
# Windows user scope
C:\Users\{username}\.claude\

# Project scope
.claude/

# Check current configuration
claude mcp get <server-name>
```

## API Key Management

### Required API Keys
- **GitHub**: `GITHUB_PERSONAL_ACCESS_TOKEN`
- **Magic**: `TWENTY_FIRST_API_KEY`
- **Figma**: `FIGMA_API_KEY`

### Environment Setup
```bash
# Windows
set API_KEY=your-key-here

# Cross-platform
export API_KEY="your-key-here"
```

## Windows-Specific Considerations

### Path Handling
- Use double backslashes (\\\\) in JSON configurations
- Example: `"C:\\\\Users\\\\username\\\\file.txt"`

### Command Execution
- Prefer `cmd.exe` wrapper for npx commands
- Use `-y` flag to auto-accept installations
- Consider PowerShell for complex operations

### Configuration Formats
```json
{
  "server-name": {
    "type": "stdio",
    "command": "cmd.exe",
    "args": ["/c", "npx", "-y", "package-name"],
    "env": {
      "API_KEY": "value"
    }
  }
}
```

## Documentation Maintenance

### Adding New Servers
1. Create documentation file in `docs/servers/`
2. Update README.md server count and table
3. Update QUICK_START.md installation commands
4. Test installation and functionality
5. Update status indicators

### Updating Existing Servers
1. Verify current functionality
2. Update installation instructions if changed
3. Add new features or usage examples
4. Update troubleshooting section with new issues
5. Maintain consistent documentation format

## Quality Assurance

### Before Committing Changes
- Verify all installation commands work
- Test on Windows environment
- Check markdown formatting and links
- Ensure consistent documentation structure
- Update version numbers and dates

### Testing Checklist
- [ ] Server installs successfully
- [ ] Shows as "✓ Connected" in `claude mcp list`
- [ ] Functions correctly in debug mode
- [ ] API keys and environment variables work
- [ ] Documentation is complete and accurate

## Project Goals

### Primary Objectives
- Provide reliable MCP server installation guides
- Maintain up-to-date documentation for all servers
- Offer troubleshooting solutions for common issues
- Support multiple operating systems (focus on Windows)

### Quality Standards
- All servers must be tested and verified
- Documentation must be comprehensive and clear
- Installation instructions must work on first try
- Troubleshooting guides must solve real problems

## Important Notes

### Installation Philosophy
- Install only requested MCP servers
- Use user scope (--scope user) for global availability
- Verify functionality after each installation
- Document any issues or workarounds

### Error Handling
- Database servers may show errors without running database
- API servers need valid keys to function properly
- Network-dependent servers may have connectivity issues
- Always provide fallback installation methods

### User Experience
- Provide clear, step-by-step instructions
- Include both automated and manual installation options
- Offer multiple configuration approaches
- Maintain comprehensive troubleshooting guides

---

**Test Environment**: Windows, Claude CLI  