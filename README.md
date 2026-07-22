# Minute Math

A single-page, self-contained game for practicing multiplication facts, inspired by the classic classroom "Minute Math" challenge: **solve as many problems as you can in 60 seconds, then try to beat your own score.**

## Play

Open `minute-math.html` in any modern browser. No build step, no server, no internet — everything (logic, styling, and sound) is inline in the one file.

## How it works

- **One minute on the clock.** A live countdown ring shows time remaining and turns red for the final 10 seconds.
- **Every correct answer is a point.** There's no passing score — it's a competition against your own personal best, which is saved in your browser (`localStorage`) between sessions.
- **Instant feedback.** Answers check as you type, so you never need to press Enter. Correct answers flash green with a chime; misses buzz and reset your streak.
- **Play your way.** Choose to practice tables up to 5×, 9×, or 12×. Type with a keyboard or use the on-screen keypad on touch devices.
- **End-of-round summary.** See your score, accuracy, and best streak — with a confetti celebration and fanfare when you set a new record.

## Design notes

- Web Audio API generates all sound effects at runtime, so there are no external audio files to load.
- Responsive layout works on phones and desktops; a 🔊 toggle mutes sound.
- Verified in headless Chromium: start → countdown → play loop → scoring → streak reset → end screen, all passing with no console errors.
