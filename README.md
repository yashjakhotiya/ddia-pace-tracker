# DDIA Pace Tracker

A single-file web app that keeps you on pace while reading *Designing Data-Intensive Applications* (or any book). Tells you which page you should be on right now and how many seconds you have left to finish it. Ticks a clock when you're on-pace-or-behind in the last 20 seconds of a page, so you stop dawdling.

## Use

Open `index.html` in a browser. Enter:

- **Pages already read this session** — `0` if starting fresh, non-zero to resume.
- **Total pages** — defaults to `81` (DDIA 2nd ed preface + Ch 1–3).
- **Total minutes** — defaults to `240` (4h).

Hit **Start**. The app shows:

- The page you *should* be on (huge number, color-coded: green on/ahead, amber 1 behind, red 2+ behind).
- A countdown — seconds left to finish the current page.
- Your actual page, session time remaining, and a progress bar with a yellow target tick.

### Controls

| Action | Button | Key |
|---|---|---|
| Mark current page done | ✓ Page done | `Space` |
| Pause / resume | ⏸ / ▶ | `P` |
| Undo last page | ↶ Undo last page | `U` |
| Add 5 min to session | +5 min slack | — |
| Reset everything | Reset session | — |

State persists in `localStorage` — close the tab, come back, pick up where you were (clock keeps counting if not paused).

### Tick sound

`assets/clock-ticking-sound.mp3` loops automatically when:
- You're on the target page **or behind**, AND
- The current page has **less than 20 seconds** left.

Toggle off via the checkbox at the bottom. Sound preference is also persisted.

## Customizing chapter boundaries

Edit the `CHAPTERS` constant near the top of the `<script>` block. Session-internal page numbers (1..N), not the book's printed page numbers:

```js
const CHAPTERS = [
  { name: 'Preface',   start: 1,  end: 6  },
  { name: 'Chapter 1', start: 7,  end: 31 },
  { name: 'Chapter 2', start: 32, end: 38 },
  { name: 'Chapter 3', start: 39, end: 81 }
];
```

## Files

```
ddia-pace-tracker/
├── index.html                 # the app (HTML + CSS + JS, no build step)
├── assets/
│   └── clock-ticking-sound.mp3
└── README.md
```

No dependencies, no build, no server. Just open the HTML.
