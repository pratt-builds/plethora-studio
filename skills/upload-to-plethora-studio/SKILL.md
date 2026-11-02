---
name: upload-to-plethora-studio
description: 'Use when the creator says "upload to plethora studio", "upload to Plethora", "put this on Plethora" or "make a Plethora Bit". Builds a Bit (a tiny interactive piece for the Plethora phone app) from their idea and saves it as a draft once they approve a pairing in the Plethora app. No login, password or API key needed.'
---

# Upload to Plethora Studio

Plethora (https://plethora.studio) is a phone app of tiny interactive Bits.
The creator tells you an idea and says "upload to plethora studio". You build
the Bit, the creator approves a pairing in the Plethora app, and you save the
Bit to their account as a draft. Publishing stays the creator's choice in the
app.

This skill works with the `plethora` MCP server that comes with this plugin.
Its tools are `get_bit_guide`, `start_pairing`, `wait_for_pairing` and
`upload_draft`; your host may show them with a prefix. If those tools are not
available, tell the creator that the Plethora connector needs to be enabled,
and stop.

## Ground rules

- No login, password or API key is involved. Never ask the creator for a
  password, API key, login, username or email. Access comes only from a
  pairing the creator approves in the Plethora app.
- Uploads are drafts. Never say a Bit is published or live.
- Keep `pairingSecret` and `uploadKey` private: out of files, commits and
  chat summaries.
- Send only what an upload needs: the Bit's title, description, tags, source
  and manifest.
- If the creator declines the pairing, stop and ask before starting another.

## Steps

1. **Look up the reference.** Call `get_bit_guide` with topic `start`. It
   describes what a Bit is and the package shape, and lists smaller reference
   topics (for example the SDK index, single SDK topics, examples and the
   upload format) with their sizes. Read only the topics this Bit needs; the
   full reference is large. The SDK changes over time, so check the APIs you
   use against the reference rather than from memory.
2. **Build the Bit** to the package shape the reference describes, and test
   what you can.
3. **Start pairing.** Call `start_pairing`. Show the creator the 8-character
   `pairingCode` and the links (`approvalUrl`, and `pairingUrl` to open on
   their phone), and ask them to approve it in the Plethora app.
4. **Wait for approval.** Call `wait_for_pairing` with `pairingId` and
   `pairingSecret`, using a `waitSeconds` of 20 or less, and call it again
   while the pairing is still waiting. If `expiresAt` passes first, start a
   new pairing. Once approved it returns an `uploadKey`, valid for 4 hours;
   reuse it for more uploads in that time.
5. **Save the draft.** Call `upload_draft` with the `uploadKey` and the Bit's
   `title`, `description`, `tags`, `source` and `manifest`.
6. **Fix refusals.** A refusal names what to fix and says "Nothing was saved."
   Fix what it names and upload again.
7. **Report.** Tell the creator "Saved draft", the title and `bitId`, the tests
   you actually ran, and any `notices`. Say the draft is in Create → Drafts in
   the Plethora app, where the creator plays it and can publish it.
