# Note Pairs handoff

The delivered game matches treble notes to names, with three levels, local best scores, sound controls, a system check and the documented extension surface. No feature-menu item is included.

## Deviations and added copy

The self-check panel adds the labels `สำรับ`, `ระดับ`, `โน้ต`, `บันทึกได้`, `บันทึกไม่ได้` and `ส่วนเสริม` to report table counts, storage status and extension errors, which the shared rules require but the copy table does not supply. The HUD also has the accessible label `ผลการเล่น`. The system-check test names are additional Thai text as required by the shared rules. CSS values are exposed as custom properties; SVG paths retain their drawing coordinates.

## Checks run

- `cd tests && node --test note-pairs*.test.cjs`: 15 tests passed, including core functions, fixed-seed shuffle, silent play, extension reveal and throwing-handler probes, custom deck, storage fallback and oscillator calls.
- `node tools/note-browser-check.mjs`: Chrome loaded the local file and self-check, finished a game with audio unavailable at 320 px, with no console output, network requests or horizontal overflow in that run.
- `node tools/note-browser-extra.mjs`: Chrome checked keyboard activation and arrow focus, reduced motion, four-column width, wrong-pair timeout, win, best-score persistence, all notehead positions and ledger counts, and card-back tokens. C4, B4, F5 and A5 were visually inspected in the generated fixture image.
- `node tools/shot.mjs note-pairs`: generated 320 × 640, 390 × 844 and 1280 × 800 screenshots in light and dark. The six initial-screen screenshots were viewed individually; no clipping, overlap, horizontal scrolling or visibly unreadable text was found.

- `node tools/contrast-check.mjs`: visible text passed contrast checks in sampled playing or selected states in both light and dark schemes. This does not cover every possible student modification.

- `node tools/audio-browser-check.mjs`: both audio-enabled games completed in headless Chrome with zero console messages and network requests. This does not establish audible speaker quality.

## Not verified

Real sound on speakers and subjective sound quality, touch feel on a real phone, the school lab's Windows PCs, and deployment to GitHub Pages were not tested. A separate private Sites preview was deployed for the instructor; the Sites service reported success. The automated contrast checks are not exhaustive for all user-added content. Students adding a custom deck should check its labels and distinguishability themselves; duplicate keys and unknown staff notes are reported by the system check and skipped.

## v2 upgrade

Added four decks, Classic/Race/Ear play, a learning strip, score and streaks,
results with confusions, medals, first-visit instructions, theme and motion settings,
and migration of best turns from v1. Ear play requires an available AudioContext.
The v1 helper, event and storage names remain available.

- Baseline: the 15 Note Pairs tests passed before edits and again after the
  readability changes. The unchanged all-app package check also passed.
- `cd tests && node --test --test-reporter=spec note-pairs*.test.cjs packaging.test.cjs`:
  24 passed. Old UI fixtures enter the game through the home screen, disable the
  peek where unnecessary, expect the expanded self-check, and use the new
  two-step exit to change levels. The oscillator fixture includes the new miss
  tone. The tests cover all decks, race redeal and time-out, ear replay and its
  unavailable-audio notice, v1 migration, a zone E two-player probe, and a throwing handler.
- `node tools/note-v2-browser.mjs`: keyboard completion in audio-enabled Chrome
  for three modes and in silent Chrome for Classic and Race, with the Ear
  notice verified in silent Chrome. No console output or network requests from
  the app after file navigation. Captured 36 screen images and inspected
  the six screen types at three viewport sizes in both themes by contact sheet.
- `?selfcheck=1`: 31 tests passed. File size below 300 KB, with no source line
  longer than 120 characters.
- New copy outside the supplied table includes `ไปหน้าแรก`, `เปิดเสียงเพื่อเล่นโหมดฟังเสียง`,
  `สัญลักษณ์ดนตรี` (the card's accessible label), the best-score readout, and the
  mode, medal and screen counts in the self-check.
- Physical phone input, audible playback, and Windows lab devices were not tested.
