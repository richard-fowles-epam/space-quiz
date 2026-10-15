# Orbit space quiz

## Running and checking the app

Open `index.html` directly in the integrated browser using its local `file://` URL.
On macOS, `open index.html` opens it in the default browser. Keep the app usable
directly from disk without a server, dependencies, external fonts, or remote assets.

For a focused browser check, reload the page and test the affected interaction on
the first question: `2` selects Mars correctly; `1` selects Venus incorrectly.
Reloading resets the entire quiz.

For a full browser smoke test:

- Check native Tab/Shift+Tab navigation, visible focus, Enter/Space button
  activation, and the `1`-`4` answer shortcuts. Synthetic keyboard events alone
  do not verify native tabbing or button activation.
- Confirm Next is disabled until an answer is selected, then all answers lock
  and focus moves to Next. Advancing focuses the new question heading.
- Confirm a correct answer adds exactly one point and shows green feedback;
  a wrong answer adds none, shakes red, and reveals the correct answer.
  Both paths show an explanation and advance progress. Repeated selections
  must not change the score.
- Complete all ten questions and check the final score, correct/incorrect totals,
  emoji reaction, results-heading focus, and replay resetting score and progress.
  Numeric answer keys must do nothing on the results screen.
- Check both color schemes, a narrow viewport, and reduced-motion preferences.

The current all-correct numeric-key sequence is `2, 3, 4, 1, 3, 2, 3, 4, 1, 2`.
Result reactions change at scores 4, 7, and 10.

## Architecture

`index.html` is the complete application: inline CSS, semantic HTML, inline SVG
artwork, and a plain JavaScript script at the end of the body.

The quiz uses in-memory state (`current`, `score`, `answered`).
`renderQuestion()` recreates answer buttons and clears feedback;
`choose(index)` is the shared mouse/keyboard answer path, locks the question,
updates score/progress, and displays feedback; `showResults()` switches from
`#quiz` to `#result`. Replay resets state before rendering the first question.
Reloading discards all progress.

Question records contain `category`, `question`, four `answers`, a zero-based
`correct` index, and `fact`. Preserve the ten-question format: some counters,
progress markup, result totals, and score thresholds explicitly assume ten,
even where navigation uses `questions.length`.

## Conventions to preserve

- Use the existing `$()` helper for ID lookups. Keep question and explanation
  strings inserted through `textContent`; `innerHTML` is used for controlled
  markup templates.
- Theme colors are CSS custom properties in `:root`, overridden by
  `prefers-color-scheme: dark`. Use paired foreground/background tokens for
  feedback and check new text against its actual background in both themes.
- Keep the centered 520px maximum-width column, 15px sans-serif body, mobile
  adjustments at 420px, and monospaced mission-control heading treatment.
- Animate progress with `transform: scaleX()` from the left. The final
  `prefers-reduced-motion` rule disables animations and transitions.
- Preserve `[hidden]` screen switching, native answer buttons, the
  `answered` guard, and disabled states. Numeric shortcuts ignore Alt/Ctrl/Meta,
  held-key repeats, and the results screen.
- Preserve score and feedback live announcements, progressbar ARIA values,
  heading-label relationships, and programmatic heading focus via `tabindex="-1"`.
  Correctness is conveyed through text and symbols as well as color.
