# Plethora Studio

Plethora Studio gives your coding agent the Plethora skill and the Plethora MCP
server, so you can turn an idea into a Bit for [Plethora](https://plethora.studio),
the phone app of tiny interactive Bits. Tell your agent the idea and say
"upload to plethora studio". The agent builds the Bit, shows you a pairing code
to approve in the Plethora app, and uploads the Bit as a draft; publishing stays
your choice in the app.

No login, password or API key is needed. The same plugin installs in Claude
Code and in Codex.

## Install in Claude Code

In a Claude Code session:

```text
/plugin marketplace add pratt-builds/plethora-studio
/plugin install plethora-studio@plethora
```

From your shell, the same steps are
`claude plugin marketplace add pratt-builds/plethora-studio` and
`claude plugin install plethora-studio@plethora`. The skill runs as
`/plethora-studio:upload-to-plethora-studio`, and Claude also picks it up when
you say "upload to plethora studio".

MCP server only, without the skill:

```bash
claude mcp add --transport http plethora https://agent.plethora.studio/mcp
```

## Install in Codex

```bash
codex plugin marketplace add pratt-builds/plethora-studio
codex plugin add plethora-studio@plethora
```

You can also add the marketplace, run `/plugins` in Codex and install
Plethora Studio from the Plethora marketplace. Start a new session before you
use it.

MCP server only, without the skill:

```bash
codex mcp add plethora --url https://agent.plethora.studio/mcp
```

## claude.ai and ChatGPT

Add the MCP server as a custom connector with the URL
`https://agent.plethora.studio/mcp` and no authentication:

- claude.ai: Customize > Connectors > Add custom connector. Enter the URL,
  choose No sign-in if asked, then Add.
- ChatGPT: chatgpt.com/plugins > + > Add custom MCP server. Enter a name and
  the URL, set authentication to none, accept the warning, then Create as a
  plugin.

## Sandboxed agents

If your agent runs in a sandbox, give it network access to Plethora:

- Claude Code on the web or in the Claude app: Network access → Full, or
  Custom with `plethora.studio` and `agent.plethora.studio`.
- Codex cloud: turn internet access on, allow all domains or just those two
  hosts, and allow all HTTP methods.
- Codex on a computer: approve network access when Codex asks.

## What it contacts and stores

Hosts contacted: agent.plethora.studio only (docs, pairing, draft upload over
HTTPS). The plugin stores nothing.

The agent reads the Bit guide, starts a pairing, and at upload sends the Bit's
title, description, tags, source and manifest. The plugin has no hooks,
scripts or binaries: it is one skill plus the address of one remote MCP
server.

## How pairing keeps it safe

- The agent never asks for a password, API key or login.
- You approve each pairing yourself in the Plethora app, with the 8-character
  code or the approval link the agent shows you.
- The key the agent gets can only upload drafts, lasts 4 hours, and can be
  revoked.
- Nothing is published until you publish it in the app.

## Privacy

[Privacy policy](https://plethora.studio/privacy): Plethora's policy covers
the Bits and drafts you upload.

## Support

Visit [plethora.studio](https://plethora.studio).

## License

MIT. See [LICENSE](LICENSE).
