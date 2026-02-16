# MCP Configuration Context

## Existing Setup

The Trello MCP server is already configured at the user level with the API key set up. The server configuration is located at `~/.kiro/settings/mcp.json` under the name `power-gmkpt-trello`.

## Important Guidelines

- **Always check existing configs first**: Before configuring or modifying any MCP servers, check the user-level configuration at `~/.kiro/settings/mcp.json` to avoid creating duplicates
- **Config precedence**: User config < workspace configs (later workspaces override earlier ones)
- **Template vs Active Config**: The `mcp.json` file in the workspace root is a template/documentation file, not an active configuration
- **Active server name**: `power-gmkpt-trello` (not `trello`)

## When Working with MCP

1. Check `~/.kiro/settings/mcp.json` before making changes
2. Don't create duplicate server configurations
3. Respect existing API keys and credentials
4. Only modify configs when explicitly requested by the user
