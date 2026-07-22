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
- Responsive layout works on phones and desktops; a 🔊 toggle mutes sound.
- Verified in headless Chromium: start → countdown → play loop → scoring → streak reset → end screen, all passing with no console errors.
