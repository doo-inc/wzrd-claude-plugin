# WZRD for Claude

WZRD turns a conversation into a live, shareable experience: a sales page, onboarding hub, data room, event page or course, with pages, blocks and an assistant that answers visitors by voice or text from everything you gave it.

Ask Claude to create something and describe what it's for. Add the details it should use, and any documents, pictures or websites. **No WZRD account is needed to create.** WZRD builds and publishes a guest room and gives you two links: **Preview** (share with visitors) and **Edit & claim** (open the editor and save it to your account).

Connect your WZRD account when you want Claude to work with *your* rooms: find and read them, change them in plain language (and undo), publish or unpublish, make share links, see visits and activity, and add to or search what the assistant knows.

WZRD only receives what a request needs, never your chat history.

## What's included

- **WZRD MCP server**: `https://wzrd.to/api/mcp/claude` — guest create without sign-in; account tools after OAuth.
- **Skills**:
  - `build-a-room`: turn a conversation, documents, or a described job into a shareable WZRD experience (no account required).
  - `edit-a-room`: find something in your account, change it, publish or share it (Connect required).
  - `room-results`: visits, outcomes, activity and visitor questions (Connect required).
  - `wzrd-review`: brand, UX writing, and product-trust reviews for WZRD surfaces.

## Getting started

1. Install the plugin from Claude's directory, or in Claude Code run:
   ```
   claude plugin marketplace add doo-inc/wzrd-plugin
   claude plugin install wzrd@wzrd
   ```
2. Open the WZRD plugin’s **Connectors** tab and enable the WZRD connector (`https://wzrd.to/api/mcp/claude`). Creating a room does not need a password; Connect is only required for account tools.
3. Try one of these:
   - "Make a WZRD sales room for my coffee subscription with pricing and an FAQ."
   - "Turn this conversation and its documents into a WZRD room."
   - "Change the headline of my Acme onboarding room to 'Welcome aboard, Acme'." (needs Connect)
   - "How many visits did my Acme room get this week?" (needs Connect)

## What the plugin sends and where

The plugin contains no code that runs on your machine. It has two parts:

- The skills, which are Markdown instructions for Claude (plus reference docs).
- One remote MCP server, `https://wzrd.to/api/mcp/claude`, run by DOO Inc.

When you ask Claude to use WZRD, Claude sends that server what the request needs: a description of what to build, the details it should use, and any files, pictures or website addresses you choose to include. WZRD uses this only to build, run and change your work, and sends the results back to Claude. WZRD may fetch the websites you name. It never asks Claude for your chat history.

Sign-in uses OAuth when you Connect for account tools. To disconnect, remove the WZRD connector in Claude's settings, or remove Claude's access under **Connected agents** in Studio.

## Privacy Policy

How DOO Inc. collects, uses, stores, shares and keeps data, including what AI assistants send, is in the WZRD Privacy Policy: [wzrd.to/privacy](https://wzrd.to/privacy). For questions, or to ask for access to or deletion of your data, email hello@wzrd.to.

## Support

- Help and contact: [wzrd.to/support](https://wzrd.to/support)
- Setup guide: [wzrd.to/claude](https://wzrd.to/claude)
- Terms: [wzrd.to/terms](https://wzrd.to/terms)

## License

MIT. See [LICENSE](LICENSE).
