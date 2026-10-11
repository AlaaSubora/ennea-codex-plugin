---
name: setup
description: Check the Ennea plugin connection and explain the connected workspace and available operations.
---

Use the connected Ennea MCP tools. Call `ennea_context` to check the actual account,
workspace, environment and granted access, then `ennea_capabilities` to discover
supported operations. Explain the connected context in the user's language.
Installed tools alone do not prove a working connection.

If Ennea tools are not listed, use the harness's tool search when available to
discover them before concluding they are absent. If they remain unavailable,
report that this chat has not exposed the plugin's tools. Check that Ennea is
enabled and start a new chat with the plugin selected so the host can load it.
Missing tools alone do not establish an OAuth failure; do not recommend repeated
reconnection or claim that the connection is missing or expired.

If an actual connection or tool response reports authentication required, such as
HTTP 401, use the host's Ennea plugin connection settings and browser sign-in and
consent flow. Do not request credentials in chat, write tokens into files, or
install the CLI. The user selects actions and record types for the intended
workspace; Codex manages the tokens. Revocation is available in Ennea under
Agents → Agent access. Report the actual failure if authentication does not
restore access instead of repeating the connection flow.

Setup performs reads only. Do not create sample materials or proposals. If the
connected workspace differs from the user's intended destination, resolve that
before writing; the workspace is bound to the connection, not a tool argument.

Explain that the agent can explore any source in its own environment and submit
structured operations, individually or in batches. Configuration changes require
review in Ennea. Keep the explanation brief and let the user choose their task.
