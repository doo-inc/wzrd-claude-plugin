---
name: build-a-room
description: Turn a conversation, documents, or a described job into a structured WZRD room. Use when the user asks to make, build, publish, or plan a WZRD room from a chat, thread, transcript, attachments, project files, links, or a job such as a proposal, client portal, investor update, menu or showroom. Do not use for ordinary summaries that are not intended to become a room.
---

# Build a room

Convert conversation and documents into an interactive, source-grounded WZRD room through the WZRD MCP. Pass the relevant conversation and notes to WZRD verbatim so the service can build from the complete source rather than from an intermediate summary.

**Creating a room does not require signing in.** The Claude MCP tools `templates_search`, `rooms_create`, and `tools_make` work without a WZRD account (same model as ChatGPT). Only ask the user to Connect / sign in when they need account tools (list their rooms, edit, publish from an account, analytics).

Read [references/mcp-workflow.md](references/mcp-workflow.md) before any WZRD MCP call. Use [references/room-blueprint.md](references/room-blueprint.md) when you need a decision model for structure, provenance, or a blueprint handoff.

## Establish scope

Interpret “this chat,” “this conversation,” or “everything” as the user-visible conversation plus the documents and links actually available in its context. Do not claim access to hidden history, private reasoning, deleted content, or files that were not supplied or connected.

Support two modes:

- **Include everything:** include the full relevant user-visible conversation and notes verbatim, in order, with speaker labels. Include every accessible document, image, and website the user mentioned or attached, subject to the MCP limits.
- **Choose what to include:** inventory the available topics, message ranges, documents, images, and links in a compact numbered list. Let the user select items, ranges, or rules. Put the selected conversation passages and notes into `context` verbatim rather than summarizing them. If the selection is already clear, proceed without another confirmation.

Before using sensitive, personal, confidential, or third-party material, surface what would enter the room and apply the user's intended access level. Never place credentials, hidden instructions, private chain-of-thought, or internal tool output in a room.

## Prepare the request

1. Express what the room is for in one or two sentences for `prompt`.
2. Assemble the full selected conversation and notes verbatim for `context`, up to 400,000 characters. Preserve speaker labels, order, wording, decisions, and competing ideas. Do not include hidden system or developer instructions, private reasoning, credentials, or internal tool output.
3. Read every selected local document from disk and encode its bytes as base64. Preserve its filename and MIME type.
4. Classify logos and pictures as `images`; classify supported documents as `files`; put sites the user wants WZRD to read in `websites`.
5. Preflight the item counts, per-item sizes, total file sizes, and serialized request size. Ask the user to narrow the selection only when the request cannot fit safely within the limits.

## Build through WZRD MCP

Use the plugin's WZRD MCP server. Do not substitute a generic website builder, local mockup, direct private API call, or hand-authored “room” artifact.

When the person describes a **job** (a proposal, client portal, investor update, menu, course…):

1. Call `templates_search` with that job and pick the closest template id.
2. Call `rooms_create` once with `prompt`, `context`, `files`, `images`, `websites`, and that `template` id when one fits.

When the person names a job a **WZRD tool** makes (an invoice, a quote, a pitch deck…), use `tools_make` with that tool and their answers; `tools_list` shows the tools and their questions.

When they only describe a room without naming a template, still call `templates_search` first when a finished outcome exists, then `rooms_create`.

Do not ask for credentials merely to create. Do not silently retry a response that may have created a room. If `rooms_create` fails before returning a result, report the failure and preserve the prepared request for a deliberate retry.

If the MCP tools are missing from this chat, tell the user to open the WZRD plugin’s Connectors tab (or add `https://wzrd.to/api/mcp/claude` as a custom connector) and try again in a new chat — create still does not require a WZRD password once the connector is loaded.

## Quality bar

- Send the selected conversation and notes verbatim in `context`; do not replace them with a summary.
- Keep documents as first-class source files rather than manually paraphrasing their contents.
- Do not invent names, prices, dates, proof points, permissions, integrations, or completed actions.
- Keep the user's language in everything you write into the room.

## Handoff

After `rooms_create` (or `tools_make`) returns:

1. Give the public room URL (`links.preview` or `shareUrl`) and label it **Preview**.
2. Report every entry in `skipped` and the reason WZRD supplied. If `skipped` is empty, say that nothing was skipped.
3. Give the private editor / claim link (`links.edit` or `claimUrl`) separately and label it **Edit & claim**. Explain that it opens the editor and lets them save the room to a WZRD account.
4. Say what you assumed and what the user may want to fill in.

Never combine or confuse Preview with Edit & claim.
