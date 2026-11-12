# Schedchie for AI assistants

Plugins, extensions, an agent skill and setup steps that connect AI assistants to [Schedchie](https://www.schedchie.com), the flat-price social media scheduler, through its hosted MCP server. This repository holds configuration and instructions only. The Schedchie service and its command-line client are not open source and are not in it.

- **Server:** `https://mcp.schedchie.com/mcp` (Streamable HTTP)
- **Sign-in:** OAuth in your browser on schedchie.com. The assistant registers itself, so there is no key, client ID or password to paste. A few clients cannot do OAuth yet and take a connection token you create yourself in the Schedchie dashboard; their sections below link to those steps. If you signed up with Google, the sign-in page explains how to sign in with such a token.
- **Needs:** a Schedchie account with an active plan or trial. Social accounts are connected in the Schedchie web app.

## What the assistant can do

You and the assistant write the post; Schedchie schedules it and publishes it at the time you set. Once connected, the assistant can:

- list your connected accounts and say which ones need a reconnect
- schedule, edit, reschedule, retry and delete posts, on one account or many in one call, with different text per network
- upload images and video from a link, or hand you an upload link for a file on your computer
- read analytics on Instagram, Facebook, TikTok, LinkedIn, Pinterest, YouTube, Threads, Bluesky, Mastodon, Telegram, Google Business Profile and Discord: followers, posts published and the per-post numbers each network reports
- approve or reject teammates' posts held for your review, and manage members (the workspace owner, on Ultra and higher plans)
- create client review links, on every plan (a team member needs the owner's permission to share them)
- read and answer comments on published posts
- keep notes, publishing presets and account groups

On the sign-in screen you choose what the connection may do, in six groups: Schedule and edit posts; Upload media; Read analytics; Team and approvals; Notes, presets and groups; Comments, mentions and reviews. A tool outside the groups you ticked does not exist for that connection. Deleting a post, removing a member or disconnecting an account is marked destructive, and the skill in this repository tells the assistant to ask you first.

Networks: Instagram, Facebook, TikTok, LinkedIn, Pinterest, YouTube, Threads, Bluesky, Mastodon, Telegram, Google Business Profile, Discord, Slack, WordPress, Dev.to, Hashnode, Ghost, Pixelfed, Listmonk and X. Posting to X is included in every paid plan under fair use. The current list and the setup for every client: https://www.schedchie.com/ai

## What is sent where

Nothing in this repository runs on install or sends anything by itself. When you ask your assistant to act, it calls tools on `mcp.schedchie.com` over HTTPS with the OAuth token from your sign-in, carrying whatever you ask it to act on: post text, times, account choices, media files or links, comment replies, notes and presets, and the email addresses of people you invite. Schedchie then publishes to the networks you connected in its web app. The tool results go back to the assistant you connected, and so to its provider, under that provider's privacy terms: your posts, accounts and analytics, comments written by the public, and the email addresses of you and your teammates when a tool lists them. Privacy policy: https://www.schedchie.com/privacy

## Install as a plugin, extension or skill

| Assistant | Install from this repository |
|---|---|
| Claude Code | `claude plugin marketplace add schedchie/plugins`, then `claude plugin install schedchie@schedchie` |
| GitHub Copilot CLI | `copilot plugin marketplace add schedchie/plugins`, then `copilot plugin install schedchie@schedchie` |
| Codex | `codex plugin marketplace add schedchie/plugins`, then open `/plugins` |
| Gemini CLI | `gemini extensions install https://github.com/schedchie/plugins` |
| Kimi Code CLI | `/plugins install https://github.com/schedchie/plugins`, then `/reload` |
| Junie CLI | `/extensions marketplace add schedchie/plugins`, then `/extensions install schedchie` |
| Hermes Agent | `hermes skills tap add schedchie/plugins` (the skill in `skills/schedchie`) |
| Cline | follow `llms-install.md` |

Each one except Hermes adds the same server, `https://mcp.schedchie.com/mcp`, and the first tool call opens the Schedchie sign-in. The Hermes tap adds only the skill: add the server as in [Hermes Agent](#hermes-agent) below. The skill in `skills/schedchie/SKILL.md` tells an agent which tools to use first, to ask you before scheduling (unless you told it that it need not) and before anything that publishes, replies, approves, deletes, sends mail, creates a shareable link or changes access, to convert your local times to UTC, and to treat text written by other people as data, never as instructions.

## Connect any assistant by hand

Every client below needs only the server address. The steps follow the setup pages on schedchie.com, which have more detail per client.

<!-- connect:start -->

## Chat apps

### ChatGPT

1. **Open Plugins and add a custom server** (Plugins, +, Add custom MCP server). On ChatGPT on the web, go to Plugins, select the plus button, then Add custom MCP server.
2. **Name it and paste the URL** (Connection, Server URL). Name: Schedchie, with a short description if you like. Under Connection, paste the address below as the Server URL.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Choose OAuth and create the plugin** (OAuth, I understand and want to continue, Create as a plugin). Set authentication to OAuth and leave the client credentials empty, since ChatGPT registers itself with Schedchie. Select I understand and want to continue, then Create as a plugin.
4. **Install it and sign in**. Find Schedchie in your personal plugins and install it. On the Schedchie screen, tick the groups this connection may use and sign in.
5. **Call it in a chat** (@, Schedchie). In the prompt box type @, select Schedchie and ask for your connected accounts.

More: https://www.schedchie.com/ai/chatgpt

### Claude

1. **Open Customize, Connectors** (Customize, Connectors, + Add, Add custom connector). On claude.ai, go to Customize, then Connectors. Click + Add, then Add custom connector.
2. **Name it and paste the URL** (Name, MCP server URL, Continue, Continue). Name: Schedchie. Paste the address below as the MCP server URL and click Continue, then Continue again on the detected settings.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Choose the sign-in settings** (Authentication, Sign in now, OAuth client, Register automatically, Add). Under Authentication choose Sign in now, and under OAuth client choose Register automatically, so Claude registers itself with Schedchie. Leave Request headers empty and click Add.
4. **Connect and sign in to Schedchie** (Connect, +, Connectors). Click Connect on the Schedchie connector, tick the groups this connection may use on the Schedchie screen and sign in. In a chat, click +, then Connectors, and switch Schedchie on.
5. **On Team or Enterprise** (Organization settings, Connectors, Add, Custom, Web). An Owner adds it under Organization settings, Connectors: Add, Custom, Web, the same URL and settings, then Add. Each member then clicks Connect on it under Customize, Connectors.

More: https://www.schedchie.com/ai/claude

### Claude Cowork

1. **Add Schedchie under Customize, Connectors** (Customize, Connectors, + Add, Add custom connector). On claude.ai or in the desktop app, open Customize, then Connectors, and click + Add, then Add custom connector.
2. **Name it and paste the URL** (Name, MCP server URL, Continue, Continue, Sign in now, Register automatically, Add). Name: Schedchie. Paste the address below as the MCP server URL and click Continue twice. Choose Authentication Sign in now and OAuth client Register automatically, then click Add.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Connect and sign in** (Connect). Click Connect on the Schedchie connector, tick the groups this connection may use and sign in.
4. **Start a Cowork task** (Cowork). In the message box, select Cowork in the bottom left and describe the week of posts. With the new Claude experience there is no Cowork option: describe the task in any conversation, and approve Schedchie tools when Cowork asks.

More: https://www.schedchie.com/ai/claude-cowork

### Claude Desktop

1. **Open Customize, Connectors** (Customize, Connectors). In the Claude desktop app, open Customize, then Connectors. A Schedchie connector you added on claude.ai is already listed, so skip to the last step.
2. **Add a custom connector** (+ Add, Add custom connector, Name, MCP server URL, Continue, Continue). Click + Add, then Add custom connector. Name: Schedchie. Paste the address below as the MCP server URL, then click Continue twice.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Choose the sign-in settings** (Authentication, Sign in now, OAuth client, Register automatically, Add). Under Authentication choose Sign in now, and under OAuth client choose Register automatically. Click Add.
4. **Connect and turn it on** (Connect, +, Connectors). Click Connect on the Schedchie connector, tick the groups this connection may use and sign in. In a chat, click +, then Connectors, and switch Schedchie on.

More: https://www.schedchie.com/ai/claude-desktop

### Perplexity

1. **Open Add MCP connector** (Plugins, Add custom, Add MCP connector, Remote). Open Plugins in the sidebar (or Customize, Connectors if Plugins is not there yet), then Add custom, Add MCP connector, and choose Remote.
2. **Name it and paste the URL** (Name, MCP server URL). Name: Schedchie. Paste the address below as the MCP server URL.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Set Advanced, then Add** (Advanced, Authentication, OAuth, Transport, Streamable HTTP, Add). Under Advanced set Authentication to OAuth and Transport to Streamable HTTP, leave Network access on Public and leave Client ID and Client Secret empty. Tick the acknowledgement and select Add.
4. **Sign in from the connector card** (Plugins, Schedchie). On the Plugins page, select the Schedchie card to start the sign-in, then tick the groups and sign in. Name it in a request, such as: Using Schedchie, list my connected accounts.
5. **In an organization** (Organization settings, Connectors, Custom connector). An admin adds it under Organization settings, Connectors, Custom connector and turns it on there, since organization connectors start off. Members add their own only after an admin turns on Allow members to add custom connectors.

More: https://www.schedchie.com/ai/perplexity

### Mistral Le Chat

1. **Open Connectors in Vibe** (Connectors, + Add Connector, Custom MCP Connector). On chat.mistral.ai (Le Chat is now Mistral Vibe), open the Connectors page, click + Add Connector and switch to the Custom MCP Connector tab.
2. **Name it and paste the URL** (Connector name, Server URL, Description). Connector name: schedchie, with no spaces or special characters. Paste the address below as the Server URL; Description is optional.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Connect and sign in** (Connect). Click Connect. Vibe detects OAuth 2.1 with dynamic client registration and takes you to the Schedchie screen: tick the groups and sign in.

More: https://www.schedchie.com/ai/mistral-le-chat

### Manus

This client takes a connection token instead of the OAuth sign-in. Steps: https://www.schedchie.com/ai/manus

### Gemini app

1. **Open Connected Apps** (Settings, Connected Apps). On gemini.google.com in a desktop browser, click Settings, then Connected Apps.
2. **Add a custom app** (Custom apps, Add a custom app, Next). Under Custom apps, paste the address below into the Add a custom app link to get started field, or click Add a custom app if you already have one. Leave Advanced features closed and click Next.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Sign in to Schedchie**. Follow the on-screen steps to the Schedchie screen, tick the groups Gemini may use and sign in.
4. **Call it in a chat** (@, Schedchie). Enter @, select Schedchie and ask, on the web or in the mobile app.

More: https://www.schedchie.com/ai/gemini

### Grok

1. **Open Connectors in Grok** (New Connector, Custom). Go to grok.com/connectors, click New Connector, then select Custom.
2. **Paste the Schedchie URL**. Enter the address below as the MCP server URL.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Sign in to Schedchie**. Complete the sign-in Grok asks for on the Schedchie screen, ticking what Grok may use. Grok then uses the Schedchie tools whenever a request needs them.
4. **On Business and Enterprise** (Grok Business, Connectors, + Add Connector, Other). A team admin first adds it at console.x.ai: select the team, then Grok Business, Connectors, + Add Connector, Other, and the Schedchie URL. Members then connect at grok.com/connectors.

More: https://www.schedchie.com/ai/grok

### Muse

1. **Ask Muse for a custom connector**. In a Muse chat, ask it to create a Custom Connector for Schedchie at the address below.

   ```text
   Create a Custom Connector for Schedchie, the MCP server at https://mcp.schedchie.com/mcp.
   ```
2. **Muse Code: add it to settings.json**. In ~/.config/muse/settings.json, add a schedchie entry to mcp_servers with the streamable_http transport.

   ```json
   {
     "schema_version": 1,
     "mcp_servers": {
       "schedchie": { "transport": "streamable_http", "url": "https://mcp.schedchie.com/mcp" }
     }
   }
   ```
3. **Muse Code: sign in**. Run this and finish the Schedchie sign-in in your browser.

   ```text
   muse mcp login schedchie
   ```

If it asks for a token instead of the sign-in: https://www.schedchie.com/ai/muse

### DeepSeek

No direct route today. Details: https://www.schedchie.com/ai/deepseek

## Coding agents, editors and terminals

### Claude Code

1. **Add the server**. Run it in your project folder. It is saved for you in that project; add --scope user to have it in every project.

   ```bash
   claude mcp add --transport http schedchie https://mcp.schedchie.com/mcp
   ```
2. **Sign in**. Your browser opens the Schedchie screen, where you tick what Claude Code may use and sign in. Over SSH it prints the link instead: open it on your computer and paste back the address the browser lands on. Inside a session, /mcp does the same.

   ```bash
   claude mcp login schedchie
   ```
3. **Check it, then call list_accounts**. claude mcp get schedchie shows whether it still needs the sign-in. Then start claude and ask for your connected Schedchie accounts.

   ```bash
   claude mcp get schedchie
   ```
4. **Already connected on claude.ai** (/mcp). If Claude Code is signed in with your claude.ai account, a Schedchie connector added at claude.ai/customize/connectors already shows in /mcp. Nothing to add.

More: https://www.schedchie.com/ai/claude-code

### Cursor

1. **Add Schedchie to mcp.json** (.cursor/mcp.json). Open .cursor/mcp.json in your project, or ~/.cursor/mcp.json for every project, and add this entry. Leave out headers and auth: Cursor registers itself with Schedchie.

   ```json
   {
     "mcpServers": {
       "schedchie": {
         "url": "https://mcp.schedchie.com/mcp"
       }
     }
   }
   ```
2. **Turn it on in Customize** (Customize). Open Customize in the sidebar. Schedchie is listed with your MCP servers; make sure its toggle is on.
3. **Sign in to Schedchie**. Start the sign-in Cursor shows for Schedchie. Your browser opens the Schedchie screen: tick the groups Cursor may use and sign in.
4. **Call list_accounts in Agent chat**. In Agent chat, ask Cursor to list your Schedchie accounts.

More: https://www.schedchie.com/ai/cursor

### Codex

1. **Add the server**. It writes [mcp_servers.schedchie] to ~/.codex/config.toml, which the Codex CLI, the IDE extension and the ChatGPT desktop app share. OAuth is the default, so the URL is all it needs.

   ```bash
   codex mcp add schedchie --url https://mcp.schedchie.com/mcp
   ```
2. **Sign in**. Your browser opens the Schedchie screen, where you tick what Codex may use. Without a local browser, add --no-browser, open the printed link and paste the full redirect URL back into the terminal.

   ```bash
   codex mcp login schedchie
   ```
3. **Or add it in the IDE extension** (MCP servers, Add server, Streamable HTTP, Save, Restart extension, Authenticate). Open the gear menu and choose MCP servers, then Add server. Name it schedchie, choose Streamable HTTP and paste the URL, save, restart the extension and select Authenticate. The ChatGPT desktop app has the same form under Settings, MCP servers.

   ```text
   https://mcp.schedchie.com/mcp
   ```
4. **Check it, then call list_accounts**. In a codex session, /mcp lists schedchie as active. Then ask Codex for your connected Schedchie accounts.

   ```text
   /mcp
   ```

More: https://www.schedchie.com/ai/codex

### VS Code

1. **Open MCP Servers** (Chat: Open Customizations, MCP Servers, Add Server (+)). With Copilot selected in the Session Target dropdown, run Chat: Open Customizations from the Command Palette, select MCP Servers, then Add Server (+) in the User group. MCP: Add Server starts the same flow.
2. **Choose HTTP and paste the URL** (HTTP (HTTP or Server-Sent Events)). Choose HTTP (HTTP or Server-Sent Events), paste the Schedchie URL and enter schedchie as the server ID.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Save it for every workspace** (Global, Copilot Global). Select Global, then Copilot Global. VS Code writes this entry to ~/.copilot/mcp-config.json.

   ```json
   {
     "mcpServers": {
       "schedchie": {
         "type": "http",
         "url": "https://mcp.schedchie.com/mcp"
       }
     }
   }
   ```
4. **Sign in to Schedchie**. Accept the trust and sign-in prompts. Your browser opens the Schedchie screen: tick the groups Copilot may use and sign in.
5. **Call list_accounts in Copilot chat**. In Copilot chat, ask for your connected Schedchie accounts. That runs list_accounts, which returns the account ids the other Schedchie tools take.

More: https://www.schedchie.com/ai/vscode

### Hermes Agent

1. **Add the server**. In ~/.hermes/config.yaml, under mcp_servers. auth: oauth lets Hermes register itself with Schedchie.

   ```yaml
   mcp_servers:
     schedchie:
       url: "https://mcp.schedchie.com/mcp"
       auth: oauth
   ```
2. **Sign in from a new terminal**. Hermes prints an authorize link and opens the Schedchie screen, where you tick what Hermes may use. Over SSH, open the link on any device and paste the redirect address back when it asks.

   ```bash
   hermes mcp login schedchie
   ```
3. **Check it, then call list_accounts**. The test reports what Schedchie answered. In a session that was already running, /reload-mcp loads the server. Then ask Hermes for your connected Schedchie accounts.

   ```bash
   hermes mcp test schedchie
   ```
4. **Add the Schedchie skill**. Optional. It tells Hermes which Schedchie tools to use first and to show you each post before it is scheduled. It holds no credentials.

   ```bash
   hermes skills install well-known:https://www.schedchie.com/.well-known/skills/schedchie
   ```

More: https://www.schedchie.com/ai/hermes-agent

### Gemini CLI

1. **Add the server**. --transport http makes it a Streamable HTTP server. -s user writes ~/.gemini/settings.json for every project instead of .gemini/settings.json in this one.

   ```bash
   gemini mcp add --transport http -s user schedchie https://mcp.schedchie.com/mcp
   ```
2. **Or write it in settings.json**. The key is httpUrl. Gemini CLI reads url as an SSE endpoint, the wrong transport for Schedchie.

   ```json
   { "mcpServers": { "schedchie": { "httpUrl": "https://mcp.schedchie.com/mcp" } } }
   ```
3. **Sign in**. Start gemini and run it. Gemini CLI finds the sign-in itself and opens the Schedchie screen in your browser, where you tick what it may use. It needs a browser on the same machine, so not over SSH without X11 forwarding or in a container.

   ```text
   /mcp auth schedchie
   ```
4. **Check it, then call list_accounts**. /mcp shows schedchie with its tools; gemini mcp list does the same from the shell. Then ask Gemini CLI for your connected Schedchie accounts.

   ```text
   /mcp
   ```

More: https://www.schedchie.com/ai/gemini-cli

### Grok Build

1. **Add the server**. It writes ~/.grok/config.toml. Add --scope project to write .grok/config.toml in the current folder instead.

   ```bash
   grok mcp add --transport http schedchie https://mcp.schedchie.com/mcp
   ```
2. **Or edit config.toml**. The same entry by hand. Leave out headers: the sign-in supplies the token.

   ```toml
   [mcp_servers.schedchie]
   url = "https://mcp.schedchie.com/mcp"
   ```
3. **Sign in** (/mcps, schedchie, i). In Grok Build, type /mcps to open the MCP tab, select schedchie and press i. The browser opens the Schedchie screen, where you tick what Grok may use. Grok also starts this sign-in on first use.

   ```text
   /mcps
   ```
4. **Check it, then call list_accounts**. grok mcp doctor checks the config and the connection. Then ask Grok Build for your connected Schedchie accounts.

   ```bash
   grok mcp doctor schedchie
   ```

More: https://www.schedchie.com/ai/grok-build

### Kimi Code CLI

1. **Add the server**. In ~/.kimi-code/mcp.json for every project, or .kimi-code/mcp.json for one repository. An entry with a url and no transport is an HTTP server. /mcp-config in Kimi Code adds it without editing the file.

   ```json
   { "mcpServers": { "schedchie": { "url": "https://mcp.schedchie.com/mcp" } } }
   ```
2. **Start a new session and sign in**. A server added to mcp.json joins sessions started after the change, so start kimi afresh, then run the login. The browser opens the Schedchie screen, where you tick what Kimi Code may use.

   ```text
   /mcp-config login schedchie
   ```
3. **Check it, then call list_accounts**. /mcp shows the connection state of every server. Then ask Kimi Code for your connected Schedchie accounts.

   ```text
   /mcp
   ```

More: https://www.schedchie.com/ai/kimi-code

### Windsurf

1. **Add Schedchie to mcp_config.json**. Devin Desktop (formerly Windsurf) gives its agent, Devin Local, the servers in ~/.config/devin/mcp_config.json, or %APPDATA%\devin\mcp_config.json on Windows. Add this entry there, or in .devin/mcp_config.json to share it with a project.

   ```json
   {
     "mcpServers": {
       "schedchie": {
         "url": "https://mcp.schedchie.com/mcp",
         "transport": "http"
       }
     }
   }
   ```
2. **Find it under MCPs** (Customize, MCPs, Install MCPs for, This computer). Open Customize in the agent sidebar, then MCPs. With Install MCPs for set to This computer, schedchie is listed; make sure its toggle is on.
3. **Sign in to Schedchie** (Needs authentication, Authenticate). Devin Local asks you to authenticate the first time it uses the server. Your browser opens the Schedchie screen: tick the groups and sign in. If schedchie later shows Needs authentication, press Authenticate.
4. **Call list_accounts in Devin Local**. Ask Devin Local to list your Schedchie accounts.

More: https://www.schedchie.com/ai/windsurf

### goose

1. **Desktop: add a custom extension** (Extensions, Add custom extension, Streamable HTTP, Add). Click Extensions in the sidebar, then Add custom extension. Choose the Streamable HTTP type, name it Schedchie, paste the URL and click Add.

   ```text
   https://mcp.schedchie.com/mcp
   ```
2. **CLI: add a remote extension** (Add Extension, Remote Extension (Streamable HTTP)). Choose Add Extension, then Remote Extension (Streamable HTTP). Call it schedchie, paste the URL as the endpoint URI, keep the timeout and answer No to custom headers. It is saved in ~/.config/goose/config.yaml.

   ```bash
   goose configure
   ```
3. **Sign in**. An OAuth window opens in your browser the first time goose uses Schedchie: the Schedchie screen, where you tick what goose may use. goose gets its own client ID from Schedchie, so there is nothing to fill in.
4. **Call list_accounts**. In a new chat, ask goose for your connected Schedchie accounts. For one session only, goose session --with-streamable-http-extension with the URL loads it without saving.

More: https://www.schedchie.com/ai/goose

### opencode

1. **Add the server**. --global puts it in your global opencode config; leave it out to keep Schedchie to this project.

   ```bash
   opencode mcp add schedchie --global --url https://mcp.schedchie.com/mcp
   ```
2. **Or write opencode.json**. The same entry by hand, under mcp.servers. OAuth is on by default, so the type and the URL are all it needs.

   ```json
   {
     "$schema": "https://opencode.ai/config.json",
     "mcp": {
       "servers": {
         "schedchie": {
           "type": "remote",
           "url": "https://mcp.schedchie.com/mcp"
         }
       }
     }
   }
   ```
3. **Sign in** (/mcps, schedchie). opencode mcp list shows schedchie as needs authentication. Open opencode, type /mcps and select schedchie, or run the command below. The browser opens the Schedchie screen, where you tick what opencode may use. Over SSH, paste the failed callback page's address into the sign-in prompt.

   ```bash
   opencode mcp auth schedchie
   ```
4. **Check it, then call list_accounts**. opencode mcp list shows schedchie connected. Then ask opencode for your connected Schedchie accounts.

   ```bash
   opencode mcp list
   ```

More: https://www.schedchie.com/ai/opencode

### Zed

1. **Open MCP Servers** (Settings, AI, MCP Servers, Add Server, Add Remote Server). Open Settings, then AI, then MCP Servers (or run agent: open settings and select MCP Servers). Click Add Server, then Add Remote Server.
2. **Enter the Schedchie server**. Give it the Schedchie URL and no Authorization header. Zed saves the entry under context_servers in your settings file (zed: open settings file).

   ```json
   {
     "context_servers": {
       "schedchie": {
         "url": "https://mcp.schedchie.com/mcp"
       }
     }
   }
   ```
3. **Sign in to Schedchie**. With no Authorization header, Zed prompts you to authenticate. Your browser opens the Schedchie screen: tick the groups the agent may use and sign in.
4. **Check it, then call list_accounts**. In MCP Servers the dot next to schedchie turns green and its tooltip says Server is active. Then ask the agent in the Agent Panel to list your Schedchie accounts.

More: https://www.schedchie.com/ai/zed

### Junie CLI

1. **Add Schedchie to mcp.json**. Put this entry in ~/.junie/mcp/mcp.json for every project, or .junie/mcp/mcp.json at the project root. Junie imports it and enables it by default.

   ```json
   {
     "mcpServers": {
       "schedchie": {
         "url": "https://mcp.schedchie.com/mcp"
       }
     }
   }
   ```
2. **Open /mcp** (/mcp). Run /mcp in Junie. schedchie is listed with the status Authorization required.

   ```text
   /mcp
   ```
3. **Authorize** (schedchie, Authorize). Select schedchie, then Authorize. Your browser opens the Schedchie screen: tick the groups Junie may use and sign in. The status changes to Active.

More: https://www.schedchie.com/ai/junie

### GitHub Copilot CLI

1. **Add the server**. It writes ~/.copilot/mcp-config.json. No header: the sign-in supplies the token.

   ```bash
   copilot mcp add --transport http schedchie https://mcp.schedchie.com/mcp
   ```
2. **Or use the form in copilot** (/mcp add, Server Name, Server Type, HTTP, URL, Tools). Enter /mcp add, name it schedchie, pick HTTP as the server type and paste the URL. Leave HTTP Headers empty and Tools at *, then press Ctrl+S.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Sign in**. In copilot, run it. The browser opens the Schedchie screen, where you tick what Copilot may use, and the server reconnects on its own.

   ```text
   /mcp auth schedchie
   ```
4. **Check it, then call list_accounts**. /mcp show schedchie lists its tools. Then ask Copilot for your connected Schedchie accounts.

   ```text
   /mcp show schedchie
   ```

More: https://www.schedchie.com/ai/copilot-cli

### JetBrains AI Assistant

This client cannot sign in to a remote server with OAuth yet, so its setup runs a local bridge program. Steps: https://www.schedchie.com/ai/jetbrains-ai-assistant

### Cline

1. **Open Remote Servers** (MCP Servers, Remote Servers). In the Cline panel, click the MCP Servers icon in the top toolbar, then the Remote Servers tab.
2. **Add the server** (Server Name, Server URL, Transport Type, Streamable HTTP, Add Server). Server Name: schedchie. Server URL: the Schedchie URL. Transport Type: Streamable HTTP. Then click Add Server.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Sign in to Schedchie**. Cline answers Schedchie's 401 with the OAuth sign-in and registers itself. Your browser opens the Schedchie screen: tick the groups Cline may use and sign in.
4. **Or from the Cline CLI** (Authorize OAuth). The first command saves the server. Then run cline mcp and choose Authorize OAuth to sign in.

   ```bash
   cline mcp add schedchie https://mcp.schedchie.com/mcp --transport http --yes
   cline mcp
   ```

More: https://www.schedchie.com/ai/cline

### Continue

This client takes a connection token instead of the OAuth sign-in. Steps: https://www.schedchie.com/ai/continue

### Warp

1. **Open MCP servers** (Settings, Agents, MCP servers). Or search Open MCP Servers in the Command Palette, or go to Warp Drive, Personal, MCP Servers.
2. **Add the server** (+ Add, Streamable HTTP or SSE Server (URL)). Click + Add, choose Streamable HTTP or SSE Server (URL) and paste the entry. No headers: the sign-in supplies the token.

   ```json
   {
     "schedchie": {
       "url": "https://mcp.schedchie.com/mcp"
     }
   }
   ```
3. **Start and sign in** (Start). Click Start.
4. **Call list_accounts** (View Logs). Ask Warp's agent for your connected Schedchie accounts. If the server does not start, View Logs on the server shows why.

More: https://www.schedchie.com/ai/warp

## Agent gateways and automation

### OpenClaw

1. **Stop the Gateway**. The openclaw mcp commands that save a server, sign in or probe run only while the local Gateway is stopped.

   ```bash
   openclaw gateway stop
   ```
2. **Add the server**. It writes mcp.servers.schedchie. Keep transport streamable-http: without it, OpenClaw assumes SSE.

   ```bash
   openclaw mcp set schedchie '{"url":"https://mcp.schedchie.com/mcp","transport":"streamable-http","auth":"oauth","enabled":true}'
   ```
3. **Sign in**. Open the link it prints: the Schedchie screen, where you tick what OpenClaw may use. OpenClaw catches the redirect itself; if the browser cannot reach it, run the --code command it prints.

   ```bash
   openclaw mcp login schedchie
   ```
4. **Check it and start the Gateway**. The probe lists the Schedchie tools. Then start the Gateway and ask OpenClaw from your chat app for your connected Schedchie accounts.

   ```bash
   openclaw mcp probe schedchie
   openclaw gateway start
   ```
5. **Or from the Control UI** (Settings, MCP, Configured servers, Add server, Streamable HTTP, Add server, Sign in). With the Gateway running: add schedchie with the URL, set auth to oauth in the scoped config editor on the same page, then select Sign in on the server and approve in the browser.

   ```text
   https://mcp.schedchie.com/mcp
   ```

More: https://www.schedchie.com/ai/openclaw

### Paperclip

1. **Connect your own MCP server** (Connectors, Connect your own MCP server). In the left sidebar, select Connectors, choose Connect your own MCP server and paste the Schedchie URL. Paperclip sees that Schedchie uses OAuth and registers itself.

   ```text
   https://mcp.schedchie.com/mcp
   ```
2. **Choose who may use it** (Which humans can use this credential?, Just me, Which agents can use this connection?, Just agents I pick). Pick Just me, then Just agents I pick, and select the agents that should post.
3. **Sign in**. Paperclip opens the browser sign-in: the Schedchie screen, where you tick what this connection may use.
4. **Set permissions and test** (Permissions, Ask first). Set writes to Ask first if a post should wait for your yes, then give an agent a task and check the connector's activity.
5. **Or through the agent's own runtime**. For claude_local: as the OS user that runs the heartbeat, add Schedchie to Claude Code, then run claude, type /mcp and finish the sign-in once.

   ```bash
   claude mcp add --transport http --scope user schedchie https://mcp.schedchie.com/mcp
   ```

More: https://www.schedchie.com/ai/paperclip

### NanoClaw

This client takes a connection token instead of the OAuth sign-in. Steps: https://www.schedchie.com/ai/nanoclaw

### OpenAI dots

1. **Add Schedchie to ChatGPT** (Plugins, +, Add custom MCP server, Connection, Server URL). On ChatGPT on the web, go to Plugins, select the plus button, then Add custom MCP server. Name it Schedchie and paste the address below as the Server URL under Connection.

   ```text
   https://mcp.schedchie.com/mcp
   ```
2. **Choose OAuth and create the plugin** (OAuth, I understand and want to continue, Create as a plugin). Set authentication to OAuth, select I understand and want to continue, then Create as a plugin.
3. **Install it and sign in**. Install Schedchie from your personal plugins, then tick the groups on the Schedchie screen and sign in. Your dot uses the plugins installed and connected on your account.
4. **Give your dot the job**. Message your dot what to post and when, such as the weekly digest every Monday at 8:00. It schedules through the Schedchie plugin.

More: https://www.schedchie.com/ai/openai-dots

### Claude Duet

1. **Add Schedchie on claude.ai** (Customize, Connectors, + Add, Add custom connector). Go to Customize, then Connectors, and click + Add, then Add custom connector.
2. **Name it and paste the URL** (Name, MCP server URL, Continue, Continue, Sign in now, Register automatically, Add). Name: Schedchie. Paste the address below as the MCP server URL and click Continue twice. Choose Authentication Sign in now and OAuth client Register automatically, then click Add.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Connect and sign in** (Connect). Click Connect on the Schedchie connector, tick the groups your Claude account may use and sign in.
4. **Hand Duet the job**. Duet uses the connectors on your Claude account, so Schedchie is already there. Message it what to post and when, such as the week's posts every Monday from your changelog.

More: https://www.schedchie.com/ai/claude-duet

### Grok Bot

1. **Ask a Bot to add Schedchie**. In a Grok Bot chat, ask it to add the Schedchie MCP server by URL.

   ```text
   Add the MCP server https://mcp.schedchie.com/mcp as an app named Schedchie.
   ```
2. **Sign in to Schedchie** (Connect, Authorize). When the Bot shows a Connect card or asks you to Authorize, finish the Schedchie sign-in in your browser and tick what your Bots may use. If it stalls, choose Reopen on the card.
3. **Check it is installed** (Connect apps, Installed). Open Connect apps in the sidebar (on mobile, your avatar, then Connect apps) and confirm Schedchie is under Installed. Apps are account-wide, so every Bot you run can use it.
4. **Give a Bot the job** (@, Schedchie). Type @ to attach Schedchie to the task and say what to post and when, such as a LinkedIn and a Bluesky post for each new blog post.

More: https://www.schedchie.com/ai/grok-bot

### Cue

1. **Ask Cue to add Schedchie**. Send Cue this message. If it asks whether the server is a URL or a command, answer URL.

   ```text
   Add the MCP server https://mcp.schedchie.com/mcp as a connector named Schedchie. It is a URL over HTTP and signs in with OAuth.
   ```
2. **Sign in to Schedchie**. Cue opens the Schedchie screen in your browser. Tick what Cue may use and sign in.
3. **Give it the schedule**. Tell Cue what to post and when, such as the week's digest every Monday at 8:00.

More: https://www.schedchie.com/ai/cue

### n8n

1. **Add the MCP Client Tool** (AI Agent, Tool, MCP Client Tool). In a workflow with an AI Agent node, click its Tool connector and add MCP Client Tool.
2. **Point it at Schedchie** (Endpoint, Server Transport, HTTP Streamable). Endpoint: the Schedchie URL. Server Transport: HTTP Streamable.

   ```text
   https://mcp.schedchie.com/mcp
   ```
3. **Sign in with MCP OAuth2** (Authentication, MCP OAuth2, Credentials, Use Dynamic Client Registration, Connect my account). Authentication: MCP OAuth2. Create a new credential, keep Use Dynamic Client Registration on and click Connect my account. The Schedchie screen opens: tick the groups and sign in.
4. **Pick the tools** (Tools to Include, All, Selected). Tools to Include: All, or Selected to give the agent only the Schedchie tools the workflow needs.

More: https://www.schedchie.com/ai/n8n

## Your own agent

### Claude API and Agent SDK

This client takes a connection token instead of the OAuth sign-in. Steps: https://www.schedchie.com/ai/claude-api

### OpenAI Responses API

This client takes a connection token instead of the OAuth sign-in. Steps: https://www.schedchie.com/ai/openai-responses-api

## Command line

### Schedchie CLI

1. **Install it**. From npm, on Node.js 20.3 or later. Or skip the install and put npx in front of every command.

   ```bash
   npm install -g schedchie
   ```
2. **Sign in**. Your browser opens the Schedchie screen, where you tick what the CLI may use and approve; the terminal prints Signed in. On a server or over SSH, add --no-browser, open the printed link on any computer and paste back the address the browser lands on.

   ```bash
   schedchie login
   ```
3. **Check it**. Your profile, then your connected accounts as JSON.

   ```bash
   schedchie whoami
   schedchie list-accounts --json
   ```
4. **Schedule a post**. Upload a local photo or video, then pass the descriptor it prints to schedule-post.

   ```bash
   schedchie upload ./photo.jpg --json
   schedchie schedule-post --account-ids <accountId> --text "Hello from the CLI" --scheduled-time 2027-01-15T09:00:00.000Z --media '<descriptor from upload>' --json
   ```
5. **Hand it to your agent**. Put this line in its instructions. schedchie tools lists every command; schedchie <command> --help shows its flags.

   ```text
   Use the `schedchie` command for Schedchie. Run `schedchie <command> --json`; `schedchie tools` lists the commands you can call and `schedchie <command> --help` shows each one's flags. Never pass `--yes` (it confirms deletes and other destructive actions) without asking me first.
   ```

More: https://www.schedchie.com/ai/ai-agents-cli

<!-- connect:end -->

## Support

- Help and setup: https://www.schedchie.com/ai
- Contact: support@schedchie.com or https://www.schedchie.com/contact
- Terms: https://www.schedchie.com/terms
- Security reports: see [SECURITY.md](SECURITY.md)

Issues on this repository are for the files in it. For your account, mail support@schedchie.com.

## Licence

The manifests, the skill and the documentation are under the MIT licence ([LICENSE](LICENSE)). The Schedchie name and the logo files in `assets/` are trademarks and are not licensed: see [TRADEMARKS.md](TRADEMARKS.md).
