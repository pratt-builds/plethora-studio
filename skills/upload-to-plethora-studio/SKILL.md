---
name: upload-to-plethora-studio
description: 'Use when the creator says "upload to plethora studio", "upload to Plethora", "put this on Plethora" or "make a Plethora Bit". Builds a Bit (a tiny interactive piece for the Plethora phone app) from their idea and uploads it as a draft once they approve a pairing code in the Plethora app. No login, password or API key needed.'
---

# Upload to Plethora Studio

Plethora (https://plethora.studio) is a phone app of tiny interactive Bits.
The creator tells you an idea and says "upload to plethora studio". You build
the Bit, the creator approves a pairing in the Plethora app, and you upload the
Bit as a draft. Publishing stays the creator's choice in the app.

## Ground rules

- There is no login, password or API key for this. Never ask the creator for
  a password, API key, login, username or email. Access comes only from a
  pairing the creator approves in the Plethora app.
- The Bit contract changes. Read the current guide for every new Bit and again
  before each upload. Do not build from memory or from an earlier chat.
- Uploads are drafts. Never say a Bit is published or live.
- Keep `pairingSecret` and `uploadKey` private: out of files, commits and
  chat summaries.
- If the creator declines the pairing, stop and ask before starting another.

## Path A: plethora MCP tools (preferred)

Use this path when the `plethora` MCP server is connected. Its tools are
`get_bit_guide`, `start_pairing`, `wait_for_pairing` and `upload_draft`; your
host may show them with a prefix.

1. Call `get_bit_guide` with topic `start`. Read the further topics it names
   (such as `sdk`, `context`, `examples` and `upload`) before writing code.
2. Build the Bit exactly as the guide says, and test what you can.
3. Call `start_pairing`. Show the creator the 8-character `pairingCode` and
   the links (`approvalUrl`, and `pairingUrl` to open on their phone), and ask
   them to approve the pairing in the Plethora app.
4. Call `wait_for_pairing` with `pairingId` and `pairingSecret`, using a
   `waitSeconds` of 20 or less. Call it again while the pairing is still
   waiting. If `expiresAt` passes first, start a new pairing. Once approved it
   returns an `uploadKey`, valid for 4 hours; reuse it for more uploads in
   that time.
5. Call `upload_draft` with the `uploadKey` and the Bit's `title`,
   `description`, `tags`, `source` and `manifest`, shaped as the guide says.
6. A refusal explains what to fix and says "Nothing was saved." Fix what it
   names, re-read the guide if it points you there, and upload again.
7. On success, tell the creator "Saved draft", the title and `bitId`, the
   tests you actually ran, and any `notices`. Say the draft is in
   Create → Drafts in the Plethora app, and share the `draftsUrl`.

## Path B: HTTPS, without MCP

Fetch https://agent.plethora.studio/v1/agent/start.md and follow it step by
step. It covers the same guide, pairing and draft upload over plain HTTPS, and
the ground rules above still apply.

## When network access is refused

If a fetch or POST to agent.plethora.studio is blocked, tell the creator the
setting their agent needs, then try again once they have changed it:

- Claude Code on the web or in the Claude app: Network access → Full, or
  Custom with `plethora.studio` and `agent.plethora.studio`.
- Codex cloud: turn internet access on, allow all domains or just those two
  hosts, and allow all HTTP methods.
- Codex on a computer: approve network access when Codex asks.
