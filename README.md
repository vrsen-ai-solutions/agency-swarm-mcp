# Agency Swarm MCP [![GitHub stars](https://img.shields.io/github/stars/VRSEN/agency-swarm-mcp?style=social)](https://github.com/VRSEN/agency-swarm-mcp/stargazers)

[![CI](https://github.com/VRSEN/agency-swarm-mcp/actions/workflows/ci.yml/badge.svg)](https://github.com/VRSEN/agency-swarm-mcp/actions/workflows/ci.yml) [![npm version](https://badge.fury.io/js/agency-swarm-mcp.svg)](https://badge.fury.io/js/agency-swarm-mcp) ![Discord Follow](https://dcbadge.limes.pink/api/server/https://discord.gg/cw2xBaWfFM?style=flat) [![License: MIT with Commons Clause](https://img.shields.io/badge/
license-MIT%20with%20Commons%20Clause-blue.svg)](LICENSE)

**This is a minimal-difference fork of claude-task-master, maintained by VRSEN.**
[![Twitter Follow](https://img.shields.io/twitter/follow/__vrsen__?style=flat)](https://x.com/__vrsen__)
[![Twitter Follow](https://img.shields.io/twitter/follow/nicko_ai?style=flat)](https://x.com/nicko_ai)

A task management system for AI-driven development with Claude, designed to work seamlessly with Cursor AI.

> For agency-swarm projects, the dev_workflow.mdc protocol always applies. All other rules in .cursor/rules are inherited from Task Master unless otherwise noted.

## Requirements

- Anthropic API key (Claude API)
- OpenAI SDK (for Perplexity API integration, optional)

## Quick Start

### Option 1 | MCP (Recommended):

MCP (Model Control Protocol) provides the easiest way to get started with Agency Swarm MCP directly in your editor.

1. **Install the package**

```bash
npm i -g agency-swarm-mcp
```

2. **Add the MCP config to your editor** (Cursor recommended, but it works with other text editors):

```json
{
	"mcpServers": {
		"agency-swarm": {
			"command": "npx",
			"args": ["-y", "agency-swarm-mcp"],
			"env": {
				"ANTHROPIC_API_KEY": "YOUR_ANTHROPIC_API_KEY_HERE",
				"PERPLEXITY_API_KEY": "YOUR_PERPLEXITY_API_KEY_HERE",
				"MODEL": "claude-3-7-sonnet-20250219",
				"PERPLEXITY_MODEL": "sonar-pro",
				"MAX_TOKENS": 64000,
				"TEMPERATURE": 0.2,
				"DEFAULT_SUBTASKS": 5,
				"DEFAULT_PRIORITY": "medium"
			}
		}
	}
}
```

2. **Enable the MCP** in your editor

3. **Prompt the AI** to initialize Agency Swarm MCP:

```
Can you please initialize agency-swarm-mcp into my project?
```

4. **Use common commands** directly through your AI assistant:

```txt
Can you parse my PRD at scripts/prd.txt?
What's the next task I should work on?
Can you help me implement task 3?
Can you help me expand task 4?
```

### Option 2: Using Command Line

#### Installation

```bash
# Install globally
npm install -g agency-swarm-mcp

# OR install locally within your project
npm install agency-swarm-mcp
```

#### Initialize a new project

```bash
# If installed globally
task-master init

# If installed locally
npx task-master-init
```

> **Note:** The CLI command `task-master` is still available for compatibility, but the main entrypoint for MCP is `agency-swarm-mcp`.

This will prompt you for project details and set up a new project with the necessary files and structure.

#### Common Commands

```bash
# Initialize a new project
task-master init

# Parse a PRD and generate tasks
task-master parse-prd your-prd.txt

# List all tasks
task-master list

# Show the next task to work on
task-master next

# Generate task files
task-master generate
```

## Documentation

For more detailed information, check out the documentation in the `docs` directory:

- [Configuration Guide](docs/configuration.md) - Set up environment variables and customize Agency Swarm MCP
- [Tutorial](docs/tutorial.md) - Step-by-step guide to getting started
- [Command Reference](docs/command-reference.md) - Complete list of all available commands
- [Task Structure](docs/task-structure.md) - Understanding the task format and features
- [Example Interactions](docs/examples.md) - Common Cursor AI interaction examples

## Publishing to npm

To publish a new version to npm:

```bash
npm publish --access public
```

## Keeping Your Fork Up-to-Date

To keep your fork in sync with upstream changes:

```bash
git remote add upstream https://github.com/eyaltoledano/claude-task-master.git
git fetch upstream
git merge upstream/main
```

Resolve any conflicts, test, and publish a new npm version if needed.

## Licensing

Agency Swarm MCP is licensed under the MIT License with Commons Clause. This means you can:

✅ **Allowed**:

- Use Agency Swarm MCP for any purpose (personal, commercial, academic)
- Modify the code
- Distribute copies
- Create and sell products built using Agency Swarm MCP

❌ **Not Allowed**:

- Sell Agency Swarm MCP itself
- Offer Agency Swarm MCP as a hosted service
- Create competing products based on Agency Swarm MCP

See the [LICENSE](LICENSE) file for the complete license text and [licensing details](docs/licensing.md) for more information.
