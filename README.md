# Hermes Petdex

A visual, faceted selector for the 4,824 animated pets in the [petdex.dev](https://petdex.dev) gallery, built for **Hermes Agent**. Pick a pet by what it *is* — franchise, style, creature type — or just shuffle and see what catches your eye.

A portfolio / development artifact, published as a single-page site on GitHub Pages.

---

## Why

The petdex gallery has 4,824 pets, but no easy way to discover them by *identity*. The native search only matches names, and it doesn't index franchise, visual style, or creature type. If you want "a dragon from a 2000s RPG" or "a chibi capybara" you have to already know the pet's name to find it.

This project adds the discovery layer on top of the existing gallery: the full catalog, indexed and filterable by what each pet actually is.

## Features

- **Faceted, multi-axis filtering** across five dimensions:
  - **Category** — character / creature / object
  - **Universe / franchise** — 41: Pokémon, One Piece, Naruto, Dragon Ball, Genshin Impact, and more
  - **Origin** — anime / video game / TV
  - **Visual style** — pixel, chibi, 3D, cartoon, cyber, plush, sticker, anime
  - **Type** — cat, dog, capybara, dragon, slime, robot, and more
- **Search by name or description** — real descriptions are indexed, so you can hunt by behavior or vibes, not just the name.
- **Real artwork for all 4,824 pets** — actual `webp` thumbnails extracted from the gallery's spritesheets (no placeholders).
- **Curated ordering or "surprise me"** — browse "recognizable first" or hit shuffle for a random browse.
- **Load-in-batches grid** — 120 cards at a time with a **load more** button.
- **1-click install** — click any pet to open a detail modal with name, category, tags (universe / style / type), the real description, and a button that copies the install command:

  ```
  hermes pets install <slug>
  ```

## Data

The dataset is the heart of the project. The `petdex.dev` manifest lists the full set of pets; from that we pulled each spritesheet and extracted the individual `webp` thumbnails into `assets/thumbs/`.

Every pet carries a structured record:

- `slug`, `name`
- `category`
- `author`
- `universe(s)` — franchise or series
- `origin` — anime / video game / TV
- `style` — visual style
- `type` — kind of creature
- `description`
- internal curation metadata — a `recognizable / original / noise` tag plus an `identity` score used purely for ordering, never shown in the UI

Labeling was done heuristically from descriptions, with manual curation of the key franchises to make sure the recognizable canon sorts to the top. Totals: **4,824 pets across 41 universes.**

## Structure

```
.
├── index.html                  # the whole UI — single self-contained file
├── data.js                     # the pet dataset, loaded by index.html
├── petdex_4824_final.json      # source dataset (master copy)
├── assets/
│   └── thumbs/                 # 4,824 webp thumbnails
└── README.md
```

The app is a single self-contained `index.html` plus `data.js` — nothing to build, no dependencies to install.

## How to run / deploy

**Run locally**

```bash
cd petdex
python3 -m http.server 8000
```

Then open http://localhost:8000.

**Deploy to GitHub Pages**

1. Push the repo to GitHub.
2. Repo **Settings → Pages**.
3. Set **Source** to `Deploy from a branch`, choose `main` (root folder).
4. GitHub Pages serves `index.html` at `https://<user>.github.io/<repo>/`.

## Stack

- Vanilla **HTML / CSS / JavaScript** — no frameworks, no build step, no dependencies.
- Data stored as a plain JS file for instant client-side filtering.
- Total footprint ~**33 MB** (mostly the 4,824 thumbnails).

## Credits

All pet artwork and metadata come from the public [petdex.dev](https://petdex.dev) gallery. This project is an independent discovery interface built on top of it, not affiliated with petdex.dev or Hermes Agent.
