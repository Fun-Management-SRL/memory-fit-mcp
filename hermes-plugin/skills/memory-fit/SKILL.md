---
name: memory-fit
description: Read the person's own training, sleep, recovery and fuel data (from their watch and health apps) and write their plan back through the Memory.fit MCP server. Use when they ask about workouts, sleep, HRV, recovery, fuel or races, or want their week planned or changed.
---

# Memory.fit

Memory.fit is a hosted MCP server that keeps one athlete's training, sleep, recovery and fuel in one place. It does not build plans itself: you read their data, you propose the plan, and with their permission you write it back to Memory.fit, where it shows in the Memory.fit app and goes to their watch.

## Connect

The server is Streamable HTTP at `https://api.memory.fit/mcp`.

- Key: the person makes a personal key in the Memory.fit app (Settings, AI agents, Use a key instead). It starts with `mem_pat_` and goes in `~/.hermes/.env` as `MEMORY_FIT_API_KEY`. This plugin sends it as `Authorization: Bearer`.
- Sign-in instead of a key: the server supports OAuth 2.1 with dynamic client registration. A plugin package cannot declare OAuth, so add the server by hand with `auth: oauth` in `~/.hermes/config.yaml`, then run `hermes mcp login memory-fit` (see the plugin README).
- Needs a Memory.fit account that has been set up in the app first. No account yet: https://memory.fit/app

Never print, log or echo the key back to the person.

## When to use it

- "How did my ride go?", "Did I sleep enough this week?", "Am I recovered for intervals?"
- Trends: training load, HRV, resting heart rate, sleep, weight, fuel.
- Planning: look at the week and the races ahead, then propose sessions and daily targets.
- Doing: write sessions, targets, meal plans or notes. These change the person's own Memory.fit data, so confirm the details with them first.

## How to use it well

1. At the start of a conversation about training, call `get_updates`: it returns only what arrived since you last looked. Call `get_guide` once to learn the tools and rules.
2. Quote the numbers you get back instead of rounding them into vague words.
3. Only sources the person connected return data. If something is missing, say so and use another source.
4. Memory.fit gives no medical advice and recommends nothing itself. Plans are yours to propose and the person's to accept.
