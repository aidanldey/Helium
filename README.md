# HomeLearners.org games

Self-contained, single-file browser games for **HomeLearners.org**. Each game is one
HTML file with all of its logic, styling, and sound inline — open it in any modern
browser, no build step, no server, no internet.

| Game | File | What it is |
| --- | --- | --- |
| Minute Math | `minute-math.html` | 60-second multiplication facts challenge |
| Slide Puzzle | `slide-puzzle.html` | 5×5 sliding tile puzzle (24 tiles + one space) |

---

## Minute Math

A single-page, self-contained game for practicing multiplication facts, inspired by the classic classroom "Minute Math" challenge: **solve as many problems as you can in 60 seconds, then try to beat your own score.**

### Play

Open `minute-math.html` in any modern browser. No build step, no server, no internet — everything (logic, styling, and sound) is inline in the one file.

### How it works

- **One minute on the clock.** A live countdown ring shows time remaining and turns red for the final 10 seconds.
- **Every correct answer is a point.** There's no passing score — it's a competition against your own personal best, which is saved in your browser (`localStorage`) between sessions.
- **Instant feedback.** Answers check as you type, so you never need to press Enter. Correct answers flash green with a chime; misses buzz and reset your streak.
- **Choose exactly which tables to drill.** Two modes: *Up to a table* includes every table from 1× up to the one you pick, or *Pick each* lets you toggle any individual tables (1×–12×) with All/None shortcuts. Every problem is built only from the tables you selected.
- **Play your way.** Type with a keyboard or use the on-screen keypad on touch devices.
- **End-of-round summary.** Your round (problems solved, accuracy, best streak) is shown side by side with your all-time records (All-Time High, Best Accuracy, Longest Streak) for easy comparison. Beat a record in any of the three categories and you get confetti, a fanfare, a gold "NEW" badge on each record you broke, and a temporary toast spelling out what you achieved. (An accuracy record needs at least five answered problems, so a lucky two-problem round can't lock in 100%.)

### Design notes

- Web Audio API generates all sound effects at runtime, so there are no external audio files to load.
- Responsive layout works on phones and desktops; a 🔊 toggle mutes sound. The card centers when it fits and scrolls when the window is short, so nothing gets clipped.
- Verified in headless Chromium: start → countdown → play loop → scoring → streak reset → end screen, all passing with no console errors.

---

## Slide Puzzle

The classic sliding tile puzzle: **24 numbered tiles share a 5×5 grid with one empty
space. Slide them around until they read 1 to 24 in order.**

### Play

Open `slide-puzzle.html` in any modern browser.

### How it works

- **Tap to slide.** Any tile sitting directly next to the empty space slides into it when you tap or click it. Tiles that can move right now are outlined, so the legal moves are always obvious. Tapping a tile that can't move nudges the board and buzzes instead of doing nothing silently.
- **Keyboard too.** The arrow keys (or WASD) slide the neighbouring tile into the space — `↑` pulls the tile *below* the space upward, so it feels like dragging the space around.
- **Solved means 1 → 24 in reading order**, with the empty space back in the bottom-right corner. Tiles already sitting in their finished position get a small green underline, which makes progress visible while you work down the board.
- **Always solvable.** The shuffle walks the empty space randomly around a solved board rather than dealing the tiles at random — exactly half of all random arrangements of a 5×5 board are impossible to solve, and this rules those out by construction.
- **Moves, time, and personal bests.** The clock starts on your first move, not when the page loads. Fewest moves and fastest time are saved separately in your browser (`localStorage`), and beating either one gets you confetti, a fanfare, and a gold badge naming the record you broke.
- **New Puzzle** deals a fresh scramble; **Restart** rewinds the *current* puzzle back to how it was dealt, so you can retry the same board.

### Light and dark mode

- The 🌙/☀️ button in the corner switches themes, and your choice is remembered between visits.
- With no saved choice, the page follows the operating system's `prefers-color-scheme` setting and keeps following it live if you change the OS theme mid-session. Picking a theme by hand takes over from then on.
- Both themes are driven by one set of CSS custom properties on `<html data-theme>`, so there is a single place to adjust colors. The mobile browser chrome color (`theme-color`) switches with the theme as well.

### Design notes

- Tiles are absolutely positioned and moved with `transform`, so each slide is one GPU-composited transition instead of a grid re-layout — smooth even on older phones. `prefers-reduced-motion` turns the animations off.
- Web Audio API generates all sound effects at runtime, so there are no external audio files to load. A 🔊 toggle mutes them, and the setting is saved.
- Every `localStorage` access is wrapped in a `try/catch`, so private-mode Safari degrades to "no saved data" instead of breaking the game.
- Tiles are real `<button>` elements with live `aria-label`s describing each tile's number, row, column, and whether it can move, so the board is usable with a screen reader.
- Verified in headless Chromium: layout, shuffle, legal/illegal taps, arrow keys, theme toggle and persistence across reload, Restart, and a full puzzle solved through real clicks to the win screen and saved record — all passing with no console errors.

---

## Publishing & discoverability

Both games are built for hosting on **HomeLearners.org** (a subtle byline links back to
the site from each game). Every `<head>` includes:

- SEO metadata — a keyword-rich `<title>` and description, `keywords`, `author`, and `robots: index, follow`.
- Social share tags — Open Graph and Twitter Card, so links unfurl nicely.
- A self-contained SVG favicon (data URI — no separate icon file).
- **Structured data (JSON-LD)** describing the page as a free `LearningResource` / `WebApplication`, including what it *teaches* and who it's for. Minute Math is aligned to Common Core `3.OA.C.7`; Slide Puzzle is additionally typed as a `Game`. This is what helps Google rich results — and AI assistants — understand and recommend these as free learning resources.

**Before publishing:** each game's canonical/share URL defaults to
`https://homelearners.org/<file-name>`. If you host a game at a different path, update
the URL in three places in its `<head>` (the `canonical` link, the `og:url` meta, and
the `url` field in the JSON-LD) — there's a comment at the top of each `<head>` marking
them — and update `sitemap.xml` to match.

### `robots.txt` and `sitemap.xml`

Starter files are included in this repo for the site root (not just one page):

- **`robots.txt`** — allows all crawlers, and explicitly welcomes AI assistants and AI-search crawlers by name (`GPTBot`, `ChatGPT-User`, `ClaudeBot`, `Claude-User`, `PerplexityBot`, `Google-Extended`, etc.) so it's unambiguous they're invited to read, index, and recommend the content. It points to the sitemap.
- **`sitemap.xml`** — lists `minute-math.html` and `slide-puzzle.html`. As you publish more pages/games on HomeLearners.org, add one `<url>` block per page and bump `<lastmod>` when content changes meaningfully.

Deploy both at the **site root** — `https://homelearners.org/robots.txt` and `https://homelearners.org/sitemap.xml` — not nested in a subfolder, or crawlers won't find them at their expected well-known locations. If HomeLearners.org already has a `robots.txt`/`sitemap.xml`, merge these entries into the existing files rather than overwriting them.
