# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

## What this repo is

This is the `jakerains/jakerains` GitHub profile README repository. Its sole purpose is to render a custom profile page at https://github.com/jakerains. The `README.md` in `main` is automatically displayed on the GitHub profile.

## Making changes

Edit `README.md` and push to `main` — GitHub renders it live within seconds. No build step, no dependencies.

```bash
git add README.md && git commit -m "your message" && git push
```

For image assets, add to `assets/` and reference via raw GitHub URL:
```
https://raw.githubusercontent.com/jakerains/jakerains/main/assets/filename.ext
```

## Image assets

All images live in `assets/`. Current inventory:

| File | Used for |
|---|---|
| `header-banner-jake.png` | Full-width header (Jake avatar + cosmic builder poster + "Building cool things") — **active** |
| `jake-workstation.png` | Bio section float-right image — **active** |
| `header-banner-v4.png` | Superseded header (alien + nebula + title text + speech bubble) — keep for reference |
| `alien-workstation.png` | Superseded bio image — keep for reference |
| `kain-github.jpeg` | Original reference image for the alien character — use as `--image` input when generating new assets |
| `header-banner.png`, `v2`, `v3` | Superseded header iterations — keep for reference |
| `alien-coder.png` | Superseded bio image |

## Generating new images

Prefer the built-in `imagegen` tool for normal image generation and editing. It runs from the current Codex session and does not require `OPENAI_API_KEY`.

The CLI fallback exists at `~/.Codex/skills/imagegen/scripts/image_gen.py` and requires `OPENAI_API_KEY`; use it only when explicitly requested.

```bash
# Generate new image
python3 ~/.Codex/skills/imagegen/scripts/image_gen.py generate \
  --prompt "..." --model gpt-image-1 --size 1024x1024 --quality high --out assets/name.png

# Edit/composite from reference (e.g. keep alien character accurate)
python3 ~/.Codex/skills/imagegen/scripts/image_gen.py edit \
  --prompt "..." --image assets/kain-github.jpeg --size 1536x1024 --quality high --out assets/name.png
```

Valid sizes for `gpt-image-1`: `1024x1024`, `1536x1024`, `1024x1536`

For Jake avatar assets, use `/Users/jakerains/Downloads/Jake-cartoon-pic.jpeg` as the identity reference when available: black knit beanie, big glossy eyes, full beard with gray streaks, green shirt, cheerful cartoon style.

Use `kain-github.jpeg` as the reference `--image` only when the alien character needs to appear, to keep him on-model (green, big dark eyes, two antenna balls, cartoon style).

## Contribution snake

The snake SVG is auto-generated daily by `.github/workflows/snake.yml` via `Platane/snk@v3` and pushed to the `output` branch. The README references it with a `<picture>` element that swaps light/dark variants based on `prefers-color-scheme`.

To manually re-trigger: Actions tab → "Generate Contribution Snake" → "Run workflow".

The workflow requires `permissions: contents: write` on the job (already set) — without it, the git push to `output` fails with exit code 128.

## Design system

Color palette used throughout badges, stats cards, and snake:
- Purple: `#A78BFA` (primary accent)
- Cyan: `#06B6D4` (secondary accent)
- Dark violet: `#7C3AED`
- Background: `#0D1117` (GitHub dark)

Stats cards use `theme=tokyonight` with `hide_border=true` and `bg_color=0D1117`.

## What to avoid

- **Third-party SVG card services** (`github-readme-stats.vercel.app` pin cards, `github-profile-trophy.vercel.app`) — these are rate-limited and break unpredictably. Use plain markdown tables instead.
- **Capsule Render** for the header — replaced with a custom generated image.
- **External GIFs** (giphy URLs) — replaced with repo-hosted assets.

## Profile content sources

Project data and descriptions are sourced from https://jakerains.com/projects. When updating the Shipped Projects or Open Source & Tools tables, scrape that page to get current descriptions and links rather than guessing.
