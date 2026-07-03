# Magic Prospekt — Flyer CMS

Admin review console for the Magic Prospekt flyer-extraction pipeline. A single
self-contained `index.html` that talks directly to Supabase (Auth + PostgREST +
Storage + Edge Functions) from the browser.

**Live:** https://iordanalexandru1997.github.io/Magic-Prospekt-v2-CMS/

## What it does

- **Prospekte** — discover Lidl flyers (Schwarz API), download/upload PDFs,
  trigger parsing, see a retailer × week availability grid.
- **Review** — the parsed offers of each page next to the rendered PDF page,
  with bounding-box markers, editable fields, and anomaly badges. Approve /
  reject before anything reaches the app.
- **Konfiguration** — parse model, page limit, guardrail thresholds.
- **Läufe** — audit log of every fetch/parse run.

## Access

The page is public, but it only shows a **login screen** to anyone who isn't an
allow-listed admin. All data is gated by Supabase Row-Level Security plus a
`flyer_admins` table — a random visitor can load the page and do nothing.

First time: **Registrieren** with the email that is on the `flyer_admins`
allowlist, choose a password, then **Anmelden**. If your account isn't
allow-listed you'll see "Kein Admin-Zugang".

## Security note

The embedded `SUPABASE_ANON_KEY` is the **public** anon key — the same one
shipped inside the mobile app. It is safe to publish: it grants nothing on its
own; RLS + `flyer_admins` enforce every permission. No service-role key, crawler
secret, or model API key is present in this file.

## Source of truth

This repo is a **deploy mirror**. The canonical CMS lives in the main (private)
Magic Prospekt V2 repo at `app/supabase/cms/index.html`; changes are copied here
to publish. See `docs/FLYER_PIPELINE_GUIDE.md` there for the full pipeline.
