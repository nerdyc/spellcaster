# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Server

Serve the site locally from the `public/` directory:

```bash
python3 -m http.server 8000 --directory public
```

Then open `http://localhost:8000`. The CMU Pronouncing Dictionary file (`cmudict-0.7b.txt`) must be present in `public/` and is loaded via `fetch()` at page load.

## Architecture

This is a single-page app contained entirely in `public/index.html` (inline CSS + JS, no build step). It has no dependencies beyond Bootstrap 5 via CDN.

**Data flow:**
1. On load, `loadDictionary()` fetches `cmudict-0.7b.txt` and parses it into `cmuDict` — a plain object mapping uppercase words to arrays of ARPABET phoneme strings (e.g. `{ "HELLO": ["HH", "AH0", "L", "OW1"] }`). Alternate pronunciations (words ending in `(\d+)`) are skipped.
2. `phonemeMap` — a plain object mapping each ARPABET base phoneme (stress digits stripped) to a user-defined SpellCast symbol — is initialized from the hardcoded `PHONEMES` array and updated live as the user edits the table inputs.
3. `translate(inputText)` tokenizes input by splitting on non-word characters (preserving separators), looks up each word token in `cmuDict`, maps phonemes through `phonemeMap`, applies case matching (all-caps / title-case / lowercase) to the result, and wraps unknown words in `[brackets]`.
4. Both the English textarea and all SpellCast table inputs fire `updateOutput()` on `input` events.

**Key globals in the script:** `PHONEMES` (hardcoded phoneme metadata), `phonemeMap`, `cmuDict`.
