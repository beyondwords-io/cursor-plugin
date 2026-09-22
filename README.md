# BeyondWords plugin for Cursor

The official [BeyondWords](https://beyondwords.io/) plugin for [Cursor](https://cursor.com/). It securely connects
Cursor to the BeyondWords MCP, allowing the agent to manage projects, create and update audio, configure voices, add
pronunciation rules, explore analytics, update player settings, and more.

Work with your BeyondWords account using natural-language prompts, and combine BeyondWords data and actions with
Cursor's understanding of your codebase and other connected tools.

## Installation

### Prerequisites

You'll need:

- A [BeyondWords](https://beyondwords.io/) account
- A [Cursor](https://cursor.com/) account

### Install from the Cursor Marketplace

1. Open **Cursor Settings**
2. Go to **Customize → Plugins**
3. Search for **BeyondWords**
4. Click **Add** next to the BeyondWords plugin
5. Follow the [Authentication](#authenticate) steps

### Install locally

For local development or manual installation, clone this repository into Cursor's local plugins directory:

```sh
git clone https://github.com/beyondwords-io/cursor-plugin.git ~/.cursor/plugins/local/beyondwords
```

Reload Cursor by opening the Command Palette and selecting **Developer: Reload Window**.

### Authenticate

After installing the plugin, ask Cursor:

> List my BeyondWords projects

Cursor will prompt you to authenticate your account. Click **Authenticate** to open the BeyondWords login page in your
browser. Sign in with the BeyondWords account whose project(s) you want to access, then approve the requested
permissions.

Two scopes are available:

- `api.read` — List and view projects, content, playlists, voices, languages, pronunciation rules, analytics, and
  player settings
- `api.write` — Create, update, duplicate, regenerate, and delete supported resources

Write tools are only available when the granted token includes `api.write`. A read-only grant therefore exposes a
read-only set of tools to the agent.

> [!NOTE]
> The plugin connects to `https://mcp.beyondwords.io/api`, an OAuth 2.1–protected MCP server. There are no API keys or
> credentials to copy into Cursor.

## Tools

The plugin provides 33 tools for working with your BeyondWords account. Tools are grouped by resource and separated by
the permission they require.

| Resource            | Read tools (`api.read`)                                        | Write tools (`api.write`)                                                                      |
| ------------------- | -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Projects            | `list_projects`, `get_project`                                 | `create_project`, `update_project`                                                             |
| Content             | `list_content`, `get_content`                                  | `create_content`, `update_content`, `regenerate_content`, `duplicate_content`, `delete_content` |
| Analytics           | `get_analytics`                                                | —                                                                                              |
| Voices              | `list_voices`, `get_voice`                                     | `update_voice`, `delete_voice`                                                                 |
| Languages           | `list_languages`                                               | —                                                                                              |
| Playlists           | `list_playlists`, `get_playlist`, `get_playlist_feed_settings` | `create_playlist`, `update_playlist`, `delete_playlist`, `update_playlist_feed_settings`       |
| Pronunciation rules | `list_rules`, `get_rule`, `list_rule_phonemes`                 | `create_rule`, `update_rule`, `delete_rule`, `transcribe_rule_text`                            |
| Player settings     | `get_player_settings`                                          | `update_player_settings`                                                                       |

The tools available to Cursor depend on the permissions granted during authentication. A token with only `api.read`
exposes the read tools, while a token with `api.write` also exposes tools that can modify your account.

`delete_content`, `delete_playlist`, `delete_voice`, and `delete_rule` are marked as destructive, as are
`update_content` and `regenerate_content`, which replace an item's existing audio. Cursor can therefore request
appropriate confirmation. All other tools are marked as read-only or as non-destructive writes.

## Example prompts

- "List my BeyondWords projects and show the number of listens each received last week"
- "Create content in project 1234 from https://example.com/my-article and tell me when the audio is ready"
- "Add a pronunciation rule to my NE Daily project so that 'NCL' is pronounced 'Newcastle'"
- "Show me my best-performing audio content from the past 30 days"
- "Update the BeyondWords player colors to match the styles in this codebase"

## Support

If the plugin is unavailable, check the BeyondWords connection under **Cursor Settings → Tools & MCP**.

For help using the BeyondWords for Cursor plugin:

- Email [support@beyondwords.io](mailto:support@beyondwords.io).
- View the [BeyondWords MCP doc](https://docs.beyondwords.io/docs-and-guides/support/beyondwords-mcp).
- Read the [BeyondWords privacy policy](https://beyondwords.io/privacy/).
