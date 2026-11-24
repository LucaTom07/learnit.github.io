# Parla – Learn Languages (Italian, Spanish, French)

Mobile-first PWA. Three files run the app (`index.html`, `sw.js`, `manifest.webmanifest`) plus the icons.

## Deploy on GitHub Pages
1. Copy everything in this folder (except `logos/` and `README.md`, which are optional) to the root of your repo, replacing the old files.
2. Commit and push. Open the Pages URL once online so the service worker caches the app.
3. On a phone: Share / menu -> Add to Home Screen.

## Files
- `index.html`: the whole app (UI, curriculum, lesson engine, voices, tutor, quizzes, streaks).
- `sw.js`: network-first service worker, cache `parla-v4`; old caches are deleted on activate. When you ship a new version, bump `CACHE`.
- `manifest.webmanifest`: name, colours, icons (192, 512, 512 maskable).
- `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png`: app icons referenced by the manifest and `<head>`.
- `logos/`: icon at 1024 and 180 px, `icon.svg`, and one logo per language (`logo-it`, `logo-es`, `logo-fr`, PNG + SVG).

## Existing users
Old progress is stored under the localStorage key `it`. On first load it is treated as Italian progress and is saved into `S.langs.it`. Streaks, XP, badges, name and goal stay shared across languages.

## Curriculum size
Italian: 36 units. Spanish and French: 18 units each (3 chapters, A1 to A2), every unit with 8 words, 4 sentences and a grammar tip. Chapter quizzes appear after every 6 units. To add units, append objects to the `ES` / `FR` arrays at the top of the script (format `n`, `g`, `w`, `s`); the path, quizzes, games and tutor pick them up automatically. Have a native speaker review new Spanish and French content before publishing.

## Games (Play tab)
Lightning round, Memory match, Word scramble, Hangman and Swipe flashcards. All use only words from completed units in the active language, award XP, count towards the daily streak, and keep a best score per language.

## AI tutor
Inside Claude artifacts the tutor calls Claude. On GitHub Pages there is no `window.claude`, so the app switches to offline tutor mode immediately (greetings, introductions, common phrases, accent corrections, then a practice sentence from your completed units).

## Voices
Each language has 3 voice slots. They map to the best installed `it` / `es` / `fr` voices on the phone and always sound different (pitch and rate change even when only one voice is installed). Profile -> "Test voices and mic" checks this phone.
