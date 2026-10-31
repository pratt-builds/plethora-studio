# Security

Please report security issues in this plugin or in the Plethora MCP server
(https://agent.plethora.studio/mcp) to **pratt@plethora.studio**.

Include what you found, the steps to reproduce it, and what an attacker could
do with it. Please don't share the issue publicly until we have replied and
fixed it. We aim to reply within a few business days.

The same contact is published at https://plethora.studio/.well-known/security.txt.

## Scope

- This repository: the skill, the plugin manifests and the MCP configuration.
- The Plethora MCP server and the pairing and draft upload it provides.

How pairing limits access: the agent never receives a password or API key. The
creator approves each pairing in the Plethora app, and the key the agent gets
can only save drafts, lasts 4 hours and can be revoked at
https://create.plethora.studio/agents.
