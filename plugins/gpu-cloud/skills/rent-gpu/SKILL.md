---
description: Rents a GPU on Center AI Vision for training, fine-tuning, inference or a notebook, then cleans up. Use when the user wants a GPU, more GPU memory than their machine has, or to run a job on an A100, H100, L40 or RTX card.
---

Use the `center-ai-vision` MCP tools. If they aren't connected yet, ask the user to run `/mcp` and sign in.

1. Call `get_account`. If the account can't start GPUs yet, tell the user what is missing (funds or the one-time ID check) and give them the link it returns. Don't continue.
2. Call `list_gpus` and pick a rentable GPU with enough memory for the job: about 2 GB per billion parameters to serve a model in 16-bit, and roughly four times that to fine-tune it in full.
3. Call `quote_gpu` with the fewest hours that fit the job. Show the user the GPU, setup, hours and total, and ask for a clear yes. Never call `start_gpu` without it.
4. Call `start_gpu` with the quote id. For Ubuntu + SSH, pass the user's SSH key ids from `list_ssh_keys`, or add their public key with `add_ssh_key` first.
5. Poll `list_machines` until the machine is running, then connect with the address it gives.
6. When the work is done, copy results off the machine (its disk is deleted when it stops), then call `stop_machine` so unused time returns to the balance.

If a call is refused because of a spending limit, tell the user how much the key has left and stop. Don't look for another key.
