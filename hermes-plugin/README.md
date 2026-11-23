# Memory.fit for Hermes Agent

Memory.fit: your training, your AI, one memory. Memory.fit connects your watch and health apps to the AI you already use. Your AI reads your training, sleep, recovery and fuel, and writes your plan back to the app and your watch.

This folder is an Agent Plugins v1 package: `plugin.json`, `mcp.json` and one skill. It is configuration only. There is no local code. The server is hosted by Memory.fit at `https://api.memory.fit/mcp` (Streamable HTTP).

## Install

1. In the Memory.fit app, set up your account, then make a personal key: Settings, AI agents, Use a key instead. It starts with `mem_pat_`.
2. Put it where Hermes reads secrets, then install and enable:

```bash
echo 'MEMORY_FIT_API_KEY=mem_pat_...' >> ~/.hermes/.env
hermes plugins install memory-fit
hermes plugins enable memory-fit
```

No Memory.fit account yet? Start at https://memory.fit/app.

### Sign in instead of a key (OAuth)

Memory.fit MCP supports OAuth 2.1 with dynamic client registration. A portable plugin package has no field for OAuth, so use a plain server entry in `~/.hermes/config.yaml` instead of this plugin:

```yaml
mcp_servers:
  memory-fit:
    url: "https://api.memory.fit/mcp"
    auth: oauth
```

Then run `hermes mcp login memory-fit` from a terminal. You choose what your AI may do on the Memory.fit sign-in page.

## What you should know before installing

- Every tool call, with its arguments, goes to `api.memory.fit`. Training, sleep, recovery and fuel data from your Memory.fit account comes back from that server.
- Needs a Memory.fit account (7 days free, then a subscription) and a personal key in `MEMORY_FIT_API_KEY`. Hermes reads the key from its own secret store. The plugin reads no other files and runs no commands or background processes.
- Some tools write to your own Memory.fit account (sessions, daily targets, meal plans, logged meals, notes), and sessions can go on to your watch. The package marks the server untrusted, so Hermes asks before every tool the server does not annotate as read-only.
- The tool set is served by the remote server at runtime. It is not covered by the pinned commit.
- No telemetry is sent by this plugin. Memory.fit does not give medical advice.

## Links

Website https://memory.fit, docs https://memory.fit/ai-agents, privacy https://memory.fit/privacy, terms https://memory.fit/terms, contact contact@memory.fit.
