# NeutralEye - Overview 

NeutralEye analyzes how news articles frame a story through tone, sourcing, emphasis, and omission. It is available as a web application and Chrome extension.

> This repository contains public technical documentation for NeutralEye. The production source code is maintained privately.

**Live**
- Web app: [tryneutraleye.com](https://tryneutraleye.com)
- Chrome extension: [NeutralEye - Bias Checker](https://chromewebstore.google.com/detail/neutraleye-bias-checker/fdkachmcdaebefhpkpjapoglbiakoffe)

## Overview

NeutralEye analyzes article text and returns a structured framing analysis across five signals:

- **Tone:** loaded or emotionally charged language
- **Framing:** what is emphasized or backgrounded
- **Attribution:** whether claims are clearly sourced
- **Source balance:** whether multiple relevant perspectives are represented
- **Omission:** important context that may be absent

Flagged signals are tied to quoted language from the article so users can check the analysis against the original text.

The system also classifies content as news, opinion, or analysis and adjusts its evaluation accordingly. Results include a confidence score and suggested sources covering the same story from other perspectives.

## Product Architecture

NeutralEye consists of a Next.js web application and a Chrome extension that use the same backend analysis system.

### Web Application

The web application uses Next.js with the App Router. Analysis, authentication, rate limiting, and saved history are handled through Next.js API routes and deployed on Vercel.

### Chrome Extension

The Chrome extension extracts article text from the active page and sends it through the same analysis API used by the web application, keeping analysis behavior consistent across both clients.

### Data and Authentication

Supabase provides PostgreSQL storage, authentication, Google OAuth, and Row Level Security for user-scoped analysis history.

### Analysis Pipeline

Article text passes through a two-stage OpenAI pipeline.

The first stage handles extraction and validation. The second performs the structured framing analysis.

The analysis distinguishes a journalist's own framing from quoted statements made by people in the article. Bylines and image captions are excluded before analysis, and news, opinion, and analysis content are evaluated using different standards.

## Infrastructure

- **Application:** Next.js, React
- **Database and Auth:** Supabase, PostgreSQL, Row Level Security
- **AI:** OpenAI API
- **Rate limiting:** Upstash Redis
- **Monitoring:** Sentry
- **Email:** Resend
- **Hosting:** Vercel
- **DNS/CDN:** Cloudflare
- **Extension:** Chrome Extensions API, Manifest V3

## Current Product

NeutralEye currently supports:

- Article analysis from pasted text or URLs
- Browser-based analysis through the Chrome extension
- Five-signal framing analysis with quoted evidence
- Content-type classification with adjusted evaluation standards
- Confidence scoring
- Suggested sources for cross-reading
- User accounts and saved analysis history
- Side-by-side comparison of framing across outlets

The application also includes protections around URL fetching, extension rendering, API access, rate limiting, CORS, and security headers.
