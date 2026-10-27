# BumbleBox MCP server

[![Listed on mcpservers.org](https://mcpservers.org/badge.svg)](https://mcpservers.org/servers/bumblebox/bumblebox-mcp) [![mcptry](https://mcptry.com/badge/ai.bumblebox/mail)](https://mcptry.com/servers/ai.bumblebox/mail)

Email intelligence for people running several businesses, inside your AI assistant.
[BumbleBox](https://bumblebox.ai) triages every connected mailbox (Gmail, Outlook, any IMAP);
this remote MCP server lets Claude, ChatGPT, Cursor, VS Code or any MCP client work with it.

- **Endpoint**: `https://api.bumblebox.ai/api/mcp` (streamable HTTP)
- **Auth**: OAuth 2.1 with dynamic client registration and PKCE. You approve once on
  bumblebox.ai and see exactly which permissions the assistant gets.
- **Plans**: Pro or Business ([pricing](https://bumblebox.ai/pricing)).
- **Setup for every client**: https://bumblebox.ai/integrations

## Install

**Claude Code** (plugin, with the `/bumblebox:to-answer` and `/bumblebox:tidy` commands):

```
/plugin marketplace add BumbleBox/bumblebox-mcp
/plugin install bumblebox@bumblebox
```

Or just the server: `claude mcp add --transport http bumblebox https://api.bumblebox.ai/api/mcp`

**Claude (claude.ai, desktop)**: Settings → Connectors → Add custom connector →
`https://api.bumblebox.ai/api/mcp`.

**ChatGPT**: Settings → Apps & Connectors → create a connector (developer mode), paste the
server URL, authentication OAuth.

**Cursor** (`~/.cursor/mcp.json`):

```json
{ "mcpServers": { "bumblebox": { "url": "https://api.bumblebox.ai/api/mcp" } } }
```

**VS Code** (`.vscode/mcp.json`):

```json
{ "servers": { "bumblebox": { "type": "http", "url": "https://api.bumblebox.ai/api/mcp" } } }
```

## Tools

| Tool                                                                | What it does                                                      |
| ------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `search_emails`, `get_email`                                        | Search and read every connected mailbox                           |
| `list_to_answer`                                                    | Emails waiting for your reply                                     |
| `search_contacts`, `list_folders`, `list_calendar_events`           | Contacts, folders, calendar                                       |
| `draft_reply`                                                       | A reply draft that waits in BumbleBox for your click on Send      |
| `send_reply`                                                        | A reply to the original sender, at the level you set in BumbleBox |
| `archive_email`, `move_email`, `trash_email`, `restore_to_inbox`    | Tidy on request, always undoable                                  |
| `list_missions`, `list_campaign_drafts`, `list_replies_to_validate` | Your campaigns                                                    |
| `create_campaign_draft`, `update_campaign_draft`                    | Campaign drafts, sent only from BumbleBox                         |

## What it never does

BumbleBox sends nothing without your click — Send, Schedule, or a standing permission you set
yourself in BumbleBox for a precise scope (existing participants of a thread you opened, a
message with no commitment), capped, logged and cancellable. Anything else waits for your
validation, and an assistant can never change that permission.

There is no permanent deletion: `trash_email` moves only certified noise to the Trash and turns
anything else into a one-tap proposal in BumbleBox; everything is undone with `restore_to_inbox`.

## Links

- Privacy policy: https://bumblebox.ai/privacy
- Terms: https://bumblebox.ai/terms
- Support: contact@bumblebox.ai
- `llms.txt`: https://bumblebox.ai/llms.txt

This repository holds the public metadata (registry `server.json`, Claude Code plugin). The
server itself is operated by BumbleBox. Licence: MIT.
