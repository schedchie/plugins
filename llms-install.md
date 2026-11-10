# Install the Schedchie MCP server in Cline

Schedchie is a hosted, remote MCP server at `https://mcp.schedchie.com/mcp` (Streamable HTTP). There is nothing to download, build or run, and no API key: the user signs in with OAuth in the browser, and Cline registers itself with Schedchie.

## Steps

1. In the Cline panel, click the MCP Servers icon in the top toolbar, then the Remote Servers tab.
2. Server Name: `schedchie`. Server URL: `https://mcp.schedchie.com/mcp`. Transport Type: Streamable HTTP. Click Add Server.
3. Cline answers the server's 401 with the OAuth sign-in. The browser opens the Schedchie screen: the user ticks the permission groups Cline may use and signs in. Never ask the user for their password.

The same entry in `cline_mcp_settings.json` (Configure MCP Servers):

```json
{
  "mcpServers": {
    "schedchie": {
      "type": "streamableHttp",
      "url": "https://mcp.schedchie.com/mcp",
      "disabled": false
    }
  }
}
```

From the Cline CLI, `cline mcp add schedchie https://mcp.schedchie.com/mcp --transport http --yes` saves the server; then `cline mcp` and Authorize OAuth signs in.

## Check it

Ask Cline: "Call whoami, then list_accounts." It should name the signed-in Schedchie user and list the connected social accounts.

## Requirements

A Schedchie account with an active plan or trial (https://www.schedchie.com). Social accounts are connected in the Schedchie web app, not in Cline. Setup notes for every client: https://www.schedchie.com/ai/cline
