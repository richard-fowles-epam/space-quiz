# Orbit space quiz

Orbit is a ten-question quiz about space exploration. Each answer includes an
explanation, and the results screen shows the final score and lets players review
their missed answers. The app supports keyboard controls, light and dark colour
schemes, and reduced-motion preferences.

The website is published at
[richard-fowles-epam.github.io/space-quiz](https://richard-fowles-epam.github.io/space-quiz/).

## Running locally

Open `index.html` in a browser. On macOS, this can be done from the repository
directory with:

```sh
open index.html
```

There is no installation or build step. The HTML, CSS, JavaScript and SVG artwork
are all in `index.html`, with no external assets or dependencies. The app works
directly from disk and does not need a web server.

Answers can be selected with the mouse or the `1`-`4` keys. Tab and Shift+Tab move
between controls, and Enter or Space activates a focused button. Reloading the
page resets the quiz; the replay button starts another attempt after the results.

## Deployment

`.github/workflows/pages.yml` validates the inline JavaScript and packages only
`index.html` as the website artifact. Pull requests targeting `main` run the
validation and packaging job without deploying. Pushes to `main` publish the
artifact to GitHub Pages. The workflow can also be run manually from the Actions
tab on `main`.

The repository's Pages source is **GitHub Actions** under
**Settings > Pages**. Deployment uses the `github-pages` environment and the
workflow's short-lived GitHub token; no separate deployment secret is needed.
