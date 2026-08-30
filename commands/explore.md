---
description: Start a Northlit exploration — a board of design direction mocks from a brief
argument-hint: <design brief — product, audience, vibe, any reference image URLs>
---

Run a Northlit design exploration for this brief:

$ARGUMENTS

Use the northlit MCP tools:

1. If you haven't this session, call `whoami` — note the credit balance and default project.
2. Call `create_exploration` ONCE with the full brief. Pass reference image URLs via referenceImageUrls (for local files, `upload_reference_image` first), style presets via styleIds, and a projectId only if the user named one.
3. Poll `check_progress` every 10–20 seconds until phase "ready" — never block.
4. When mocks land: `list_directions`, then `view_mock` the two or three strongest so they render inline, and share the board's openUrl so the user can open it in Northlit. If your client doesn't render the tool's image blocks (ChatGPT doesn't), ALSO include each mock as `![name](url)` verbatim in your reply — ChatGPT renders markdown images.

House rules:

- ONE exploration per brief. Remember the designRunId for the whole session; follow-ups belong on the SAME board — `add_directions` for more takes, `generate_variations` to iterate one card into children. A new exploration is only for a genuinely new brief.
- Billable tools spend the user's real credits. If a tool refuses with an upgrade payload, surface it to the user; don't retry past it.
