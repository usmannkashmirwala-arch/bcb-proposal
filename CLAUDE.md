# BCB Proposal Site — Claude Code Instructions

> Project-specific instructions for any AI agent working on this proposal page.
> This project is fully independent from the main bettercallbot.com website repo — do not assume shared tooling, build steps, or file locations.

---

## What This Project Is

A **single static HTML page** that serves the "BCB Proposal" client proposal at **https://proposal.bettercallbot.com**.

It was originally a Canva design embedded via iframe, but the iframe was slow and janky to scroll/pinch-zoom on mobile. It has since been rebuilt as native HTML/CSS with the same layout, copy, colors, and fonts — so it's fast and scrolls natively.

This is a **brochure/sales page for one specific proposal**, not a marketing site — it's marked `noindex, nofollow` on purpose and isn't meant to be discovered via search.

---

## Tech Stack

| Layer | Technology | Notes |
|---|---|---|
| **Markup** | HTML5 | Single file: `index.html` |
| **Styling** | CSS3 (inline `<style>` block) | All styles live in `index.html` — no external `.css` |
| **Fonts** | Google Fonts CDN | `Anton` (display/headings) + `DM Sans` (body + italic red labels) — same pairing as the main bettercallbot.com site |
| **Images** | Static files in `images/` | See below |
| **Build tools** | None | Zero npm, zero bundlers, zero dependencies. Just edit and push. |
| **Deployment** | GitHub Pages | Auto-deploys on every push to `main` |

**The entire page is one file: `index.html`.** All CSS is in the `<style>` block in `<head>`. There is no JS.

---

## File Structure

```
index.html          — the whole page (markup + styles)
CNAME                — contains "proposal.bettercallbot.com", required by GitHub Pages, do not delete
images/
  ctrl-key-icon.png     — hero section, orange "Ctrl" key graphic
  help-icons.png        — "Omni Channel AI Customer Support" section icon (bag + device)
  dashboard.jpg          — "Personal Omni Channel Dashboard" screenshot
  shopping-assist.jpg    — "AI Shopping Assistant" phone mockup
  pricing-photo.jpg      — pricing section, Hush Puppies site + chat widget screenshot
```

---

## Brand Tokens

Pulled directly from the source Canva design — keep these consistent with any edits:

| Token | Value |
|---|---|
| Background | `#f5f4f0` |
| Text (body) | `#1a1a1a` / `#2b2b2b` |
| Accent (red) | `#ff3131` |
| Display font | `Anton` (uppercase, headings, stylized hero text, bold section labels) |
| Body font | `DM Sans` (paragraphs at regular weight; red feature-title lines use `DM Sans` bold italic) |

---

## How to Edit & Publish

No build step. Edit `index.html` directly (or swap files in `images/`), then:

```bash
git add -A
git commit -m "describe the change"
git push
```

GitHub Pages rebuilds automatically — changes are usually live at proposal.bettercallbot.com within 1–2 minutes. No need to touch DNS, GitHub Pages settings, or the `CNAME` file for normal content edits.

---

## Hosting & Domain (reference — normally shouldn't need to change)

- **GitHub repo:** `github.com/usmannkashmirwala-arch/bcb-proposal` (public), deployed via GitHub Pages from `main` branch, root path
- **Custom domain:** `proposal.bettercallbot.com`, bound via the `CNAME` file and GitHub Pages custom-domain settings
- **DNS:** `bettercallbot.com` is on GoDaddy nameservers. A CNAME record exists: host `proposal` → `usmannkashmirwala-arch.github.io`
- **HTTPS:** enforced, cert auto-issued/renewed by GitHub. If a future DNS or domain change ever leaves the cert stuck (check via `gh api repos/usmannkashmirwala-arch/bcb-proposal/pages` — look at the `https_certificate` field), the fix is to clear and re-set the custom domain to force re-provisioning:
  ```bash
  gh api -X PUT repos/usmannkashmirwala-arch/bcb-proposal/pages -F "cname="
  # wait ~15s
  gh api -X PUT repos/usmannkashmirwala-arch/bcb-proposal/pages -f "cname=proposal.bettercallbot.com"
  ```

---

## Provenance

The layout, copy, and images were extracted from the original Canva design ("BCB Proposal", design ID `DAHTA4ZXfQE`) via the Canva MCP integration — reading its structured element data (text, positions, colors, fonts) and exporting/cropping its images. If the source Canva design changes significantly and needs re-syncing, that's the process to repeat rather than trying to re-embed the iframe.

Two obvious typos present in the original Canva copy were silently corrected during the rebuild: "nstead" → "instead", "stockright" → "in stock right". No other copy changes were made.
