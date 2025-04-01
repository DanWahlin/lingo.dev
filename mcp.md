# Model Context Protocol

[![Install with NPM in VS Code](https://img.shields.io/badge/VS_Code-NPM-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22lingo%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22lingo.dev%22%2C%22mcp%22%2C%22%24%7Binput%3Alingo_api_key%7D%22%5D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22lingo_api_key%22%2C%22description%22%3A%22Lingo.dev%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with NPM in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-NPM-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22lingo%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22lingo.dev%22%2C%22mcp%22%2C%22%24%7Binput%3Alingo_api_key%7D%22%5D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22lingo_api_key%22%2C%22description%22%3A%22Lingo.dev%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D)
[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Docker-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22lingo%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22LINGO_API_KEY%3D%24%7Binput%3Alingo_api_key%7D%22%2C%22lingodev%2Fmcp%22%5D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22lingo_api_key%22%2C%22description%22%3A%22Lingo.dev%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Docker-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22lingo%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22LINGO_API_KEY%3D%24%7Binput%3Alingo_api_key%7D%22%2C%22lingodev%2Fmcp%22%5D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22lingo_api_key%22%2C%22description%22%3A%22Lingo.dev%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D)

The [Model Context Protocol](https://modelcontextprotocol.io/introduction) (MCP) is a standard for connecting Large Language Models (LLMs) to external services. This guide will walk you through how to connect AI tools to Lingo.dev using MCP.

Some of the AI tools that support MCP are:

- [Cursor](https://www.cursor.com/)
- [Claude desktop](https://claude.ai/download)
- [Cline for VS Code](https://github.com/cline/cline)

Connecting these tools to Lingo.dev will allow you to translate apps, websites, and other data using the best LLM models directly in your AI tool.

## Setup

Add this command to your AI tool:

```bash
npx -y lingo.dev mcp <api-key>
```

You can find your API key in [Lingo.dev app](https://lingo.dev/app/), in your project settings.

This will allow the tool to use `translate` tool provided by Lingo.dev. The setup depends on your AI tool and might be different for each tool. Here is setup for some of the tools we use in our team:

### Cursor

1. Open Cursor and go to Cursor Settings.
2. Open MCP tab
3. Click `+ Add new MCP server`
4. Enter the following details:
   - Name: Lingo.dev
   - Type: command
   - Command: `npx -y lingo.dev mcp <api-key>` (use your project API key)
5. You will see green status indicator and "translate" tool available in the list

### Claude desktop

1. Open Claude desktop and go to Settings.
2. Open Developer tab
3. Click `Edit Config` to see configuration file in file explorer.
4. Open the file in text editor
5. Add the following configuration (use your project API key):

```json
{
  "mcpServers": {
    "supabase": {
      "command": "npx",
      "args": ["-y", "lingo.dev", "mcp", "<api-key>"]
    }
  }
}
```

6. Save the configuration file
7. Restart Claude desktop.
8. In the chat input, you will see a hammer icon with your MCP server details.

### VS Code

For the easiest installation, use the one-click install buttons at the top of this page.

For manual installation:

1. Open VS Code
2. Open User Settings (JSON) by pressing `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac) and searching for "Preferences: Open User Settings (JSON)"
3. Add the following configuration (use your project API key):

```json
{
  "mcp.servers": {
    "lingo": {
      "inputs": [
        {
          "id": "lingo_api_key",
          "description": "Lingo.dev API Key",
          "password": true
        }
      ],
      "command": "npx",
      "args": ["-y", "lingo.dev", "mcp", "${input:lingo_api_key}"],
      "env": {}
    }
  }
}
```

You can also use the CLI to add the MCP server:

For VS Code Stable:
```
code --add-mcp '{"name":"lingo","command":"npx","args":["-y","lingo.dev","mcp","${input:lingo_api_key}"],"inputs":[{"id":"lingo_api_key","description":"Lingo.dev API Key","password":true}]}'
```

For VS Code Insiders:
```
code-insiders --add-mcp '{"name":"lingo","command":"npx","args":["-y","lingo.dev","mcp","${input:lingo_api_key}"],"inputs":[{"id":"lingo_api_key","description":"Lingo.dev API Key","password":true}]}'
```

## Usage

You are now able to access Lingo.dev via MCP. You can ask AI tool translate any content via our service.
