## ADDED Requirements

### Requirement: Single-file static page

The landing page SHALL be delivered as a single `index.html` file containing all HTML, CSS, and JavaScript inline. No build step, bundler, or framework SHALL be required. Google Fonts (via `<link>` in `<head>`) is the only permitted external dependency.

#### Scenario: Direct serving from GitHub Pages

- **WHEN** a visitor requests `https://mugdha.dev/`
- **THEN** the response is a single self-contained HTML document served by GitHub Pages
- **AND** no additional CSS, JS, or bundled asset files (other than fonts) are required to render the page

### Requirement: Canonical URL tag

The page SHALL include `<link rel="canonical" href="https://mugdha.dev/">` inside `<head>`.

#### Scenario: Canonical tag present

- **WHEN** a crawler or browser parses `index.html`
- **THEN** the `<head>` contains exactly one `<link rel="canonical">` element
- **AND** its `href` attribute equals `https://mugdha.dev/`

### Requirement: SEO-facing title and description mention whatifed.com

The page SHALL declare a `<title>` and a `<meta name="description">` that both reference `whatifed.com`, reinforcing the primary backlink purpose.

#### Scenario: Title and description

- **WHEN** a crawler parses `<head>`
- **THEN** `<title>` contains the substring `whatifed.com`
- **AND** `<meta name="description" content="...">` contains the substring `whatifed.com`

### Requirement: Followable backlink to whatifed.com

The page SHALL include at least one `<a href="https://whatifed.com">` in the rendered `<body>` that is visible to unassisted users and is NOT marked `rel="nofollow"`, `rel="ugc"`, or `rel="sponsored"`. This backlink is the primary SEO purpose of the site.

#### Scenario: Followable anchor present

- **WHEN** a crawler parses the page body
- **THEN** at least one `<a>` element has `href="https://whatifed.com"` or `href="https://whatifed.com/"`
- **AND** the element has no `rel` attribute, or its `rel` attribute does not contain `nofollow`, `ugc`, or `sponsored`
- **AND** the element is not hidden via `display: none`, `visibility: hidden`, `aria-hidden="true"`, or similar

### Requirement: Hero section

The page SHALL open with a hero section containing the owner's full name, current role (title + company), and a short bio (2–3 sentences). The bio SHALL mention `whatifed.com` as a hyperlink.

#### Scenario: Hero content is present

- **WHEN** the page loads
- **THEN** the first visible content includes the text `Mugdha Adhav`
- **AND** includes a role phrase referencing `Engineering Manager` and `Acquia`
- **AND** includes a bio paragraph that links to `https://whatifed.com`

### Requirement: Experience section

The page SHALL include an `<ol>`, `<ul>`, or equivalent semantic list presenting professional experience in reverse-chronological order. Each entry SHALL include role title, company, date range, location, and 2–4 short bullets.

#### Scenario: Experience entries rendered

- **WHEN** the page loads
- **THEN** the body contains entries for these four positions, in this order:
  1. Engineering Manager at Acquia (Nov 2025 – Present, Remote)
  2. Senior Software Engineer at Acquia (Dec 2020 – Nov 2025, Remote)
  3. Software Engineer at InfraCloud Technologies (Jan 2019 – Dec 2020, Pune)
  4. Programmer Analyst at Cognizant (Oct 2017 – Dec 2018, India)
- **AND** each entry contains 2–4 bullet points

### Requirement: Links section

The page SHALL include a links section with exactly three destinations, and no others: `https://whatifed.com`, `https://github.com/mugdha-adhav`, and `mailto:mugdha.adhav@gmail.com`. LinkedIn, Twitter, or other social links SHALL NOT appear on this page; those live on the GitHub profile.

#### Scenario: Exactly three non-whatifed, non-GitHub, non-email links are absent

- **WHEN** the page loads
- **THEN** the links section (or equivalent) contains anchors for `whatifed.com`, `github.com/mugdha-adhav`, and `mailto:mugdha.adhav@gmail.com`
- **AND** no anchor in that section targets `linkedin.com`, `twitter.com`, `x.com`, or any other social platform

### Requirement: Dark theme visual treatment

The page SHALL render as a dark theme by default — a deep navy/slate background, light foreground text, and a single accent color (e.g. teal) used for links and interactive states. A light-mode toggle or `prefers-color-scheme: light` override is NOT required for v1.

#### Scenario: Dark theme on initial load

- **WHEN** the page is loaded in a fresh browser with no color-scheme preference set
- **THEN** the rendered `<body>` background is a dark color (luminance below ~20%)
- **AND** body text is light (luminance above ~70%)
- **AND** interactive elements (links, hover states) use a single accent color

### Requirement: Typography via Google Fonts

The page SHALL use a distinctive typographic pairing loaded from Google Fonts — a sans-serif for display and body text and a monospace for small labels (dates, role metadata). Generic system stacks alone SHALL NOT be the primary typefaces.

#### Scenario: Fonts loaded

- **WHEN** the page loads
- **THEN** `<head>` contains a `<link rel="stylesheet" href="https://fonts.googleapis.com/css2?...">` that loads at least one sans-serif and one monospace family
- **AND** the body text's computed `font-family` resolves to the loaded sans-serif before any system fallback

### Requirement: Accessibility baseline

The page SHALL meet a baseline of static accessibility: semantic landmarks (`<main>`, `<nav>` where appropriate, `<header>`, `<footer>`), visible focus indicators on all interactive elements, sufficient contrast for body text (WCAG AA ≥ 4.5:1), and respect for `prefers-reduced-motion`.

#### Scenario: Keyboard focus visible

- **WHEN** a keyboard user tabs through the page
- **THEN** each focusable element displays a visible focus ring
- **AND** focus order follows DOM order top-to-bottom

#### Scenario: Reduced-motion respected

- **WHEN** the OS or browser sets `prefers-reduced-motion: reduce`
- **THEN** entrance animations and transitions are disabled or reduced to sub-perceptible durations

### Requirement: Restrained entrance animation only

The page SHALL include at most one entrance animation (e.g. a fade-in of the hero and subsequent sections) on initial load. Continuous, scroll-triggered, or hover-driven animations on body content SHALL NOT be used in v1.

#### Scenario: Single entrance animation

- **WHEN** the page first loads with `prefers-reduced-motion: no-preference`
- **THEN** content fades in within the first ~400ms after load
- **AND** no further animations trigger during scrolling or hovering (link color transitions excepted)
