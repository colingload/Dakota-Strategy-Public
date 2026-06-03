# dakotastrategy.com

Source of truth for the [dakotastrategy.com](https://dakotastrategy.com) website. The site itself is hosted on [Carrd](https://carrd.co/) and served at the custom domain. This repo is where the HTML is written, versioned, and pushed to GitHub before being copy-pasted into Carrd.

The whole site is a single self-contained HTML file (`index.html`) — no build step, no framework, no `npm install`. That constraint exists because Carrd's Embed element accepts one block of code, so everything (HTML + inline CSS + any inline JS) lives in one file.

---

## How to update the site

1. **Edit** `index.html` in this folder. Open it in a browser to preview your changes.
2. **Commit** the change to git and push to GitHub:
   ```powershell
   git add index.html
   git commit -m "describe the change"
   git push
   ```
3. **Open Carrd** → open the dakotastrategy.com project → click the Embed element on the page → switch it to **Code** mode → select-all and replace with the full contents of `index.html`.
4. **Publish** in Carrd. Within a minute or two the live site updates.

That's it. The repo is always ahead of (or equal to) what's on Carrd. If Carrd and the repo ever drift, the repo wins — paste the repo version back in.

---

## Local preview

Just open `index.html` in your browser by double-clicking it.

If you want a real localhost server (e.g. so external fonts and CDN assets behave exactly like production):

```powershell
# from this folder
python -m http.server 8000
# then visit http://localhost:8000
```

No other commands. No build. No watch mode.

---

## File layout

```
dakotastrategy.com/
├── README.md      ← this file
├── .gitignore
└── index.html     ← the entire site
```

**Why one file:** Carrd's Embed element takes one chunk of code. Relative paths to `assets/foo.png` won't resolve once pasted into Carrd. So images need to be either:
- inlined as data URIs (small icons, SVGs), or
- hosted somewhere with an absolute URL (e.g. an image CDN, or a `raw.githubusercontent.com` link to this repo).

Same for CSS and JS — keep it inline in `<style>` and `<script>` tags inside `index.html`.

---

## GitHub

This folder is the local working copy of the public repo
**[colingload/Dakota-Strategy-Public](https://github.com/colingload/Dakota-Strategy-Public)** —
the source of truth for the site. Every update is just:

```powershell
git add index.html
git commit -m "describe the change"
git push
```

The repo is always ahead of (or equal to) what's pasted into Carrd.

---

## Alternative deploy: GitHub Pages (optional)

If the paste-into-Carrd loop ever feels tedious, the exact same `index.html` will work on **GitHub Pages** for free with no code changes:

1. In the GitHub repo settings → **Pages** → set source to `main` branch, root folder.
2. GitHub gives you `https://<username>.github.io/dakotastrategy.com/`.
3. To use the dakotastrategy.com custom domain, point its DNS at GitHub Pages instead of Carrd, and add a `CNAME` file containing `dakotastrategy.com`.

This trades Carrd's visual editor for a true git-push-deploys workflow. Not necessary now — just an option.

---

## Version history & related folders

- **Old v2.0 site (content reference):** lives in this repo's git history — the prior `index.html`
  committed to `Dakota-Strategy-Public` before this version. `git log -- index.html` to find it.
  Reference it for voice/content; the current site is a structural redo.
- **Internal/private strategy docs:** [../dakota-strategy/](../dakota-strategy/) — dashboards, runbook, architecture notes. Not for public consumption.
