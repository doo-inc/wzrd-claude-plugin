# WZRD for Claude

WZRD turns a conversation into a live, shareable experience: a sales page, onboarding hub, data room, event page or course, with pages, blocks and an assistant that answers visitors by voice or text from everything you gave it.

Ask Claude to create something and describe what it's for. Add the details it should use, and any documents, pictures or websites. WZRD builds it from a matching template, and Claude can publish it and give you the share link.

Work with your WZRD work from Claude: find and read it, change it in plain language (every change is labelled and can be undone), publish or unpublish, make share links, see visits, outcomes and what visitors asked, and add to or search what the assistant knows. By default, changes from Claude wait for your approval in Studio.

WZRD only receives what a request needs, never your chat history.

## What's included

- **WZRD MCP server**: connects Claude to `https://wzrd.to/api/mcp` (OAuth sign-in).
- **Skills**:
  - `build-a-room`: turn a conversation, documents, or a described job into a shareable WZRD experience.
  - `edit-a-room`: find something you built, change it, publish or share it.
  - `room-results`: visits, outcomes, activity and visitor questions, with suggestions.
  - `wzrd-review`: brand, UX writing, and product-trust reviews for WZRD surfaces.

## Getting started

1. Install the plugin from Claude's directory, or in Claude Code run:
   ```
   claude plugin marketplace add doo-inc/wzrd-plugin
   claude plugin install wzrd@wzrd
   ```
2. The first time Claude uses WZRD, you're asked to sign in to your WZRD account and approve what Claude may do. A free account works: sign up at [wzrd.to/signup](https://wzrd.to/signup).
3. Try one of these:
   - "Make a WZRD sales room for my coffee subscription with pricing and an FAQ."
   - "Turn this conversation and its documents into a WZRD room."
   - "Change the headline of my Acme onboarding room to 'Welcome aboard, Acme'."
   - "How many visits did my Acme room get this week?"
   - "Give me the share link for my Acme room."

By default, edits and publishing from Claude can wait for your approval. You approve them in Studio. An owner can change this under **Agents → What connected agents can do**.

## What the plugin sends and where

The plugin contains no code that runs on your machine. It has two parts:

- The skills, which are Markdown instructions for Claude (plus reference docs).
- One remote MCP server, `https://wzrd.to/api/mcp`, run by DOO Inc.

When you ask Claude to use WZRD, Claude sends that server what the request needs: a description of what to build, the details it should use, and any files, pictures or website addresses you choose to include. WZRD uses this only to build, run and change your work, and sends the results back to Claude. WZRD may fetch the websites you name. It never asks Claude for your chat history.

Sign-in uses OAuth. Claude holds an access token for your WZRD account, limited to the permissions you approved. To disconnect, remove the WZRD connector in Claude's settings, or remove Claude's access under **Connected agents** in Studio.

## Privacy Policy

How DOO Inc. collects, uses, stores, shares and keeps data, including what AI assistants send, is in the WZRD Privacy Policy: [wzrd.to/privacy](https://wzrd.to/privacy). For questions, or to ask for access to or deletion of your data, email hello@wzrd.to.

## Support

- Help and contact: [wzrd.to/support](https://wzrd.to/support)
- Setup guide: [wzrd.to/claude](https://wzrd.to/claude)
- Terms: [wzrd.to/terms](https://wzrd.to/terms)

## License

MIT. See [LICENSE](LICENSE).
