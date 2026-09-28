# Ajmal Perfume — Tax Invoice Generator

A one-page, no-install invoicing tool for Ajmal Perfume Co., Ltd. It runs entirely in the browser (no server, no database, no monthly cost) and is built to be handed to someone who is comfortable with basic tools like Word or Excel.

## What it does

- Editable tax invoice: business details, logo, client details, line items, VAT (7% by default) and totals
- Saves everything typed on that device automatically (browser local storage) — no login needed
- Keeps a "Recent invoices" list on that device of every invoice downloaded or emailed
- **Download PDF** — generates a print-ready tax invoice PDF
- **Email to client** — downloads the PDF and opens the default email app with the client's address, subject and message pre-filled (the PDF must be attached manually — a plain webpage cannot attach files to an email on its own; see "Upgrading email" below if you want true one-click send)

## Files

```
index.html       the whole app (open this in a browser to use it locally, no setup needed)
assets/logo.png  the business logo shown by default (replace this file to change the default logo)
LICENSE          proprietary notice — see "Licensing" below
.gitignore       keeps OS clutter and any future secret files out of the repo
```

## Put it on GitHub Pages (free hosting)

1. On github.com, click **New repository**. Name it something like `ajmal-invoice`, keep it **Public** (required for free Pages), and create it.
2. Click **Add file → Upload files**, drag in `index.html` and the `assets` folder from this download, and commit.
3. Go to the repo's **Settings → Pages**. Under "Build and deployment", set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`, then **Save**.
4. Wait about a minute, then refresh the Pages settings page — it will show your live link, something like:
   `https://<your-github-username>.github.io/ajmal-invoice/`
5. That link is what you hand to the business. Bookmark it on the computer(s) that will use it — because it saves data per browser, use the same browser/device each time to keep the invoice history and saved business details.

Any time you want to change the tool (fix a typo, adjust VAT rate default, etc.), edit `index.html` and re-upload it the same way — GitHub Pages updates automatically within a minute or two of a commit.

## Notes on the data

- Nothing is sent to a server. Business details, client details and invoice history live only in that browser's local storage.
- Clearing browser data/history, using a different browser, or using private/incognito mode will not show past invoices.
- There is no login and no way to view this data from another device — it's a single-device record-keeper, not shared bookkeeping. If the business grows past that, a proper invoicing service (Xero, QuickBooks, etc.) would be the next step up.

## Licensing

The LICENSE file marks this as proprietary — all rights reserved to Ajmal Perfume Co., Ltd, rather than an open-source license like MIT. That's the right choice for an internal business tool: it means no one else may copy, reuse, or redistribute it without permission. Note that a license controls legal reuse rights, not visibility — it doesn't hide the code from anyone who has the repo link (see "Public vs. private" below for that).

## Public vs. private repository — which to use long term

GitHub Pages' free hosting only works with a **public** repository. Making the repo private and still getting free Pages hosting from GitHub itself isn't possible — that combination needs a paid GitHub Pro plan (~US$4/month).

In practice, going public is lower-risk than it sounds: the repo only ever contains the page's code, the logo, and this README — never any actual invoice data, client details, or credentials (those all stay in the browser's local storage, or in your own email once sent, and never touch the repo). So a public repo doesn't expose business records, just the tool itself and Ajmal's public contact details, which are already on the invoices you send out anyway.

Two ways to think about the choice long term:

- **Public GitHub repo + GitHub Pages (free, simplest)** — recommended for now. Anyone with the exact link *could* open the tool, but nothing sensitive lives in it, the URL isn't indexed by search engines unless something links to it, and no one can see any invoice your team has actually made.
- **Private GitHub repo + Cloudflare Pages + Cloudflare Access (still free, more private)** — if you'd rather the page itself require a login, keep the GitHub repo private (free) and deploy it through Cloudflare Pages instead of GitHub Pages (also free, and it can pull straight from a private repo). Add Cloudflare Access in front of it (free for up to 50 users) so visitors have to verify their email with a one-time code before the page loads. This is the actual "keep it hidden, only I can open it" option — say the word and I'll write up the setup steps for this path instead.

Paying for GitHub Pro just to keep the *repo* private while still using GitHub's own Pages hosting isn't worth it — Cloudflare's combination above gets you real access control for free.

## Upgrading email later (optional)

To make **Email to client** send the PDF automatically (no manual attaching), wire up a free [EmailJS](https://www.emailjs.com) account:
1. Sign up free at emailjs.com and connect an email address (Gmail, Outlook, etc.)
2. Create an email template there for the invoice message
3. In `index.html`, replace the `mailto:` line in the `emailBtn` click handler with an EmailJS `send()` call using your Service ID, Template ID and Public Key, and pass the generated PDF as a base64 attachment

This isn't wired in by default since it needs your own EmailJS account and keys — happy to add it in if you'd like to set that account up.
