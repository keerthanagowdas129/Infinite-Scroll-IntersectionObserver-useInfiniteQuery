# Threadbase — Infinite Scroll Starter

Cursor pagination is **already wired**: the server returns `{ threads, nextCursor }`,
and the React feed uses `useInfiniteQuery` with a **"Load More" button**.

Your job: replace the button with **automatic infinite scroll** using
`IntersectionObserver` wrapped in a reusable `useIntersection` hook.

## What you'll change

| File | What to do |
|---|---|
| `client/src/hooks/useIntersection.js` | Implement the custom hook (currently a stub). |
| `client/src/components/ThreadList.jsx` | Add a `sentinelRef` + sentinel `<div>`, a guarded `onIntersect`, wire the hook, remove the button, keep a "Loading more…" indicator. |

**Do not change** `server/routes/threads.js` or `client/src/services/threads.service.js` — the cursor pagination is done.

## Setup

```bash
npm run setup                       # installs root + server + client deps

cp server/.env.example server/.env  # DATABASE_URL="file:./dev.db"
npm --prefix server run db:setup    # create the SQLite DB + tables (migrate)
npm --prefix server run db:seed     # seed 35 threads → 4 pages of 10

cp client/.env.development.example client/.env.development   # VITE_API_URL

npm run dev                         # server :3001 + client :5173
```

Open http://localhost:5173.

- **Before your changes:** 10 threads load, then a **Load More** button.
- **After your changes:** no button — new threads load automatically as you scroll,
  with a brief "Loading more…" cue, and nothing fires once all 35 are loaded.

## Verify

1. Inspect the DOM: an empty `<div>` sits after the last thread; no button.
2. Open the Network tab and scroll: requests fire automatically as you approach the bottom.
3. "Loading more…" shows while each batch is in flight.
4. After the 4th page (`nextCursor: null`), scrolling fires **no** more requests.

## Submit

Push a feature branch and open a PR into `main` in your fork. Include a short note (or
screen-recording description) showing threads loading automatically as you scroll, with
no Load More button.
