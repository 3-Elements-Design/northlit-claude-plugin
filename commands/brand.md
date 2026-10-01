---
description: Design on-brand — read Northlit brand DNA before generating
argument-hint: [brand name, or what to make on-brand]
---

Work on-brand with Northlit:

$ARGUMENTS

1. `list_brands` → `read_brand` for the brand in play. Read the DNA — palette, type, voice, logos — BEFORE designing anything.
2. Logo physics, so you set expectations honestly: the real logo file only enters image generation when read_brand shows locked: true AND logoInGen: true (the "use logo in generation" toggle in the Brand DNA panel) — otherwise models redraw the mark from description. `generate_image` with `brandId` carries the whole DNA and places the REAL logo file after generation — exact on every image. Say where in plain words ("small logo bottom right") or with `logoPlacement` / `logoSize`; never describe the logo's look. If the brand has both an icon and a wordmark, set up its logo kit with `update_brand_spec` `logoVariants` (icon / wordmark / stacked / badge, each for light or dark grounds; upload files with `upload_reference_image` first; the kit is identity, so ask) — then "icon only" or `logoLockup: "mark"` places the icon, and the wordmark is the default. Where the model draws the mark itself (boards, `logoPlacement: "in-scene"`), it is close, never exact. HTML prototypes use the true SVG exactly. There is no Studio logo swap — don't promise one. Products work the same way: list them in the DNA's Products section (`update_brand_spec` `products`, one line each with the official photo URL) and `generate_image` with `product` draws the real product from those photos (several angles, each labelled with its view) — close, with a `productCheck` against the photos; `productMode: "exact"` pastes the photo pixel-exact for packshots.
3. Generate with the brand in context — `create_exploration` or `generate_image` — and check the output against the DNA before presenting it.
