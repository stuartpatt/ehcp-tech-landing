# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**ehcp.tech** is a static validation landing page for an EHCP (Education, Health and Care Plan) evidence scoring tool. Its sole purpose is to validate product-market fit before building the full product. The site is hosted on GitHub Pages with a custom domain (`ehcp.tech`).

**Success criteria:** 30+ email signups and 5%+ CTA click-through rate within 2 weeks.

## Architecture

This is a zero-dependency static site — plain HTML5, CSS3, and vanilla JavaScript with no build step, no bundler, no framework.

```
ehcp.tech/
├── CNAME              # Custom domain: ehcp.tech
├── index.html         # Landing page (inline CSS/JS)
├── thanks.html        # Post-signup confirmation
└── tidy-inventing-zephyr.md  # Implementation plan (reference doc)
```

### Key Integrations

- **Email capture:** Buttondown (free tier, embeddable HTML form, redirects to thanks.html)
- **Analytics:** Plausible Analytics (cookieless — no consent banner needed)
- **A/B testing:** URL parameter + localStorage variant assignment (~20 lines JS), tagged in Plausible events
- **Hosting:** GitHub Pages (main branch, root folder)

## Design System

Reuses tokens from the parent `ehcp.ai` project's design system:

| Token | Value |
|-------|-------|
| `--page-bg` | `#fafaf9` |
| `--card-bg` | `#ffffff` |
| `--text-primary` | `#1c1917` |
| `--accent` | `#3b82f6` |
| `--success` | `#16a34a` |
| `--error` | `#dc2626` |
| `--warning` | `#f59e0b` |
| Font stack | `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif` |
| Card radius | `16px` |
| Button radius | `8px` |

## Content Sensitivity Rules (Non-Negotiable)

The target audience is SEND parents — tone must be empathetic and honest:

- No fear-based marketing language
- No promises about EHCP outcomes
- No "AI-powered" in headlines
- No children as marketing props
- Frame professionals as allies, not adversaries
- No legal advice — include disclaimer per CEO Advisor framework

## Development

No build commands. Open `index.html` in a browser or use any local server:

```bash
# Serve locally
python3 -m http.server 8000
```

There are no tests, linters, or CI pipelines — the site is pure static HTML.

### DNS Configuration (for reference)

- CNAME: `www` → `<username>.github.io`
- A records (apex): `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`

## Analytics Events

| Event | Trigger |
|-------|---------|
| `CTA_Click` | User clicks main CTA button |
| Page view | Automatic (Plausible) |
| UTM tracking | Automatic via URL parameters |

UTM sources: `facebook`, `linkedin`, `mumsnet`, `direct`

## Related Projects

- **ehcp.ai** — Private Python FastAPI backend (the actual product this page validates)
