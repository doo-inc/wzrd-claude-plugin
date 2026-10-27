---
name: edit-a-room
description: Change an existing WZRD room in plain language — rewrite a headline, add or remove a section, update prices or dates, then publish and share it. Use when the user asks to edit, update, fix, publish, unpublish or share one of their WZRD rooms. Do not use to create a new room from a conversation (use build-a-room).
---

# Edit a room

1. **Find the room.** Use `rooms_search` with a name or phrase from the user, or `rooms_list`. If more than one room matches, ask which one.
2. **Read before you change.** Call `blocks_list` (or `rooms_get`) so you edit the right block by reference.
3. **Make the change.**
   - Change one block: `blocks_update`.
   - Add a section: `blocks_create` or `rooms_edit` with a position such as `{after: "pricing"}`.
   - Remove a block: `blocks_delete`. This is destructive, so confirm with the user first unless they asked for it directly.
   - Prose in an existing block: `rooms_write_text`.
   - A broad change described in words: `rooms_ai_edit`.
4. **Check it.** Call `rooms_history` and tell the user what changed. Every change can be reverted with `rooms_undo_change`.
5. **Publish or share when asked.** `rooms_publish` makes the room live, `share_link_create` returns its public link, and `rooms_unpublish` takes it offline.

People may be editing in the Studio at the same time. Use `presence_set` to show what you're working on. If an edit returns a conflict, read the room again and retry once.

By default, edits and publishing from Claude can wait for a person's approval. When a tool returns `approval_required`, tell the user it's waiting in the room's Studio. Do not invent names, prices, dates, or completed actions.
