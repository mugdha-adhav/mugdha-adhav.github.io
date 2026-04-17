# mugdha.dev

Personal landing page deployed to GitHub Pages as a single static HTML file.

## Stack & constraints

- **Single file**: everything lives in `index.html` — inline CSS and JS, no build step.
- **No framework, no bundler, no npm.** Google Fonts is the only external dep acceptable.
- **Deploy**: any push to `main` triggers a GitHub Pages rebuild (source = `main` branch, root).
- **Domain**: `mugdha.dev` → 4x GitHub Pages A records, DNS-only on Cloudflare (no proxy).
- **HTTPS**: Let's Encrypt cert auto-issued and enforced by GitHub Pages.

## Files

- `index.html` — the only page. All HTML/CSS/JS inline.
- `CNAME` — GitHub Pages custom-domain config (`mugdha.dev`). GitHub rewrites this from the Pages settings UI, so avoid editing by hand.
- `.gitignore` — `.DS_Store`, editor dirs.

## Purpose

Personal landing page. Primary goal: provide a clean, indexable, followable backlink to `whatifed.com`. The GitHub profile (`github.com/mugdha-adhav`) is the hub for all bio/social links, so this page only links to GitHub, whatifed.com, and email.

## Design direction

Inspired by [brittanychiang.com](https://brittanychiang.com) — dark, typography-forward, restrained. Start minimal (hero + small resume/experience list) and grow from there. Do not ship the full multi-section portfolio in one go.

## Workflow

- Use **OpenSpec** (via the `openspec-*` skills) to propose and track changes before implementation.
- After any `index.html` edit, verify the live site with `curl -sS https://mugdha.dev | grep ...` once the Pages rebuild completes.
- Never use `rel="nofollow"` on the whatifed.com link — the backlink value is the whole point.
