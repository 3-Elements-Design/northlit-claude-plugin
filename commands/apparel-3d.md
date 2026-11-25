---
description: Turn garment views into a production 3D model — one Northlit generation, then local Blender finishes it true to the image or clean for a configurator
argument-hint: <a garment sheet or views — a file, an image URL, or a card on a canvas>
---

Make a production 3D garment with Northlit:

$ARGUMENTS

Read `get_skill` with name `apparel-3d` first — it carries both pipelines, the review loop, the checks and the limits. This needs Blender on this machine (`blender --version`; on macOS it is usually `/Applications/Blender.app/Contents/MacOS/Blender`). If it isn't installed, say so and stop before any billable step.

1. **Ask which finish they want** (skip if they already said): *true to the image* — keeps folds, wrinkles and printed detail — or *clean for a configurator* — a smoothed rebuild with separate recolourable pieces and flat pattern UVs for graphics; folds and printed artwork are not carried over.
2. Download the scripts once from `https://northlit.ai/downloads/apparel-3d/`: `crop_views.py`, `mesh_check.py`, `panels.py`, `bake.py`, `clean_build.py`, `clean_render.py`, `clean_uv_tex.py`, `clean_export.py`.
3. Views: upscale a generated sheet first with `upscale_image` (top-level cards only), crop the 4K sheet with `crop_views.py`, then bring each view in with `import_image` (pass the user's canvas `runId`) to get hosted URLs in the order front, right, back, left. Never send the whole sheet as one image.
4. One generation: `generate_3d` with those `imageUrls`, `model: "fal-ai/hunyuan-3d/v3.1/pro/image-to-3d"`, `enablePbr: true`, `faceCount: 40000`. Download the GLB. Don't generate a second model to compare.
5. **Check the mesh before any Blender work:** `mesh_check.py <GLB>`. If it reports a hole (`"ok": false`), generate once more with the same views (2 more credits — say so) and keep the mesh that passes or has the smaller hole.
6. **True to the image:** `panels.py` on the GLB, read `panels.json` and look at `panels_uv.png`, then `bake.py panels.blend <the same GLB> <out>`. Show `garment_panels.glb`.
7. **Clean for a configurator:** first compare the seams and stitch lines in the image with the generated model; where they disagree or the image is unclear, ask the user whether the image is correct, and if so follow the image in approximate placement. Then `clean_build.py <GLB> out/built.blend` (the GLB is only a shape reference; for long sleeves pass a PARAMS.json with `{"long_sleeve": true}`), render with `clean_render.py`, and have reviewers that haven't seen your verdict check shape and construction each iteration; fix through PARAMS.json and rebuild until clean. Then `clean_uv_tex.py`, `clean_export.py`, and a `demo` render to prove the pieces recolour separately. Show `garment_clean.glb`.
8. Put the finished model on the canvas with `create_scene` (`fromGlbUrl`, `runId`) and the UV, texture and render images with `import_image`.

One billable 3D step (two if the first mesh has a hole). Say what the renders and UV image show and which limits apply — a clean script run is not a correct model.
