# Trello Power for Kiro

A Kiro Power that integrates the Trello MCP server, enabling you to manage Trello boards, lists, cards, and organizations directly from your development environment.

## Installation

### Option 1: Install via Kiro Powers UI (Recommended)

1. Open Kiro
2. Open the Command Palette (Cmd/Ctrl + Shift + P)
3. Type "Powers: Configure" and press Enter
4. Click "Install from Git URL" in the Powers panel
5. Enter the repository URL: `https://github.com/cargom98/gmkpt`
6. Click Install

The power will be installed to `~/.kiro/powers/trello`

### Option 2: Manual Installation

1. Clone this repository to your Kiro powers directory:
   ```bash
   mkdir -p ~/.kiro/powers
   git clone https://github.com/cargom98/gmkpt ~/.kiro/powers/trello
   ```

2. Ensure `uv` is installed (required for uvx):
   ```bash
   # macOS/Linux
   curl -LsSf https://astral.sh/uv/install.sh | sh
   
   # Or see https://docs.astral.sh/uv/getting-started/installation/
   ```

3. Restart Kiro or reload the Powers panel

## Configuration

### 1. Get Your Trello API Key

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

### 2. Configure the MCP Server

When you first try to use the Trello power, Kiro will prompt you for your API key. Alternatively, you can configure it manually:

1. Open Command Palette (Cmd/Ctrl + Shift + P)
2. Type "MCP: Open Configuration" and press Enter
3. Find or add the `kiro-power-trello` server configuration:
   ```json
   {
     "mcpServers": {
       "kiro-power-trello": {
         "command": "uvx",
         "args": ["trello-mcp-server"],
         "env": {
           "TRELLO_API_KEY": "paste_your_api_key_here"
         }
       }
     }
   }
   ```
4. Save the configuration file

### 3. Authorize the Application

On first use, the Trello MCP server will automatically open your browser to authorize access. Click "Allow" and you're ready to go! The authentication token is cached securely in `~/.trello_mcp_token.json`

## Usage

Once installed and configured, you can ask Kiro to interact with Trello:

- "List all my Trello boards"
- "Show me all lists in the [Board Name] board"
- "Create a card called 'Fix login bug' in the 'Backlog' list"
- "Move the card '[Card Name]' to the 'Done' list"
- "List all my Trello organizations"

See [POWER.md](POWER.md) for detailed workflows, troubleshooting, and advanced usage.

## Requirements

- Kiro IDE
- `uv` package manager (for uvx command)
- Trello account with API key
- Internet connection for OAuth authorization

## Troubleshooting

### Server Not Starting

If the MCP server fails to start:
1. Verify `uv` is installed: `uv --version`
2. Check the MCP Server view in Kiro for error messages
3. Ensure your API key is correctly set in the configuration
4. Restart the server from the MCP Server view

### Authentication Issues

If you encounter authentication problems:
1. Delete `~/.trello_mcp_token.json` and re-authenticate
2. Verify the **Allowed Origins** field includes `http://localhost:8765`
3. Check that you clicked "Allow" in the browser authorization

For more help, see the Troubleshooting section in [POWER.md](POWER.md).

## Files

- `POWER.md` - Complete user documentation and workflows
- `README.md` - This installation guide
- `mcp.json` - MCP server configuration template

## Support

For issues or questions:
- [GitHub Issues](https://github.com/cargom98/gmkpt/issues)
- [Trello API Documentation](https://developer.atlassian.com/cloud/trello/)

## License

See the [upstream repository](https://github.com/cargom98/gmkpt) for license details.
