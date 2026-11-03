# Center AI Vision plugins

Rent data-centre GPUs by the hour from your coding agent. Your agent can list GPUs and prices, start one with PyTorch + Jupyter, vLLM or Ubuntu + SSH, connect to it, and stop it when the work is done. It only spends your prepaid balance, it asks before it spends, and you can cap what it may spend.

## Claude Code

```
/plugin marketplace add Elchaigroup/center-ai-vision-plugins
/plugin install gpu-cloud@center-ai-vision
```

Then run `/mcp` and sign in with your Center AI Vision account. No key to copy.

Without the plugin:

```
claude mcp add --transport http center-ai-vision https://console.centeraivision.com/mcp
```

## Cursor, Codex, Claude Desktop and other MCP clients

Server address (Streamable HTTP): `https://console.centeraivision.com/mcp`. It signs in with OAuth, or takes an API key as `Authorization: Bearer cav_live_…`.

Setup for each client: https://console.centeraivision.com/claude

## Spending limits

For agents that run unattended, create an API key in the console under Settings → API keys and give it a spending limit and an expiry. The key can never commit more GPU time than its limit.

## Try it without an account

`https://console.centeraivision.com/mcp/public` lists GPUs, setups and estimated prices with no sign-in.

## What's inside

- `plugins/gpu-cloud/.mcp.json`: the remote MCP server.
- `plugins/gpu-cloud/skills/rent-gpu`: how to rent a GPU safely: check the account, quote, ask before starting, copy results off, stop.

Questions: info@centeraivision.com
