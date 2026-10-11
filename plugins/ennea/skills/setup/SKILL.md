---
name: setup
description: Check the Ennea plugin connection and explain the connected workspace and available operations.
---

Use the connected Ennea MCP tools. Call `ennea_context` to check the actual account,
workspace, environment and granted access, then `ennea_capabilities` to discover
supported operations. Explain the connected context in the user's language.
Installed tools alone do not prove a working connection.

If authentication is missing or expired, direct the user to the host's Ennea
plugin connection settings. Do not request credentials in chat, write tokens into
files, or install the CLI. Use the browser sign-in and consent flow. The user selects actions and record
types for the intended workspace; tokens are managed by Codex. Revocation is
available in Ennea under Agents → Agent access.

Setup performs reads only. Do not create sample materials or proposals. If the
connected workspace differs from the user's intended destination, resolve that
before writing; the workspace is bound to the connection, not a tool argument.

Explain that the agent can explore any source in its own environment and submit
structured operations, individually or in batches. Configuration changes require
review in Ennea. Keep the explanation brief and let the user choose their task.
