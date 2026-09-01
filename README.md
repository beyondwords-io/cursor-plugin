# BeyondWords for Cursor

[BeyondWords](https://beyondwords.io) is a text-to-speech platform for publishers. This plugin connects Cursor to the
BeyondWords MCP server, so an agent can work with your projects, content, voices and pronunciation rules directly.

## Install

Install the plugin from the Cursor marketplace, or clone this repository into `~/.cursor/plugins/local/beyondwords`
and reload the window.

## Authentication

The plugin talks to `https://mcp.beyondwords.io/api`, an OAuth 2.1 protected MCP server. There is nothing to paste:
Cursor discovers the authorization server, registers itself and opens a browser sign-in the first time a tool is
called. Approve the request with the BeyondWords account whose projects you want to use.

Two scopes are requested:

- `api.read` — list and read projects, content, voices, languages, rules, analytics and player settings.
- `api.write` — create, update, duplicate, regenerate and delete those resources.

Write tools are hidden from the agent unless the granted token carries `api.write`, so a read-only grant exposes a
read-only tool set.

## Tools

26 tools, grouped by resource:

| Group      | Read                                           | Write                                                                                           |
| ---------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Projects   | `list_projects`, `get_project`                 | `create_project`, `update_project`                                                              |
| Content    | `list_content`, `get_content`                  | `create_content`, `update_content`, `regenerate_content`, `duplicate_content`, `delete_content` |
| Analytics  | `get_analytics`                                | —                                                                                               |
| Voices     | `list_voices`, `get_voice`                     | `update_voice`, `delete_voice`                                                                  |
| Languages  | `list_languages`                               | —                                                                                               |
| Rules      | `list_rules`, `get_rule`, `list_rule_phonemes` | `create_rule`, `update_rule`, `delete_rule`, `transcribe_rule_text`                             |
| Settings   | `get_player_settings`                          | `update_player_settings`                                                                        |

`delete_content`, `delete_voice` and `delete_rule` are annotated as destructive; every other tool is annotated
read-only or as a non-destructive write, so Cursor can prompt appropriately.

## Example prompts

- "List my BeyondWords projects and show last week's listens for the main one."
- "Create content in project 1234 from this article URL and tell me when the audio is ready."
- "Add a pronunciation rule so 'BeyondWords' is read as one word, then show the phonemes."

## Support

[support@beyondwords.io](mailto:support@beyondwords.io) · [Documentation](https://docs.beyondwords.io) ·
[Privacy policy](https://beyondwords.io/privacy/)
