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

## Cursor

Install **gpu-cloud** from the Cursor marketplace, or add the server from https://console.centeraivision.com/agents (Add to Cursor), then sign in when Cursor asks.

## Codex, Claude Desktop and other MCP clients

Server address (Streamable HTTP): `https://console.centeraivision.com/mcp`. It signs in with OAuth, or takes an API key as `Authorization: Bearer cav_live_…`.

Setup for each client: https://console.centeraivision.com/agents

## Spending limits

For agents that run unattended, create an API key in the console under Settings → API keys and give it a spending limit and an expiry. The key can never commit more GPU time than its limit.

## Try it without an account

`https://console.centeraivision.com/mcp/public` lists GPUs, setups and estimated prices with no sign-in.

## Pricing feed

`GET https://console.centeraivision.com/api/v1/gpus` returns every GPU we offer with its live on-demand price and availability. It is public (no key), JSON, and refreshed every 60 seconds.

```json
[
  {
    "id": "a100-80gi-pcie",
    "name": "NVIDIA A100",
    "family": "PCIe · Ampere",
    "consumer": false,
    "specs": [["Memory", "80 GB HBM2e"], ["Bandwidth", "1.94 TB/s"]],
    "ratePerHour": 176,
    "available": 5,
    "rentable": true,
    "total": 12
  }
]
```

| Field | Meaning |
|---|---|
| `id` | Stable GPU id: model, memory and interface |
| `name`, `family` | Display name; interface and architecture |
| `consumer` | `true` for consumer cards (RTX 30/40/50 series) |
| `specs` | Label and value pairs, memory first |
| `ratePerHour` | On-demand price for one GPU, in **US cents per hour**, before 5% UAE VAT on top-ups. Billed by the minute |
| `available` | GPUs free to start right now |
| `rentable` | `true` when enough are free to start one reliably; only these can be ordered |
| `total` | GPUs of this model in the pool |

One GPU per machine, 1–47 hours per order, prepaid; unused minutes return to the balance.

## What's inside

- `plugins/gpu-cloud/.mcp.json` (Claude Code) and `plugins/gpu-cloud/mcp.json` (Cursor): the remote MCP server.
- `.claude-plugin/` and `.cursor-plugin/`: the marketplace and plugin manifests for each.
- `plugins/gpu-cloud/skills/rent-gpu`: how to rent a GPU safely: check the account, quote, ask before starting, wait for it, copy results off, stop.

Questions: info@centeraivision.com
