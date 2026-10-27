# WZRD `rooms_create` contract (Claude)

Call `rooms_create` on the WZRD MCP server declared in `.mcp.json` (`https://wzrd.to/api/mcp`). Claude connects with OAuth. Prefer `templates_search` before create when the user describes a finished job.

## Arguments

- `prompt`: one or two sentences describing what the room is for.
- `context`: the full relevant conversation and notes, verbatim, with speaker labels and original ordering. Maximum 400,000 characters. Do not substitute a summary.
- `files`: supported documents the user mentioned or attached.
- `images`: logos and pictures the user mentioned or attached.
- `websites`: site URLs WZRD should read.
- `template`: optional template id from `templates_search`.

Pass empty arrays for optional collections only when the tool schema requires them; otherwise omit empty optional fields.

## Files

Maximum 10 files, 25 MB each, and 50 MB total before the stricter whole-request limit is applied.

Supported document types: PDF, Word, PowerPoint, Excel, CSV, HTML, Markdown, and plain text.

- Local document: `{name, mimeType, base64}`. Read the exact bytes from disk and base64-encode them without textual conversion.
- Public document link: `{name, url}`.

Use the real filename and a specific MIME type when it can be determined. Do not place local filesystem paths in the MCP request.

## Images

Maximum 16 images and 5 MB per image. Supported formats: PNG, JPEG, WebP, and GIF.

- Local image: `{base64, alt}`.
- Public image: `{url, alt}`.

Write concise, useful alt text. Keep logos and pictures in `images`, not `files`.

## Websites

Pass at most 6 site URLs in `websites`. Use this for pages WZRD should read as sites. A public document download belongs in `files` as `{name, url}` instead.

## Size preflight

The complete serialized `rooms_create` request must stay under 40 MB. This is stricter than the 50 MB aggregate raw-file allowance, and base64 increases payload size. Measure or conservatively estimate the final request after encoding, including JSON, `context`, files, and images.

If limits are exceeded, do not truncate file bytes or silently omit a user-selected source. Ask the user which items to leave out or replace local files with public URLs where available.

## Call and response

Call `rooms_create` exactly once after preflight. Avoid automatic retries after an ambiguous network failure because the first request may already have created a room.

From the result:

- return `links.preview` or `shareUrl` as the public room link and label it **Preview** when it is visitor-facing;
- enumerate every item in `skipped` with the reason supplied by WZRD;
- if present, return `links.edit` or `claimUrl` separately and label it **Edit & claim**. Explain that it is the private link the user opens to edit the room and save or keep it.

Never include the Edit & claim URL in public content or describe it as a share link.

## Related tools

- `templates_search` — find a finished outcome for a job before creating.
- `tools_make` / `tools_list` — when the user names a job a WZRD tool makes (invoice, quote, pitch deck…).
- `sources_add` / `knowledge_add_text` — add more knowledge after create.
- `rooms_publish` / `share_link_create` — publish or share when asked; respect `approval_required`.
