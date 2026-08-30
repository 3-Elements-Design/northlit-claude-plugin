---
description: Build a direction into a working HTML prototype
argument-hint: [runId or which direction, plus any build notes]
---

Build a Northlit prototype:

$ARGUMENTS

1. Locate the board: the session's designRunId, or `list_runs` if the user means an earlier exploration.
2. `list_directions`, and confirm WHICH direction to build if it's ambiguous — a build takes minutes and spends real credits.
3. `build_prototype`, then keep polling `check_progress`.
4. Inspect with `read_prototype` / `read_prototype_html`.
5. Iterate with `edit_prototype` — ONE focused change per call; each lands as a saved version. `list_prototype_versions` + `revert_prototype` are the undo stack.
6. `publish_prototype` only when the user wants it live (it creates a PUBLIC URL). `get_build_link` hands the build to any coding agent as tokenized markdown.
