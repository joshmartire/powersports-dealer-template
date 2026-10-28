# Powersports Dealer Template

Demo website for a powersports and compact tractor dealership (ATVs, side-by-sides, tractors, trailers, implements, attachments), with a dealer portal for managing inventory. Built by Rank Boss.

Demo: https://powersportsdemo.getrankboss.com (noindexed)

## What's in it

**Website**
- Home: transparent two-tier header over a full-width hero with a 3D ATV drive-in (plays once per visit, falls back to an illustration), shop-by-type picker, promotions, financing strip, featured inventory slider, brands, about block, hours.
- Inventory with filters (category, condition, make, year, price, sale, recently sold) and sorting.
- Unit pages: gallery, price box with sale price, specs, payment estimator (HST toggle), lead form (price / test ride / trade).
- Financing, Service & Parts, Contact and Trade-in pages. Every form becomes a lead in the portal.

**Dealer portal** (`#admin`, footer link "Dealer login")
- Inventory table: inline price edits, one-click Mark sold / Relist, status, featured star.
- Bulk actions: status, feature, price up/down by % or $ as sale or regular price, clear sale, delete.
- Add / edit unit with photo upload (drag and drop, reorder, set cover; resized in the browser), specs, live card preview.
- Leads inbox, CSV import/export, site settings (name, phone, hours, promo banner, financing rate, how long sold units stay visible).

## Demo mode vs. live

In this demo, all data (inventory, leads, settings, photos) is saved in the visitor's browser (`localStorage`), so each visitor sees the sample data and their own edits only. Every read and write goes through the `DB` object near the top of the script in `index.html`. For a client site, those methods are swapped for `fetch()` calls to a Cloudflare Worker backed by **D1** (inventory, leads, settings) and **R2** (photos), with **Cloudflare Access** protecting `/admin`.

## Client setup checklist

- Dealer details: `seed().settings` in `index.html` (name, tagline, phone, email, address, hours, promo, rate).
- Inventory: replace the sample units in `seed()` or import a CSV from the portal.
- Promotions: `PROMOS`; brands row: the list in `homePage()`; towns served: `homePage()`.
- `_headers` only noindexes `*.pages.dev` and the demo subdomain, so a client domain is indexed normally.
- Keep the 3D model credit in the footer (see `CREDITS.md`).

## Deploy

Static site, no build step. Cloudflare Pages project `rankboss-powersports`, framework none, build command empty, output directory `/`. Pushing to `main` redeploys.
