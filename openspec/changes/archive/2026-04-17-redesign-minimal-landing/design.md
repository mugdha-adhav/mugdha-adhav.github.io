## Context

`mugdha.dev` is a single static HTML page deployed via GitHub Pages. The current design is an editorial/magazine treatment generated from the `frontend-design` plugin without the owner's sign-off; it does not match the owner's taste. The reference aesthetic for this change is [`brittanychiang.com`](https://brittanychiang.com) — dark, typography-forward, restrained, typography as the primary visual interest.

Infrastructure is already stable: four A records on Cloudflare pointing to GitHub Pages, DNS-only (no CF proxy), Let's Encrypt HTTPS enforced. This change is content/presentation only.

## Goals / Non-Goals

**Goals:**
- Replace `index.html` with a minimal, dark, typography-forward single-page landing that feels intentional.
- Keep (and strengthen) the followable backlink to `whatifed.com`.
- Present a compact, reverse-chronological experience list backed by the owner's real resume.
- Make this an intentional v1 — visibly smaller than the brittany-chiang reference so future iterations have headroom to grow.

**Non-Goals:**
- Sidebar nav, spotlight cursor, multi-section scroll-snap, projects grid, archive page.
- Build tooling, frameworks, external JS libraries.
- Light-mode theming; dark only for v1.
- LinkedIn / Twitter links on the page itself (GitHub profile is the bio hub).

## Decisions

### D1: Single-column vertical layout
**Choice:** One centered column, ~40rem max width, everything stacked vertically: hero → bio → experience → links.
**Alternatives considered:**
- Two-column (brittany's sidebar + content). Rejected: explicitly out of scope for v1.
- Grid-based "cards". Rejected: doesn't match the restrained reference.
**Why:** Pushes the reader into a linear read of name → bio → experience → links without visual noise.

### D2: Dark palette with a single accent
**Choice:** Deep navy/slate background (`#0a192f` family), slate-100 primary text, slate-400 muted text, single teal accent (`#64ffda`) for links and hover states. Matches the brittany reference closely but is not a copy.
**Alternatives considered:**
- Off-black with warm accent (e.g. amber). Rejected: user already rejected the warm-editorial direction.
- Pure black (`#000`). Rejected: too stark, reduces legibility of dark text.
**Why:** Closely evokes the reference without being derivative. Teal on navy is high-contrast and passes WCAG AA for body text.

### D3: Typography — display + body + mono
**Choice:** Display/body: **Inter** (weights 400/500/600). Mono (for role titles, dates, technical tags): **JetBrains Mono**. Both via Google Fonts.
**Alternatives considered:**
- Instrument Serif / Geist (from previous redesign). Rejected: carries the editorial mood the user rejected.
- Fraunces / Newsreader. Rejected: serifs pull toward editorial feel.
- System stack only. Rejected: loses distinctiveness.
**Why:** Inter is what the reference uses, and JetBrains Mono for small monospace labels is an established brittany-ish touch. Keeps feel close to reference without cloning it.

### D4: Minimal motion
**Choice:** A single entrance fade-in on page load (~400ms, respecting `prefers-reduced-motion`). No scroll-triggered animations, no hover-driven page effects beyond link color transitions.
**Alternatives considered:**
- Staggered per-section fade-in. Rejected: too busy for v1.
- No animation at all. Rejected: a single restrained entrance adds polish without noise.

### D5: Experience list as semantic `<ol>`
**Choice:** Use an ordered list `<ol>` with each `<li>` containing role, company, mono-styled dates, location, and a short `<ul>` of 2–4 bullets. Dates use `<time datetime="...">` where practical.
**Alternatives considered:**
- `<dl>` (definition list). Rejected: awkward for multi-field entries with bullets.
- Divs only. Rejected: weakens semantics for screen readers.
**Why:** Semantic, accessible, and preserves the reverse-chronological ordering.

### D6: Three links only, inline row
**Choice:** A single `<nav>` row or `<ul>` of three links: `whatifed.com` (featured), `GitHub`, `Email`. No icons for v1 (keeps footprint small); rely on clear anchor text.
**Alternatives considered:**
- Include LinkedIn + Twitter. Rejected by user — GitHub profile is the bio hub.
- Use SVG icons per link. Rejected: adds markup and complexity without enough payoff in v1.

## Risks / Trade-offs

- **[Risk]** Visual result still misses user's taste → **Mitigation**: proposal review (this doc) and preview before commit; additional iteration allowed through follow-up OpenSpec changes.
- **[Risk]** Minimal content (just bio + experience) feels too bare → **Mitigation**: accepted trade-off for v1; Projects/Archive sections are planned future changes.
- **[Risk]** Close resemblance to `brittanychiang.com` could read as derivative → **Mitigation**: differ in layout (single column vs sidebar), typography proportions, and accent saturation; the reference is a starting point, not a template.
- **[Trade-off]** No projects section means repeat visitors see the same page. Acceptable for v1; projects is a planned follow-up.
- **[Trade-off]** Dark-only. Some visitors prefer light. Acceptable for v1; light-mode is a small follow-up if requested.

## Migration Plan

1. Implement `index.html` rewrite on a feature branch or directly on `main` (this is a single-contributor personal repo — direct commits are acceptable).
2. Push to `origin/main`. GitHub Pages rebuilds automatically.
3. Verify live content with `curl -sS https://mugdha.dev | grep -E '<title>|whatifed|Acquia'`.
4. Manually visually inspect in a browser (hard refresh to bypass cache).
5. **Rollback**: if the result is rejected, revert the commit or open a follow-up OpenSpec change. Git history is the rollback mechanism — no other infra to unwind.

## Open Questions

- **Q1**: Should the location for each experience entry be shown (e.g. "Remote" for Acquia)? Decision: yes, it's part of the entry schema; small monospace label.
- **Q2**: Should the email be a plaintext link or obfuscated to reduce scrape risk? Decision: plaintext `mailto:` for v1 — the address is already public in git commit metadata.
- **Q3**: Should an OG image be added? Decision: deferred to a follow-up change (adds files to the repo).
