# Minute Math

A single-page, self-contained game for practicing multiplication facts, inspired by the classic classroom "Minute Math" challenge: **solve as many problems as you can in 60 seconds, then try to beat your own score.**

## Play

Open `minute-math.html` in any modern browser. No build step, no server, no internet — everything (logic, styling, and sound) is inline in the one file.

## How it works

- **One minute on the clock.** A live countdown ring shows time remaining and turns red for the final 10 seconds.
- **Every correct answer is a point.** There's no passing score — it's a competition against your own personal best, which is saved in your browser (`localStorage`) between sessions.
- **Instant feedback.** Answers check as you type, so you never need to press Enter. Correct answers flash green with a chime; misses buzz and reset your streak.
- **Choose exactly which tables to drill.** Two modes: *Up to a table* includes every table from 1× up to the one you pick, or *Pick each* lets you toggle any individual tables (1×–12×) with All/None shortcuts. Every problem is built only from the tables you selected.
- **Play your way.** Type with a keyboard or use the on-screen keypad on touch devices.
- **End-of-round summary.** Your round (problems solved, accuracy, best streak) is shown side by side with your all-time records (All-Time High, Best Accuracy, Longest Streak) for easy comparison. Beat a record in any of the three categories and you get confetti, a fanfare, a gold "NEW" badge on each record you broke, and a temporary toast spelling out what you achieved. (An accuracy record needs at least five answered problems, so a lucky two-problem round can't lock in 100%.)

## Design notes

- Web Audio API generates all sound effects at runtime, so there are no external audio files to load.
- Responsive layout works on phones and desktops; a 🔊 toggle mutes sound. The card centers when it fits and scrolls when the window is short, so nothing gets clipped.
- Verified in headless Chromium: start → countdown → play loop → scoring → streak reset → end screen, all passing with no console errors.

## Publishing & discoverability

Built for hosting on **HomeLearners.org** (a subtle byline links back to the site from the title screen). The `<head>` includes:

- SEO metadata — a keyword-rich `<title>` and description, `keywords`, `author`, and `robots: index, follow`.
- Social share tags — Open Graph and Twitter Card, so links unfurl nicely.
- A self-contained SVG favicon (data URI — no separate icon file).
- **Structured data (JSON-LD)** describing the page as a free `LearningResource` / `WebApplication` that *teaches* multiplication facts, aimed at students, parents, teachers, and homeschoolers, aligned to Common Core `3.OA.C.7`. This is what helps Google rich results — and AI assistants — understand and recommend it as a free multiplication-practice resource.

**Before publishing:** the canonical/share URL defaults to `https://homelearners.org/minute-math.html`. If you host it at a different path, update the URL in three places in `<head>` (the `canonical` link, the `og:url` meta, and the `url` field in the JSON-LD) — there's a comment at the top of `<head>` marking them. For best AI/search crawler access, also allow crawlers (including AI bots such as `GPTBot`, `ClaudeBot`, `PerplexityBot`, and `Google-Extended`) in the site's `robots.txt` and add the page to your sitemap.
