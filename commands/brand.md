---
description: Design on-brand — read Northlit brand DNA before generating
argument-hint: [brand name, or what to make on-brand]
---

Work on-brand with Northlit:

$ARGUMENTS

1. `list_brands` → `read_brand` for the brand in play. Read the DNA — palette, type, voice, logos — BEFORE designing anything.
2. Logo physics, so you set expectations honestly: the real logo file only enters image generation when read_brand shows locked: true AND logoInGen: true (the "use logo in generation" toggle in the Brand DNA panel) — otherwise models redraw the mark from description. Even with the reference, raster generation redraws pixels: close, never vector-exact. HTML prototypes use the true SVG exactly; for raster finals, offer the Studio workflow (upscale, then swap in the true mark).
3. Generate with the brand in context — `create_exploration` or `generate_image` — and check the output against the DNA before presenting it.
