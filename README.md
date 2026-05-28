# ⚽ FIFA World Cup 2026 — Fan Hub

A standalone single-file fan dashboard for the 2026 FIFA World Cup, built for England supporters.

## Features

- **Live countdown** to the opening match (Mexico vs South Africa, Jun 11)
- **🏴󠁧󠁢󠁥󠁮󠁧󠁿 England banner** — pinned fixture tracker with W/D/L badges
- **All 12 groups** — with Group L highlighted, England starred as favourite team
- **Fixtures** — filterable by group or England-only, with auto-populated results
- **Venues** — all 16 host stadiums across USA, Mexico & Canada
- **Score predictor** — predictions auto-saved to `localStorage`, persists across sessions
- **Daily results refresh** — fetches live match results from the Anthropic Claude API once per day and caches them

## Setup

### 1. Clone / add to your repo
```bash
git clone <your-repo>
cp index.html your-repo/
```

### 2. Open locally
Just open `index.html` in any browser — no build step, no dependencies, no server needed.

```bash
open index.html
```

### 3. Deploy (optional)
Drop `index.html` into any static host:
- **GitHub Pages** — push to a repo, enable Pages, done
- **Netlify** — drag and drop the file
- **Vercel** — `vercel --prod`

## AI Results Fetching

The app calls the [Anthropic Claude API](https://docs.anthropic.com) once per day to fetch confirmed match results. Results are cached in `localStorage` with a date stamp so you won't hit the API repeatedly.

**To use this feature**, you need an Anthropic API key set in the request headers. By default the app uses `anthropic-dangerous-direct-browser-access: true` for direct browser calls — suitable for personal/local use.

For a production deployment, proxy the API call through your own backend to keep your key secure:

```js
// Replace the fetch in fetchResultsFromAI() with your own endpoint:
const res = await fetch('/api/wc-results', { method: 'POST' });
```

## Tech Stack

- Vanilla HTML / CSS / JavaScript — zero dependencies
- Google Fonts (Barlow Condensed + Barlow)
- `localStorage` for prediction persistence
- Anthropic Claude API for daily results

## Customisation

| Thing | Where |
|---|---|
| Favourite team | Change `fav:true` in the `GROUPS` object |
| Add fixtures | Extend the `ALL_FIXTURES` array |
| Change theme colours | Edit CSS variables in `:root` |
| Results cache duration | Change `toDateString()` to a finer/coarser interval |
