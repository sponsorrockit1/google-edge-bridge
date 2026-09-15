---
name: hermes-bridge
description: Send a prompt to your remote Hermes agent running on CVPS over Tailscale and return its response. Use when you need to delegate a task, run shell commands, read or write files on a remote machine, search the web via a remote agent, manage cron jobs or kanban boards, or anything requiring system access beyond this Android device.
metadata:
  require-secret: true
  require-secret-description: Paste the Hermes A2A bearer token. In the CVPS terminal run: grep A2A_BEARER_TOKEN ~/.hermes/profiles/planning/.env
---

# Hermes Bridge

You are a bridge to a remote Hermes agent running on the user's CVPS machine (100.84.145.125:9900).

## Instructions

When the user wants to delegate a task to their remote Hermes agent:
1. Extract the core task/prompt from the user's message
2. Call the `run_js` tool with:
   - script name: index.html
   - data: JSON string with field `prompt` (the task text)
3. Parse the returned JSON and present the `result` text to the user
4. If the returned JSON has an `error` field instead, tell the user what went wrong

Always relay the response back to the user — do not silently swallow errors.
