---
description: Generate one image on an editable Northlit canvas
argument-hint: <image prompt>
---

Generate a single image with Northlit (no direction board):

$ARGUMENTS

1. Call `generate_image` once with the prompt. It's billed, hosted, and lands on its own editable canvas.
2. Render the result inline with `view_image` and share the openUrl — the user can open it in the app to edit in Studio, upscale, animate, or share.
3. Iterate on the SAME canvas: `generate_variations` makes children of this image. Don't create a new exploration for a tweak.

If the ask is really a design exploration — multiple directions, a brand, a whole page — use /northlit:explore instead.
