# CSC/ECE 506 — Parallel Computer Architecture

Interactive HTML lecture decks for **CSC/ECE 506 (Parallel Computer Architecture)**, North Carolina State University.

Decks are built with [reveal.js](https://revealjs.com/) and styled to match the official
**NC State** PowerPoint template (red header bar + *NC STATE UNIVERSITY* wordmark, white body).
Content is based on Yan Solihin, *Fundamentals of Parallel Multicore Architecture*.

## Contents

```
slides/
├── index.html        # landing page — links to every chapter deck
├── assets/
│   ├── theme.css     # shared NC State reveal.js theme
│   └── ncstate-bar.jpg
└── chap1.html        # Chapter 1 — Perspectives  (45 slides)
```

More chapters (2–11) are converted incrementally and added under `slides/`.

## Viewing the decks

The decks reference `assets/theme.css` by relative path, so they must be **served over HTTP**
(not opened as `file://`).

**Locally:**

```bash
cd slides
python3 -m http.server 8506
# then open http://localhost:8506/
```

**Online (GitHub Pages):** enable Pages for this repo (Settings → Pages → deploy from `main`,
folder `/` or `/docs`). The decks will then be available at
`https://fruitfly1026.github.io/CSC506/slides/`.

## Presenting

Open any deck and use:

| Key | Action |
|-----|--------|
| `←` `→` | previous / next slide (also reveals answers on review slides) |
| `S` | speaker notes |
| `F` | fullscreen |
| `ESC` | slide overview |

To export a deck to PDF, open it with `?print-pdf` appended to the URL and print to PDF from the browser.
