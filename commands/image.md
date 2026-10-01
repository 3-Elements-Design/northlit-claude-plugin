---
description: Generate one image on an editable Northlit canvas
argument-hint: <image prompt>
---

Generate a single image with Northlit (no direction board):

$ARGUMENTS

1. Call `generate_image` once with the prompt. It's billed, hosted, and lands on its own editable canvas. For an exact size (an ad slot like 300x250 or 728x90) pass `width` + `height`.
   Making a SET — several ads, a series? Pass the `runId` from the first result on every later call so they all land on ONE canvas.
   An ad under a locked brand? Pass `brandId` and the ad's words in `copy` (headline, subhead, cta) — they're drawn in the brand's real font as a lettering reference, so the type matches the brand.
   Showing the brand's own product? Pass `product` — its name from the DNA's Products section, or an https URL of an official photo. Its photos ride as references and the product is drawn in one pass, lit by the scene, from a view the photos cover — close, not pixel-exact. If the result's `productCheck` lists differences, regenerate on the same canvas. Describe the scene, never the product. For a pixel-exact packshot, add `productMode: "exact"`.
2. Render the result inline with `view_image` and share the openUrl — the user can open it in the app to edit in Studio, upscale, animate, or share. If your client doesn't render image blocks (ChatGPT doesn't), include the result's `display` markdown line verbatim in your reply instead — ChatGPT renders markdown images.
3. Iterate on the SAME canvas: `generate_variations` makes children of this image. Don't create a new exploration for a tweak.

If the ask is really a design exploration — multiple directions, a brand, a whole page — use /northlit:explore instead.
