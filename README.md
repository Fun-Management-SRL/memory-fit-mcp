# Memory.fit MCP

<img src="assets/logo.png" alt="Memory.fit" width="96" align="right">

**Memory.fit** keeps your training, sleep, recovery and fuel in one place for the AI you already use. Your AI reads workouts from your watch and apps, sleep and HRV, and what you ate, then writes your week back: sessions, daily targets and meal plans, which show in the [Memory.fit app](https://memory.fit/app) on iPhone and Android.

This repository holds only the connection settings for Memory.fit MCP, a hosted server. There is nothing to run or build.

- **Address:** `https://api.memory.fit/mcp` (Streamable HTTP)
- **Sign-in:** OAuth 2.1 with dynamic client registration. Your AI opens the Memory.fit sign-in page; you choose what it may do. No key needed. AIs without sign-in can use a personal key from the app (Settings › AI agents › Use a key instead), sent as `Authorization: Bearer mem_pat_…`.
- **Needs:** a Memory.fit account, set up in the app first.

## Connect

| App | How |
|---|---|
| Claude | Settings › Connectors › Add custom connector, paste the address |
| ChatGPT | Settings › Apps and connectors › Create, paste the address |
| Grok, Grok Bot | Connectors › New connector › Custom, paste the address |
| Cursor | Install this plugin, or add `mcp.json` from this repo to `~/.cursor/mcp.json` |
| Claude Code | `claude mcp add --transport http memory-fit https://api.memory.fit/mcp` |
| Codex | `codex mcp add memory-fit --url https://api.memory.fit/mcp` |
| Gemini CLI | `gemini extensions install https://github.com/Fun-Management-SRL/memory-fit-mcp` |
| Cline | MCP Servers › Remote Servers: name `memory-fit`, URL `https://api.memory.fit/mcp`, transport Streamable HTTP (or the JSON below) |
| Anything else | Any MCP client: the address above, then sign in |

Step-by-step pages for each AI: [memory.fit/ai-coaches](https://memory.fit/ai-coaches).

### Cline, or any client with a JSON settings file

```json
{
  "mcpServers": {
    "memory-fit": {
      "type": "streamableHttp",
      "url": "https://api.memory.fit/mcp",
      "disabled": false
    }
  }
}
```

The first call opens the Memory.fit sign-in (OAuth 2.1). A client without OAuth can use a personal key from the app (Settings › AI agents › Use a key instead) as a header:

```json
"headers": { "Authorization": "Bearer mem_pat_..." }
```

## What your AI can do

- Read: workouts (Garmin, Wahoo, COROS, Polar, Suunto, Apple Health, Health Connect and more), sleep, HRV and resting heart rate, body composition, what you ate and drank, your races and goals.
- Write, with your permission: training sessions (sent to your watch), daily targets, meal plans, logged meals, notes for your other AIs.
- Check in: `get_updates` returns only what arrived since it last looked.

Memory.fit recommends nothing itself: the plans are your AI's, the data is yours. It is not medical advice.

## Links

- Website: https://memory.fit
- Privacy: https://memory.fit/privacy
- Terms: https://memory.fit/terms
- Support: support@memory.fit

The connection settings in this repository are MIT licensed. Memory.fit, the server and the app are not.
