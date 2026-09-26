---
description: Design on-brand — read Northlit brand DNA before generating
argument-hint: [brand name, or what to make on-brand]
---

Work on-brand with Northlit:

$ARGUMENTS

1. `list_brands` → `read_brand` for the brand in play. Read the DNA — palette, type, voice, logos — BEFORE designing anything.
2. Logo physics, so you set expectations honestly: the real logo file only enters image generation when read_brand shows locked: true AND logoInGen: true (the "use logo in generation" toggle in the Brand DNA panel) — otherwise models redraw the mark from description. `generate_image` with `brandId` places the REAL logo file in a corner after generation (`logoPlacement`, default top-left) — exact on every image, so don't describe the logo in the prompt. Where the model draws the mark itself (boards, `logoPlacement: "in-scene"`), it is close, never exact. HTML prototypes use the true SVG exactly. There is no Studio logo swap — don't promise one.
3. Generate with the brand in context — `create_exploration` or `generate_image` — and check the output against the DNA before presenting it.
