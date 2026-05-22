# Inbox &amp; Diary — TMRW Lifecycle Marketing Briefing

A static HTML dashboard analysing every email sent from TMRW's HubSpot — workflows, broadcasts, and 1-to-1 sales — with strategic recommendations for lifecycle marketing.

Data was pulled live from HubSpot via MCP on **22 May 2026** and is baked into the page (no live API calls, no auth, no flaky loading states).

---

## Deploy to Vercel via GitHub (5 minutes)

### Step 1 — Push to GitHub

1. Create a new GitHub repo (e.g. `hubspot-dashboard`) at <https://github.com/new>. You can keep it private.
2. From this folder in your terminal:
   ```bash
   git init
   git add .
   git commit -m "Initial dashboard"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/hubspot-dashboard.git
   git push -u origin main
   ```

### Step 2 — Connect to Vercel

1. Go to <https://vercel.com/new>.
2. Click **Import Git Repository** and select your `hubspot-dashboard` repo.
3. Vercel will auto-detect this as a static site. Leave all settings at default — **no framework, no build command, no install command needed**.
4. Click **Deploy**.

That's it. In about 30 seconds you'll have a live URL like `https://hubspot-dashboard-yourname.vercel.app`.

### Step 3 — Custom domain (optional)

In your Vercel project → **Settings → Domains** → add a domain you own (e.g. `dashboard.startmytomorrow.com`). Vercel will give you the DNS record to add.

---

## Updating the data

When you want fresh numbers:

1. Ask Claude to "refresh the HubSpot dashboard data".
2. Claude pulls the latest numbers from HubSpot via MCP.
3. Claude updates the `DATA` constants and key narrative numbers in `index.html`.
4. Push the changes:
   ```bash
   git add index.html
   git commit -m "Refresh data — $(date +%Y-%m-%d)"
   git push
   ```
5. Vercel auto-deploys the update within ~30 seconds.

---

## What's in the report

The page is a long-scroll editorial briefing with 6 sections:

1. **Hero** — total volume (2,579 emails) and channel split
2. **Engagement funnel** — sent → opened → clicked, with industry benchmarks
3. **Channel anatomy** — marketing vs sales breakdown
4. **Workflow catalog** — decoded naming convention for every active workflow (`[OB-x]`, `[1.x]`, `[CP-x]`, `[XP-x]`, `GOV-x`, Weekly Science Email)
5. **Engagement health** — 4 cohorts (active/casual/drifting/opted-out) plus distribution chart and top recipients
6. **Strategic recommendations** — 6 ranked actions to take, derived from data patterns
7. **Methodology &amp; gaps** — what was queried, what's missing, what to pull next

---

## File structure

```
hubspot-dashboard/
├── index.html       # The entire dashboard (single file, no dependencies)
└── README.md        # This file
```

No build step. No npm install. No framework. Just HTML, CSS, and inline SVG charts — fully self-contained except for Google Fonts loaded from CDN.

---

## Tech notes

- Pure HTML + CSS + minimal vanilla JS
- Fonts: Fraunces (editorial serif) + Inter Tight (sans) + JetBrains Mono — all from Google Fonts
- Charts: hand-coded inline SVG (no library)
- Responsive down to ~380px (mobile)
- Print-friendly stylesheet
- Smooth-scroll navigation, IntersectionObserver-based reveal animations
- Should score 95+ on Lighthouse without any tuning
