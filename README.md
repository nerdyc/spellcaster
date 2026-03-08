# Spell Caster

A single-page tool for exploring phonetic respelling of English. Type any English text and see it instantly rewritten using symbols you define for each sound in the language.

## What it does

Spell Caster translates English words into a custom phonetic spelling of your design. It uses the [CMU Pronouncing Dictionary](http://www.speech.cs.cmu.edu/cgi-bin/cmudict) to look up how each word is pronounced as a sequence of [ARPABET](https://en.wikipedia.org/wiki/ARPABET) phonemes, then substitutes whatever symbol you've assigned to each phoneme.

By default each phoneme maps to its own ARPABET code, so "hello" becomes something like "HHAHLOW". From there you can customize any phoneme — assign single letters, digraphs, symbols, or anything you like — and watch the output update in real time.

## Running locally

The dictionary is loaded via `fetch()`, so the page must be served over HTTP rather than opened as a file.

1. Place `cmudict-0.7b.txt` in the `public/` directory. You can download it from the [CMU Pronouncing Dictionary](http://www.speech.cs.cmu.edu/cgi-bin/cmudict).
2. Start a local server:
   ```bash
   python3 -m http.server 8000 --directory public
   ```
3. Open `http://localhost:8000` in your browser.
4. Wait for "Dictionary loaded." to appear, then start typing.
