# NeutralEye — AI-Powered Media Framing Analysis

NeutralEye is an AI product that shows readers how a news article frames a
story — not whether it's "biased," but how tone, framing, sourcing, and
omission shape the reader's perception. It ships as both a Chrome extension
and a full web application.

**Live:**
- Web app — [tryneutraleye.com](https://tryneutraleye.com)
- Chrome Web Store — NeutralEye, Bias Checker

## Overview

NeutralEye analyzes article text — pasted directly or pulled from a URL —
and returns a structured breakdown across five signals, checked together
in a single pass:

- **Tone** — loaded or emotionally charged language
- **Framing** — what's emphasized, what's backgrounded
- **Attribution** — whether claims are sourced or left unattributed
- **Source balance** — whether multiple perspectives are represented
- **Omission** — relevant context that's missing from the piece

Every flagged signal is tied to the exact quoted language from the
article that triggered it, so the analysis can be checked against the
source rather than taken on faith. Results also include a confidence
score, a content-type classification (news vs. opinion vs. analysis,
each held to different standards), and suggested sources covering the
same story from a different vantage point.

## Architecture

NeutralEye is a Next.js application with a Chrome extension as a second
client against the same backend.

### Web App
Built on Next.js (App Router), with the entire backend — analysis,
auth, rate limiting, history — implemented as Next.js API routes rather
than a separate server. Deployed on Vercel.

### Chrome Extension
A lightweight content script and popup that extract article text from
the active tab and call the same API routes the web app uses, so
analysis behavior is consistent across both surfaces. Distributed via
the Chrome Web Store.

### Database & Auth
Supabase (PostgreSQL) handles authentication — including Google
OAuth — and stores saved analysis history behind Row Level Security
policies scoped per user.

### AI Processing
Article text is run through a two-stage OpenAI pipeline: a lightweight
pass for extraction/validation, followed by the main structured
analysis call. The prompt explicitly excludes quotes from people
covered in the article (the analysis targets the journalist's framing,
not the opinions of sources being quoted), strips bylines and image
captions before scoring, and distinguishes news from opinion content
so persuasive writing in an op-ed isn't penalized the way it would be
in a straight news report.

### Infrastructure
- **Hosting:** Vercel
- **Database/Auth:** Supabase
- **Rate limiting:** Upstash Redis
- **Error monitoring:** Sentry
- **Transactional email:** Resend
- **DNS/CDN:** Cloudflare

## Current Features

- Article analysis via pasted text or URL, on web and in-browser via
  the extension
- Five-signal framing analysis with quoted evidence per signal
- News vs. opinion/analysis classification with adjusted scoring
  standards
- Confidence scoring
- Suggested sources for cross-reading the same story
- Account system with saved analysis history (Supabase Auth + Google
  OAuth)
- Compare Analyses — side-by-side framing comparison across outlets
  (Pro feature, gated preview live)
- Production security hardening: SSRF protections on URL fetching,
  sanitized HTML rendering in the extension, rate limiting, locked-down
  CORS, and standard security headers

## Project Status

NeutralEye has moved from a single-purpose Chrome extension into a full
product with a marketing site, web app, and shared backend:

- Live Chrome extension, published and in active use
- Live web application at tryneutraleye.com
- Unified backend serving both clients
- Authentication, saved history, and a gated Pro preview (Compare
  Analyses) shipped; Pro billing is not yet active — currently free
  during beta
- Security review completed and hardening fixes applied pre-launch
- Responsive design pass across mobile, tablet, and desktop

**Roadmap:** Stripe billing for Pro, analytics, and expanded
extension-side error monitoring.

## Technologies Used

**Languages:** JavaScript / TypeScript, SQL

**Framework:** Next.js (App Router), React

**Backend:** Next.js API routes, Supabase (PostgreSQL, Auth, RLS)

**AI / NLP:** OpenAI API, prompt engineering for structured JSON output

**Infrastructure:** Vercel, Cloudflare, Upstash Redis, Sentry, Resend

**Extension:** Chrome Extensions API (Manifest V3)

**Tooling:** Git, Claude Code
