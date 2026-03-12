# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML/CSS marketing website for **PragmaApps**, an AI-first software consulting company. No build system, package manager, or backend — all files are served as-is directly in the browser.

**Contact info used across all pages:**
- Email: `info@pragmaapps.com`
- Address: `D-84, Sector 2, Noida, Uttar Pradesh 201301`

## File Structure

| File | Description |
|---|---|
| `LandingPage.html` | Main landing/home page |
| `ProductDevelopmentPage.html` | Service page — Product Development |
| `DigitalTransformationPage.html` | Service page — Digital Transformation |
| `EnterpriseIntegrationPage.html` | Service page — Enterprise Integration |
| `AIAndMLPage.html` | Service page — AI & Machine Learning |
| `CTOAsAServicePage.html` | Service page — CTO as a Service |
| `PerformanceEngineeringPage.html` | Service page — Performance Engineering |
| `GovmatesCaseStudyPage.html` | Case study — Govmates |
| `InscopixCaseStudyPage.html` | Case study — Inscopix |
| `LifeSherpaCaseStudyPage.html` | Case study — LifeSherpa |

## Design System

All CSS is embedded inside `<style>` tags within each HTML file — there is no shared external stylesheet. Every change must be applied to each file individually.

### CSS Variables (defined in `:root` on every page)

```css
--black: #0a0a0a
--black-soft: #1a1a1a
--black-mid: #2c2c2c
--red: #d72638
--red-dark: #b01e2d
--red-light: #f5e0e3
--white: #ffffff
--gray-50 / --gray-100 / --gray-200 / --gray-300 / --gray-500 / --gray-700
--font: 'Plus Jakarta Sans', sans-serif
--radius: 12px
--shadow-sm / --shadow-md / --shadow-lg
```

### Section Background Pattern (Service Pages)

Every service page follows this exact background sequence:

| Section | Background |
|---|---|
| Hero | `var(--black)` (dark) |
| Approach ("Our Process") | `var(--white)` |
| Results | `var(--gray-50)` |
| Case Study | `var(--white)` |
| Contact | `var(--gray-50)` |

When the Contact section uses `var(--gray-50)`, the inner `.contact-card` and `.contact-form` must use `var(--white)` for contrast.

## Service Page Architecture

Each service page is structured as:

1. **Fixed header** — white background (`rgba(255,255,255,0.95)`), starts with class `scrolled`. Logo: `Pragma<span>Apps</span>` — the nav span has no inline style (red via CSS), but the footer logo uses `style="color: white;"` on both the `<a>` and `<span>` to override the CSS.
2. **Hero section** — dark split-screen layout
3. **Approach section** — light theme ("Our Process" with steps)
4. **Results section** — gray-50 background with metrics
5. **Case Study section** — white background
6. **Contact section** — gray-50 background with form
7. **Footer** — dark background (`var(--black)`)

### Dark Split-Screen Hero (`.hero-inner`)

The hero uses a two-column CSS grid:

```css
.hero { background: var(--black); min-height: 94vh; padding-top: 100px; }
.hero-inner { display: grid; grid-template-columns: 1fr 1fr; gap: 72px; }
```

The right column is `.hero-visual` containing absolutely-positioned floating cards using the `.hv-*` CSS class family:

- `.hv-phase` — pipeline steps (e.g. Assess → Map → **Automate** → Monitor → Scale)
- `.hv-code` — code/config snippet card (mid-left)
- `.hv-ai` — status/health card (mid-right)
- `.hv-metrics` — metrics card (bottom-left)
- `.hv-delivery` — badge (bottom-right)

### Approach Section Light Theme

When converting an approach section from dark to light, these CSS properties need updating:

- `.approach-section { background: var(--white); }`
- `.approach-step-content`, `.approach-step-number` — remove dark backgrounds, use light colors
- `.approach-visual-header { border-bottom: 1px solid var(--gray-200); }`
- `.approach-metric { background: var(--white); border: 1px solid var(--gray-200); }`
- `.approach-metric-value { color: var(--black); }`
- `.approach-quote-text { color: var(--gray-700); }`
- `.approach-nav-btn { border: 2px solid var(--gray-300); color: var(--gray-700); }`
- `.approach-nav-counter .current { color: var(--black); }`

## Footer Logo Fix

All pages use `.logo span { color: var(--red); }` globally and `.logo { color: var(--black); }`. Since the footer has a dark background, the footer logo anchor and span both need inline overrides:

```html
<a href="LandingPage.html" class="logo" style="color: white;">Pragma<span style="color: white;">Apps</span></a>
```

Without `style="color: white;"` on the `<a>` tag, "Pragma" renders black (invisible on dark footer).

## Contact Section HTML Pattern

The contact info block used across all pages:

```html
<div class="contact-item">
    <div class="contact-item-icon">✉️</div>
    <div>
        <div class="contact-item-label">Email</div>
        <div class="contact-item-val"><a href="mailto:info@pragmaapps.com">info@pragmaapps.com</a></div>
    </div>
</div>
<div class="contact-item">
    <div class="contact-item-icon">📍</div>
    <div>
        <div class="contact-item-label">Location</div>
        <div class="contact-item-val">D-84, Sector 2, Noida, Uttar Pradesh 201301</div>
    </div>
</div>
```

Footer contact column:

```html
<a href="mailto:info@pragmaapps.com">info@pragmaapps.com</a>
<a href="#">D-84, Sector 2, Noida, Uttar Pradesh 201301</a>
```

## Page Titles

Each page has a unique `<title>` tag:

- Landing: `PragmaApps – AI-First Software Development`
- Product Development: `Product Development – PragmaApps`
- Digital Transformation: `Digital Transformation – PragmaApps`
- Enterprise Integration: `Enterprise Integration – PragmaApps`
- AI & ML: `AI &amp; Machine Learning – PragmaApps`
- CTO as a Service: `CTO as a Service – PragmaApps`
- Performance Engineering: `Performance Engineering – PragmaApps`
