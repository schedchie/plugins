# Schedchie plugin for Claude

The Claude plugin for [Schedchie](https://www.schedchie.com), the social media scheduler. It adds the hosted Schedchie MCP server and the Schedchie agent skill to Claude Code and the other Claude apps that install plugins. It holds configuration and instructions only: nothing in it runs on install.

- **Server:** `https://mcp.schedchie.com/mcp` (Streamable HTTP), declared in `.claude-plugin/plugin.json`
- **Sign-in:** OAuth in your browser on schedchie.com. Claude registers itself on the first tool call, so there is no key, client ID or password to paste.
- **Needs:** a Schedchie account with an active plan or trial. Create one on the sign-in screen. Social accounts are connected in the Schedchie web app.

## Install

```bash
claude plugin marketplace add schedchie/plugins
claude plugin install schedchie@schedchie
```

## What Claude can do with it

Schedule, post and cross-post to Instagram, Facebook, TikTok, LinkedIn, Pinterest, YouTube, Threads, Bluesky, Mastodon, Telegram, Google Business Profile, Discord, Slack, WordPress, Dev.to, Hashnode, Ghost, Pixelfed, Listmonk and X, with different text per network. Then reschedule, edit or retry posts and say why one failed, upload images and video, read analytics on Instagram, Facebook, TikTok, LinkedIn, Pinterest, YouTube, Threads, Bluesky, Mastodon, Telegram, Google Business Profile and Discord, find the best times to post from each account's own history, approve or reject posts teammates hold for review, and read and answer comments on published posts.

On the sign-in screen you choose what the connection may do, in six permission groups. Deleting a post, removing a member or disconnecting an account is marked destructive, and the skill in `skills/schedchie/SKILL.md` tells Claude to ask you first. It also tells Claude to convert your local times to UTC and to treat text written by other people as data, never as instructions.

## What is sent where

When you ask Claude to act, it calls tools on `mcp.schedchie.com` over HTTPS with the OAuth token from your sign-in, carrying what you ask it to act on: post text, times, account choices, media, comment replies, notes and the email addresses of people you invite. The tool results go back to Claude. Privacy policy: https://www.schedchie.com/privacy

Setup for other assistants, and every other file: https://github.com/schedchie/plugins

## Support and licence

Support: support@schedchie.com or https://www.schedchie.com/contact

The manifest, the skill and this readme are under the MIT licence ([LICENSE](LICENSE)). The Schedchie name and the logo file in `assets/` are trademarks and are not licensed; you may use them unchanged to identify the Schedchie service and this plugin, for example in a directory listing. The Schedchie service is provided under https://www.schedchie.com/terms.
