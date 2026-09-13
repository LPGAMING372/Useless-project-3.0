# Graveyard of Ideas

> Where ideas go to die.

A darkly humorous virtual cemetery for abandoned, useless, ridiculous, and
unfinished ideas. Bury one, get a dramatic (algorithmic, no-API) judgment, and
receive a full death certificate. Runs entirely in the browser — no backend,
no accounts, no API keys.

## Tech stack

- React 18 + Vite
- Tailwind CSS
- lucide-react icons
- localStorage for persistence (all data stays on your machine)

## Getting started

```bash
npm install
npm run dev
```

Then open the URL Vite prints (usually `http://localhost:5173`).

To build for production:

```bash
npm run build
npm run preview
```

## How it works

- **Bury an idea** — opens a modal asking for a title and short description.
  On submit, a local algorithm (`src/utils/judgment.js`) analyzes the text
  (length, buzzwords, grandiosity, a seeded random component) to generate a
  uselessness score, resurrection chance, cause of death, epitaph, and last
  words. A short "analyzing" animation plays before the death certificate is
  revealed.
- **Cemetery** — every buried idea becomes a tombstone. Tombstones get
  hash-derived visual variance (tilt, stone tint, moss, arch shape) so no two
  look identical. Search and filter (recently buried, most useless, most
  ambitious, most viewed, highest resurrection chance, random) are available.
- **Resurrect an idea** — picks a random dead idea, asks for confirmation,
  plays a short animation, then moves it into the "Unfortunately Alive"
  section. It does not become useful. That's the joke.
- **Statistics** — live counts and aggregates computed from whatever is in
  localStorage.
- **Sound** — optional, off by default, toggled from the navbar. All effects
  are generated with the Web Audio API (no audio files to load).
- **Easter eggs** — see `src/utils/judgment.js` for the full list (e.g.
  submitting "I don't know", writing something extremely long, and two very
  rare causes of death).

## Project structure

```
src/
  components/     UI components (Navbar, Hero, Cemetery, Tombstone, BurialModal,
                  DeathCertificate, Statistics, SearchBar, Filters,
                  ResurrectionModal, About, Footer, Modal, Fog, ...)
  hooks/
    useGraves.js  Central state: graves list, burial/resurrection actions, stats
  utils/
    judgment.js   The "no AI, just a clever local algorithm" judgment engine
    storage.js    localStorage read/write helpers
    sound.js      WebAudio-generated sound effects
    tombstoneVariant.js   Per-grave visual hashing
    hash.js       Small string hash + seeded PRNG
    format.js     Date/number formatting
  data/
    exampleGraves.js  ~11 fictional starter graves
  App.jsx
  main.jsx
  index.css
```

All submitted ideas are stored under a few `graveyard-of-ideas:*` keys in
`localStorage`. Clearing your browser storage resets the cemetery back to the
example graves.
