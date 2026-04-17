## Why

The current `index.html` is an editorial/magazine-styled landing page that doesn't match the owner's taste or intent. `mugdha.dev` needs a minimal, dark, typography-forward landing page that (a) provides a prominent, followable SEO backlink to `whatifed.com` and (b) reads like a lightweight personal introduction for visitors who land there from search or GitHub.

## What Changes

- **BREAKING**: Replace the existing `index.html` in its entirety with a new minimal dark-themed landing page.
- Add a hero section with name, current role ("Engineering Manager at Acquia"), and a 2–3 sentence bio that mentions `whatifed.com` as a followable link.
- Add an experience list with four reverse-chronological entries (Acquia EM, Acquia SSE, InfraCloud SWE, Cognizant PA). Each entry has role, company, dates, location, and 2–4 short bullets.
- Add a single links row with exactly three destinations: `whatifed.com`, `github.com/mugdha-adhav`, and `mailto:mugdha.adhav@gmail.com`. No LinkedIn or Twitter — those live on the GitHub profile.
- Retain site-level invariants: single-file static page, inline CSS/JS, Google Fonts only, `<link rel="canonical">` pointing at `https://mugdha.dev/`, whatifed.com link must not carry `rel="nofollow"`.
- **Non-goals** (explicitly out of scope for v1): sidebar, spotlight cursor effect, Projects section, Archive page, dark/light toggle, external JS libraries, multi-page routing, build step.

## Capabilities

### New Capabilities

- `landing-page`: The visual, structural, and content contract for `index.html` — defines the sections, information architecture, link obligations (backlink to whatifed.com, GitHub-as-bio-hub), and the design system (dark theme, typography, single accent color).

### Modified Capabilities

<!-- None — this is the first OpenSpec change in the repo and introduces the first capability. -->

## Impact

- **Files touched**: `index.html` (rewritten), `openspec/` (bootstrapped with this change + future spec).
- **Deploy**: push to `main` triggers GitHub Pages rebuild; live at `https://mugdha.dev` within a few minutes. No infra changes.
- **External deps**: may add one Google Fonts stylesheet link (no change to build/tooling).
- **SEO**: preserves (and tightens) the followable backlink to `whatifed.com`; title and meta description continue to mention `whatifed.com`.
- **Accessibility**: must continue to pass basic contrast, focus, and semantic-landmark checks; must honor `prefers-reduced-motion`.
