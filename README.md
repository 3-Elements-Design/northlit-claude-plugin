# Northlit for Claude Code

Drive [Northlit](https://northlit.ai) — an AI design studio — from Claude Code.
Explore a brief as a board of design direction mocks, build any direction into a
working HTML prototype, iterate conversationally, generate video, and publish to
a public URL. Everything lands in your Northlit workspace, on real canvases you
can open, edit, and share.

## One prompt, any agent

Not sure which route applies to you? Paste this into whatever agent you use
— Claude Code, Codex, ChatGPT, Cursor, VS Code — and it installs Northlit
the right way for itself, adds the design skill, and confirms the connection:

```text
Set up Northlit for me in this environment and confirm it works. Northlit is an AI design studio (boards of design-direction mocks, working HTML prototypes, images, video) exposed as an MCP server.

1. Connect the Northlit MCP server — remote HTTP at https://northlit.ai/api/mcp, OAuth 2.1 with dynamic client registration (a browser sign-in; no keys to paste). Use the route for the agent you are:
   - Claude Code: run `claude mcp add --transport http northlit https://northlit.ai/api/mcp` — or install the plugin with `/plugin marketplace add 3-Elements-Design/northlit-claude-plugin` then `/plugin install northlit@northlit`.
   - Codex CLI: run `codex plugin marketplace add 3-Elements-Design/northlit-codex`, then install Northlit from `/plugins` (or `codex mcp add northlit --url https://northlit.ai/api/mcp` then `codex mcp login northlit`).
   - ChatGPT: open Plugins, search "Northlit" and install it (or Plugins → + New Plugin with the server URL https://northlit.ai/api/mcp).
   - Cursor, VS Code, Windsurf, Gemini CLI or any other MCP client: add an HTTP MCP server named `northlit` with the URL https://northlit.ai/api/mcp. If the client cannot do OAuth, create an API key at https://northlit.ai/settings/api and send it as `Authorization: Bearer <key>`.
2. Install the northlit-design skill so design work follows my brand and my repo's DESIGN.md: clone https://github.com/3-Elements-Design/northlit-design-skill into your skills directory (Claude Code: `.claude/skills/northlit-design`; other agents: load its SKILL.md as context).
3. Verify: call the `whoami` tool (my plan and credits) and `getting_started`, then tell me what you found and how to start my first exploration. If I have no Northlit account yet, point me to https://northlit.ai — new accounts start with free credits.
```

## Install

```
/plugin marketplace add 3-Elements-Design/northlit-claude-plugin
/plugin install northlit@northlit
```

That's it — no API keys to paste. The plugin bundles Northlit's remote MCP
server (OAuth 2.1 with dynamic client registration): the first tool call opens a
browser consent, you sign in to your Northlit account, and your plan's models
and credits apply. Disconnect anytime by revoking the connection's access key in
[Settings → API](https://northlit.ai/settings/api).

No account yet? [northlit.ai](https://northlit.ai) — every account starts with
free trial credits.

## Commands

| Command | What it does |
| --- | --- |
| `/northlit:explore <brief>` | Start an exploration — a board of divergent design direction mocks from a brief. |
| `/northlit:image <prompt>` | Generate one image on its own editable canvas. |
| `/northlit:prototype` | Build a direction into a working HTML prototype and iterate on it. |
| `/northlit:video` | Animate an image into a video clip. |
| `/northlit:brand` | Read your brand DNA and design on-brand. |
| `/northlit:status` | Your plan, remaining credits, and recent work. |

The `northlit-designer` agent ships alongside them for work that wants its own
context — batch generation onto one canvas, long build-and-refine loops, or a
full brief-to-prototype pass.

## What the server exposes

61 tools, all acting as the signed-in user. Tools marked billable
spend the account's credits — the agent is told the balance up front (`whoami`)
and refusals carry an upgrade path instead of failing silently.

### Start here

- `getting_started` — The full guide: core loop, billing contract, tool reference.
- `whoami` — Your identity, plan, credits, admin flag, and default project.

### Workspace

- `list_projects` — Projects (brands/workspaces) you own or share.
- `list_runs` — Your explorations (mine) and boards shared with you (sharedWithMe), newest first.
- `list_moodboards` — Your moodboards, grouped by project.
- `list_brands` — Your brand libraries — id, name, locked state.
- `read_brand` — One brand's full DNA — palette, type, voice, logos.
- `list_design_systems` — Saved design systems — conform explorations via systemIds.

### Explorations & boards

- `create_exploration` — **billable** — Start a run from a brief — a board of direction mocks; returns openUrl + project.
- `check_progress` — Poll a run's pipeline phase and per-direction milestones.
- `generate_mocks` — **billable** — Generate board image mocks for directions without them.
- `add_directions` — **billable** — More TOP-LEVEL directions on an existing board (no parent card).
- `generate_variations` — **billable** — Child variations OF a card — attached under it, its image as edit base.
- `reparent_card` — Attach an orphan top-level card under another card (childless cards only).
- `list_directions` — Directions in a run with their mocks — renders as an inline gallery in ChatGPT.
- `read_direction` — One direction's full markdown.
- `read_run` — A run's AGENTS.md — the entry point before other reads.
- `read_moodboard` — A run's moodboard as markdown.
- `read_activity` — Reverse-chronological audit log of a run.
- `upscale_image` — **billable** — Upscale a direction's mock to 4K.
- `diff_directions` — Deterministic axis-by-axis diff of two directions.
- `critique_design` — **billable** — Principal-designer critique of a card — 0-100 scores, ranked issues, refine-ready fixPrompt.
- `present_board` — One composed side-by-side grid of a board's direction mocks — the comparison view for decision moments.

### Prototypes

- `build_prototype` — **billable** — Select a direction and build the full HTML prototype.
- `edit_prototype` — **billable** — Natural-language edit that lands as a new saved version.
- `list_prototype_versions` — A prototype's saved version history.
- `revert_prototype` — Make a prior version active (append-only).
- `read_prototype` — A prototype's overview, score, and version history.
- `read_prototype_html` — A prototype's raw rendered HTML.
- `read_chat` — The chat timeline for one direction.
- `publish_prototype` — Deploy a prototype to its public share URL.
- `unpublish_prototype` — Take a published prototype offline.
- `get_build_link` — Tokenized handoff URL any coding agent can fetch.
- `generate_prototype_image` — **billable** — Generate a hosted raster image INTO an existing prototype.
- `crop_mock_region` — Crop a region out of a direction's source mock (hosted URL).
- `view_mock` — See a direction's source mock — renders inline for the user too.

### Imagery

- `list_models` — Model catalog — image (flat 1 credit) + priced video models; ids feed generate_image / generate_video.
- `generate_image` — **billable** — ONE image from a prompt — lands on its own editable canvas; optional model pick.
- `upload_reference_image` — Rehost a local image (data URL) to a usable https reference URL.
- `view_image` — Render any Northlit-hosted image inline in the chat.
- `present_images` — Inline gallery widget of finished images — the display path for ChatGPT.
- `image_to_prompt` — **billable** — Reverse-prompt an image for ui/image/video scopes.

### Video & 3D

- `generate_video` — **billable** — Image-to-video render on the model registry.
- `check_video_status` — Poll a video job; the finished clip is billed on delivery.
- `save_video` — Persist a finished clip to a run — rehosted + indexed.
- `generate_3d` — **billable** — Turn a direction's mock into a 3D GLB model.

### Design knowledge

- `list_skills` — Catalog of design skills (name, description, when to use).
- `get_skill` — Full markdown body of one skill.
- `semantic_search` — Vector search across skills and run artifacts.
- `search_inspiration` — Vibe-search the curated inspiration gallery — free.
- `get_inspiration` — One inspiration item in full — prompt, image, palette; adapt via create_exploration.

### Design systems & exports

- `read_design_system` — A run's design system as markdown.
- `render_design_md` — Deterministic design.md from a system's spec block or a brand's DNA (brandId).
- `export_dtcg` — Deterministic W3C Design Tokens (DTCG) JSON export.

### Pixel-perfect kit

- `render_html` — Headless Chromium render of HTML to a PNG screenshot.
- `diff_against_mock` — **billable** — Render HTML and score it against a target mock with fixes.
- `ground_truth_hints` — OCR blocks, layers, and regions extracted from a mock.
- `pixel_perfect_html` — **billable** — Run the render→diff→fix loop until HTML matches a mock.

### Advanced (stateless)

- `analyze_moodboard` — **billable** — Stateless/advanced — vision analysis of moodboard images; saved nowhere.
- `generate_directions` — **billable** — Stateless/advanced — direction JSON only; saved nowhere.
- `generate_design_system` — **billable** — Stateless/advanced — design-system JSON from a direction; saved nowhere.

Resources: `skill://<name>`, `run://<id>`.

## Not using Claude Code?

The same server speaks to any MCP-capable harness — Claude (web/desktop),
Cursor, VS Code, ChatGPT, Windsurf, Gemini CLI:

- MCP endpoint: `https://northlit.ai/api/mcp` (Streamable HTTP, OAuth 2.1 + DCR)
- Per-harness instructions: [northlit.ai/settings/api](https://northlit.ai/settings/api)
- REST twin of every tool: [northlit.ai/api-reference.md](https://northlit.ai/api-reference.md)
- Agent-readable site map: [northlit.ai/llms.txt](https://northlit.ai/llms.txt)

## About this repo

This repo is generated from the Northlit codebase — the tool table above and
the command definitions derive from the same manifest that serves the live
server, so they can't drift from reality. Issues and feedback welcome here;
the plugin is regenerated and re-tagged when the server's surface changes.

License: MIT.
