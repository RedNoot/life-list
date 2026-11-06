# Life list

A private, ranked list of everything you've done. Write a line, then place it
by picking the better of two until it lands at its rank. The list is yours
alone: it saves in your browser, on your device, and is never sent anywhere.
If the app crashes it sends a short technical report (see "Crash reports").

It's one HTML file with no build step and no dependencies. It installs to a
phone's home screen and works offline once it has been opened.

## What it does

- **Rank by comparison.** New entries are placed with a binary search: roughly
  seven "which is better?" picks for a list of 100. You can also drag a line,
  or tap its number and type a new rank.
- **Several lists.** Tap the list name at the top to switch lists, start a
  new one, rename it or delete it. Each list has its own entries and ranking;
  the theme and settings are shared.
- **Tags.** End a line with ` - food, travel`, use `#food`, or tap **# Tag**
  above the box to pick tags or make new ones. The line under the box shows
  which tags the next entry will get. Filter by tag, year or "on this day".
- **Patterns.** Tag mix, momentum year on year, a daily heatmap, pairs of tags
  that go together, and a year-by-year breakdown.
- **Tiers.** Cuts your ranking into S–F on a normal curve, and can save it as
  an image.
- **25 themes.** The default is *Sunbaked* (light) or *Sunbaked night* (dark),
  from the RedNut design system. First launch follows your system setting.
- **Get it out.** Plain text, Markdown, CSV, or a full JSON backup. Restore or
  merge a backup, or paste in many lines at once.
- Undo/redo (Ctrl/⌘+Z), typo-tolerant search, and a warning before adding a
  near-duplicate.

## Your data

Everything is kept in `localStorage`, on the device you add things on:

| Key | Holds |
| --- | --- |
| `lifelist:lists` | The names of your lists and which one is open |
| `lifelist:prefs` | Theme and settings, shared by every list |
| `lifelist:v1` | Your first list (where older versions kept the only list) |
| `lifelist:list:<id>` | Each list after the first |

So:

- Each browser and device keeps its own lists. Move a list with **Download
  backup (JSON)** → **Restore from backup** (a backup holds the list that's
  open).
- On iPhone, a home screen app gets storage separate from Safari. Restore a
  backup there if you started in Safari.
- Clearing site data erases the list. The app asks the browser for persistent
  storage, but make a backup now and then anyway.

If storage is blocked (some private modes), it runs from memory and warns you
to back up before closing.

## Crash reports

Crashes go to AppReporter (`app-reporter.js`, a copy of the browser kit from
`D:\AppReporter`), which files them in Discord. A report holds the error, the
stack, the page, the browser and which buttons were pressed just before. It
never holds your list: quoted text is removed from error messages before
sending, and the kit never records text on screen. There's no feedback button
yet.

## Run it

Open `index.html` directly, or serve the folder to get offline support and
installing (the service worker only runs over http/https):

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles, script |
| `manifest.webmanifest` | Name, colours and icons for installing |
| `sw.js` | Offline cache, network first so updates show straight away |
| `app-reporter.js` | Crash reporting (AppReporter browser kit) |
| `icons/` | App icons (SVG, plus PNGs for Android and iOS) |

## In the portfolio

This app is one of the zones in the
[isometric portfolio](https://github.com/RedNoot/portfolio), which serves a
copy of these files from `/apps/life-list/`. This repo is the source of truth:
make changes here, then copy the files across.

## Later

- Optional sync through a database and an account, so a list can follow you
  between devices. The storage layer (`store` in `index.html`) is a small
  get/set/delete interface, so a remote backend can go in behind it.
