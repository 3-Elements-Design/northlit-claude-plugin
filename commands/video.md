---
description: Animate an image into a video clip with Northlit
argument-hint: <what to animate and how it should move>
---

Create a video clip with Northlit:

$ARGUMENTS

1. Pick the source image: a direction's mock (`list_directions` / `view_mock`), an image generated this session, or any hosted https URL. No image yet? Generate one first (/northlit:image).
2. Optionally call `image_to_prompt` with scope "video" to turn the image into motion direction.
3. Call `generate_video` with the imageUrl and motion prompt.
4. Poll `check_video_status` with the URLs it returned, echoing the same model/duration/resolution — the finished clip is billed on the completed poll.
5. Call `save_video` to keep it: provider URLs expire, saving rehosts the mp4 durably onto the run.
