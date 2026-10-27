---
name: build-a-room
description: Turn a conversation, documents, or a described job into a structured WZRD room. Use when the user asks to make, build, publish, or plan a WZRD room from a chat, thread, transcript, attachments, project files, links, or a job such as a proposal, client portal, investor update, menu or showroom. Do not use for ordinary summaries that are not intended to become a room.
---

# Build a room

Convert conversation and documents into an interactive, source-grounded WZRD room through the WZRD MCP. Pass the relevant conversation and notes to WZRD verbatim so the service can build from the complete source rather than from an intermediate summary.

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

Use the plugin's WZRD MCP server. Do not substitute a generic website builder, local mockup, direct private API call, or hand-authored “room” artifact. Claude must be signed in to WZRD (OAuth) before account tools run.

When the person describes a **job** (a proposal, client portal, investor update, menu, course…):

1. Call `templates_search` with that job and pick the closest template id.
2. Call `rooms_create` once with `prompt`, `context`, `files`, `images`, `websites`, and that `template` id when one fits.

When the person names a job a **WZRD tool** makes (an invoice, a quote, a pitch deck…), use `tools_make` with that tool and their answers; `tools_list` shows the tools and their questions.

When they only describe a room without naming a template, still call `templates_search` first when a finished outcome exists, then `rooms_create`.

Do not silently retry a response that may have created a room, because that could create a duplicate. If `rooms_create` fails before returning a result, report the failure and preserve the prepared request for a deliberate retry.

If the user shared more knowledge after creation, add it with `sources_add` or `knowledge_add_text`.

## Quality bar

- Send the selected conversation and notes verbatim in `context`; do not replace them with a summary.
- Keep documents as first-class source files rather than manually paraphrasing their contents.
- Do not invent names, prices, dates, proof points, permissions, integrations, or completed actions.
- Keep the user's language in everything you write into the room.
- By default, publishing from Claude can wait for approval. If `rooms_publish` returns `approval_required`, tell the user to approve it in the room's Studio rather than retrying.

## Handoff

After `rooms_create` (or `tools_make`) returns:

1. Give the public room URL (`links.preview`, `shareUrl`, or the published share link) and label it **Preview** when it is the visitor-facing link.
2. Report every entry in `skipped` and the reason WZRD supplied. If `skipped` is empty, say that nothing was skipped.
3. If the result includes a private editor / claim link (`links.edit` or `claimUrl`), give it separately and label it **Edit & claim**. Never combine or confuse Preview with Edit & claim.
4. Say what you assumed and what the user may want to fill in.
