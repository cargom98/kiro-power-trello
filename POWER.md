---
name: Trello
version: 2.0.1
description: Manage Trello boards, lists, cards, and organizations directly from Kiro. Get your API key at https://trello.com/power-ups/admin/new (free, takes seconds). First use opens browser for OAuth authorization.
author: cargom98
keywords:
  - trello
  - project management
  - boards
  - cards
  - lists
  - kanban
  - task management
  - organization
  - workflow
---

# Trello Power for Kiro

Integrate Trello with Kiro to manage boards, lists, cards, and organizations directly from your development environment.

## Overview

The Trello Power enables you to interact with Trello's project management features without leaving your IDE. Manage your workflow, track tasks, and organize projects seamlessly while coding.

## Features

- **Boards**: List and get board details, list board labels
- **Lists**: List and create board lists
- **Cards**: List, create, and update cards (including moving between lists)
- **Card Members**: Add, remove, and list members assigned to cards
- **Card Labels**: Add, remove, list, and filter cards by labels
- **Board Members**: Add, remove, update, invite, and list board members with permissions
- **Organizations**: Manage workspaces, boards, and team members

## Quick Start

### 1. Get Your Trello API Key

Follow these steps to obtain your API key:

1. Visit [Trello Power-Ups Admin](https://trello.com/power-ups/admin/new)
2. Log in to your Trello account if prompted
3. Fill in the Power-Up creation form:
   - **Power-Up name**: Enter any name (e.g., "Kiro Integration")
   - **Workspace**: Select any workspace (or leave default)
   - **Iframe connector URL**: Leave blank or use a placeholder
   - **Email**: Your email address
4. Click "Create" or "Generate a new API key"
5. Select the App you just created from the list
6. Copy the API key displayed on the screen
7. In the **Allowed Origins** field, add: `http://localhost:8765`
8. Save the changes

This is completely free and takes less than a minute. The API key and allowed origins configuration enable automatic browser-based authentication.

### 2. Configure the Power

When you first use the Trello power, Kiro will automatically prompt you for your API key. Simply paste your API key when asked, and Kiro will configure everything for you automatically.

If you need to update your API key later:

1. Open your MCP configuration (Command Palette → "MCP: Open Configuration")
2. Find the `power-gmkpt-trello` configuration
3. Update the `TRELLO_API_KEY` value

Example configuration:
```json
{
  "mcpServers": {
    "power-gmkpt-trello": {
      "command": "uvx",
      "args": ["trello-mcp-server"],
      "env": {
        "TRELLO_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

### 3. Authenticate

On first use, the server will automatically open your browser to authorize access. Click "Allow" and you're done! The authentication token is cached securely in `~/.trello_mcp_token.json`.

## Common Workflows

### Managing Boards

Ask Kiro to:
- "List all my Trello boards"
- "Show me details for the [Board Name] board"
- "What boards do I have access to?"

### Working with Lists

Ask Kiro to:
- "Show me all lists in the [Board Name] board"
- "Create a new list called 'In Progress' on [Board Name]"
- "What lists are on my project board?"

### Managing Cards

Ask Kiro to:
- "List all cards in the 'To Do' list"
- "Create a card called 'Fix login bug' in the 'Backlog' list"
- "Move the card '[Card Name]' to the 'Done' list"
- "Update the description of card '[Card Name]'"
- "Get details for card '[Card Name]'"
- "Add [Member Name] to the card '[Card Name]'"
- "Remove [Member Name] from card '[Card Name]'"
- "List all members assigned to card '[Card Name]'"
- "Add the 'Bug' label to card '[Card Name]'"
- "Remove the 'Bug' label from card '[Card Name]'"
- "List all labels on card '[Card Name]'"
- "Filter cards on [Board Name] by the 'Priority' label"

### Managing Board Members

Ask Kiro to:
- "List all members of the [Board Name] board"
- "Add [User Email] to the [Board Name] board"
- "Remove [Member Name] from the [Board Name] board"
- "Update [Member Name]'s permission to admin on [Board Name]"
- "Invite [Email] to join the [Board Name] board"

### Managing Board Labels

Ask Kiro to:
- "List all available labels on the [Board Name] board"
- "Show me what labels are available on my project board"

### Organization Management

Ask Kiro to:
- "List all my Trello organizations"
- "Show me details for the [Organization Name] workspace"
- "Show me boards in the [Organization Name] workspace"
- "Who are the members of [Organization Name]?"
- "Add [User Email] to the [Organization Name] organization"
- "Remove [Member Name] from [Organization Name]"

## Authentication Details

The power uses OAuth 1.0a for secure authentication:

- **API Key**: Stored in MCP configuration (safe to share within team)
- **Token**: Cached in `~/.trello_mcp_token.json` with 600 permissions
- **Token Lifetime**: Tokens never expire unless manually revoked
- **Re-authentication**: If needed, delete the token file and restart

### Manual Authentication

If automatic browser authentication doesn't work, check the MCP server logs in Kiro's MCP Server view for authentication instructions.

## Troubleshooting

### Authentication Issues

If you encounter authentication problems:

1. Verify your API key is correct in the MCP configuration
2. Delete `~/.trello_mcp_token.json` and re-authenticate
3. Check that you clicked "Allow" in the browser authorization
4. Ensure you have network access to Trello's API

### Server Not Starting

If the MCP server fails to start:

1. Ensure `uv` is installed (uvx requires it): [Installation Guide](https://docs.astral.sh/uv/getting-started/installation/)
2. Check the MCP Server view in Kiro for error messages
3. Restart the server from the MCP Server view
4. Verify your API key is correctly set in the configuration

### Permission Errors

If you get permission errors:

1. Verify you have access to the board/organization in Trello
2. Re-authenticate to refresh permissions
3. Check that the token file has correct permissions (600)

## Security

- API keys are stored in your MCP configuration (not committed to git)
- Authentication tokens are stored in your home directory with restricted permissions
- Tokens are never committed to version control
- All communication uses HTTPS

## Resources

- [Trello API Documentation](https://developer.atlassian.com/cloud/trello/)
- [Get API Key](https://trello.com/power-ups/admin/new)
- [Manage Tokens](https://trello.com/my/account)
- [GitHub Repository](https://github.com/cargom98/gmkpt)

## Support

For issues or questions:
- Check the [GitHub Issues](https://github.com/cargom98/gmkpt/issues)
- Review the authentication guide in the repository
- Consult Trello's API documentation

## Tips

- Use descriptive card names for easier management
- Organize boards by project or team
- Leverage lists to represent workflow stages
- Use organizations for team collaboration
- Keep your API key secure and never commit it to version control
- Make sure only one MCP server is created
- Make sure the name of the MCP server is kiro-power-trello
