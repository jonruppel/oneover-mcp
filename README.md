# OneOver MCP

**One API key → GPT, Gemini, Grok and Claude, plus image, video and audio generation, in Claude Code, Cursor, VS Code and any MCP client.**

Remote MCP server (Streamable HTTP). Nothing to install.

```
https://api.oneover.com/functions/v1/mcp
Authorization: Bearer oo_live_YOUR_KEY
```

Get a key: https://oneover.com/developers/dashboard (OneOver plans start at $10/month).

## Quick install

**Claude Code**
```bash
claude mcp add --transport http oneover https://api.oneover.com/functions/v1/mcp \
  --header "Authorization: Bearer $ONEOVER_API_KEY"
```

**Cursor** — `.cursor/mcp.json`
```json
{ "mcpServers": { "oneover": {
  "url": "https://api.oneover.com/functions/v1/mcp",
  "headers": { "Authorization": "Bearer oo_live_YOUR_KEY" } } } }
```

VS Code, Windsurf and Claude Desktop (via `mcp-remote`): see https://oneover.com/developers/mcp.md

New keys include chat, images, video, audio, usage, files, apps, assets, jobs and webhooks. `code` (Code Studio builds) and `billing` (top-ups) are opt-in.

## What you can ask for
- "Get a second opinion from GPT and Gemini on this diff."
- "Generate a 16:9 hero image for the landing page."
- "Make a 5-second clip of the logo animating."
- "Read this paragraph aloud and save the audio."

## Tools
`chat` · `list_models` · `generate_image` · `generate_video` · `check_video` · `generate_audio` · `get_job` · `create_run` · `get_run` · `run_app` · `list_assets` · `get_usage` · `build_*` (6) · `create_topup` (hidden unless the key has the `billing` scope; spends money)

See the full table with arguments in [the docs](https://oneover.com/developers/mcp).

Inspect without a key:
```bash
curl -s -X POST https://api.oneover.com/functions/v1/mcp \
  -H 'Content-Type: application/json' -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

## Also
- OpenAI-compatible REST: `https://api.oneover.com/functions/v1/openai-v1` 
- OpenAPI: https://oneover.com/openapi.json
- Claude Code plugin: https://github.com/jonruppel/oneover-claude-plugin
- MCP Registry: `com.oneover/mcp`

## Repo contents
- `.mcp.json`: root config so cursor.directory/Glama detect the server:
```json
{ "mcpServers": { "oneover": { "url": "https://api.oneover.com/functions/v1/mcp", "headers": { "Authorization": "Bearer ${ONEOVER_API_KEY}" } } } }
```
- `server.json` — MCP Registry manifest
- `examples/` — Claude Code, Cursor, VS Code configs

License: MIT (for this repo's docs and examples).
