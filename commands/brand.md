---
description: Design on-brand — read Northlit brand DNA before generating
argument-hint: [brand name, or what to make on-brand]
---

Work on-brand with Northlit:

$ARGUMENTS

1. `list_brands` → `read_brand` for the brand in play. Read the DNA — palette, type, voice, logos — BEFORE designing anything.
2. Logo physics, so you set expectations honestly: the real logo file only enters image generation when read_brand shows locked: true AND logoInGen: true (the "use logo in generation" toggle in the Brand DNA panel) — otherwise models redraw the mark from description. `generate_image` with `brandId` carries the whole DNA and places the REAL logo file after generation — exact on every image. Say where in plain words ("small logo bottom right") or with `logoPlacement` / `logoSize`; never describe the logo's look. Where the model draws the mark itself (boards, `logoPlacement: "in-scene"`), it is close, never exact. HTML prototypes use the true SVG exactly. There is no Studio logo swap — don't promise one.
3. Generate with the brand in context — `create_exploration` or `generate_image` — and check the output against the DNA before presenting it.
