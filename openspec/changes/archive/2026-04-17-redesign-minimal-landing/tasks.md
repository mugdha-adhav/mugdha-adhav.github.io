## 1. Prepare

- [x] 1.1 Review proposal, design, and spec to confirm scope matches user approval
- [x] 1.2 Snapshot the current `index.html` by checking the current commit SHA (rollback reference)

## 2. Markup

- [x] 2.1 Rewrite `index.html` `<head>`: charset, viewport, title ("Mugdha Adhav — whatifed.com"), meta description (must mention whatifed.com), canonical tag to `https://mugdha.dev/`
- [x] 2.2 Add Google Fonts `<link>` loading Inter (400, 500, 600) and JetBrains Mono (400, 500)
- [x] 2.3 Build `<body>` skeleton: `<main>` wrapper with hero `<header>`, experience `<section>`, links `<nav>` or `<footer>`
- [x] 2.4 Hero: name `<h1>`, role line (title + company) in mono small-caps, bio paragraph with followable `<a href="https://whatifed.com">` (no rel attribute that blocks follow)
- [x] 2.5 Experience: `<ol>` with four `<li>` entries in reverse-chronological order (Acquia EM → Acquia SSE → InfraCloud → Cognizant); each entry has role, company, dates (in `<time>` elements where practical), location, and 2–4 `<ul>` bullets trimmed from the user's LinkedIn content
- [x] 2.6 Links: three anchors only — `whatifed.com`, `github.com/mugdha-adhav`, `mailto:mugdha.adhav@gmail.com`. No LinkedIn/Twitter/icons.

## 3. Styling

- [x] 3.1 Define CSS custom properties for the palette: deep navy background, slate body, muted slate for secondary text, single teal accent (e.g. `#64ffda`)
- [x] 3.2 Apply base styles: Inter as primary family, JetBrains Mono for `.mono` utility class, line-height 1.5–1.6, antialiased
- [x] 3.3 Layout: single centered column, `max-width` ~42rem, generous vertical rhythm (section spacing ~4rem, paragraph spacing ~1.25rem), responsive horizontal padding via `clamp()`
- [x] 3.4 Hero: large display `<h1>` using Inter 600 weight, role line in mono at a smaller size, bio paragraph at body size; whatifed.com link styled with accent color and underline on hover
- [x] 3.5 Experience entries: role as semi-bold Inter, company with accent color, dates/location in mono at small size, bullets with reduced `line-height` and subtle indent
- [x] 3.6 Links: inline row with adequate gap; hover/focus state swaps accent color; visible focus-ring using accent color outline
- [x] 3.7 Add exactly one entrance animation: overall `<main>` opacity + translate fade-in (~400ms); wrap in `@media (prefers-reduced-motion: no-preference)`
- [x] 3.8 Responsive tweaks: reduce type scale + adjust padding for mobile; confirm no horizontal overflow at 320px

## 4. Accessibility & semantics

- [x] 4.1 Confirm landmarks: one `<h1>`, `<main>`, and (as appropriate) `<header>`, `<section>`, `<nav>`, `<footer>` are present with correct roles implicit from tags
- [x] 4.2 Confirm body text contrast ≥ 4.5:1 on dark background (spot-check the slate foreground and accent hues)
- [x] 4.3 Confirm focus states are visible for every interactive element (tab through the page)
- [x] 4.4 Confirm `prefers-reduced-motion: reduce` disables or severely shortens the entrance animation

## 5. SEO & link invariants

- [x] 5.1 Grep the final HTML: `<title>` and `<meta name="description">` both contain `whatifed.com`
- [x] 5.2 Grep: `<link rel="canonical" href="https://mugdha.dev/">` exactly one occurrence
- [x] 5.3 Grep: `href="https://whatifed.com"` appears at least twice (bio + links section) and no occurrence has `rel=".*nofollow.*"`, `rel=".*ugc.*"`, or `rel=".*sponsored.*"`
- [x] 5.4 Grep: no anchor links to `linkedin.com`, `twitter.com`, `x.com`, or other social platforms

## 6. Deploy & verify

- [x] 6.1 Commit with a message describing the redesign and reference to the OpenSpec change name
- [x] 6.2 Push to `origin/main`; poll the GitHub Pages build status until `built` against the new commit SHA
- [x] 6.3 `curl -sS https://mugdha.dev` and grep for `Mugdha Adhav`, `Engineering Manager`, `Acquia`, and `whatifed.com` to confirm new content is live
- [ ] 6.4 Visual smoke check in a browser (hard refresh to bypass cache); confirm layout, palette, focus ring, and animation feel match the design
- [ ] 6.5 Report outcome back and archive the OpenSpec change with `openspec-archive-change`
