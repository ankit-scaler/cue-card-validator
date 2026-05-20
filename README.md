# Cue Card Validator

A single-file, offline validator for Scaler technical-content cue cards and quiz cards.
Paste a single card or a whole multi-card playlist; it splits the file by `---`
metadata blocks and validates each card, grouping results into collapsible
**Errors** and **Warnings** boxes.

## Use it

Open `index.html` in any browser — no build step, no dependencies, no network
(only Google Fonts loads remotely; it works fine offline too).

## Host it on GitHub Pages

1. Create a new repository (e.g. `cue-card-validator`).
2. Upload `index.html` (and this `README.md`) to the repo's default branch.
3. Repo **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Pick the branch (`main`) and folder (`/root`), then **Save**.
6. Wait ~1 minute. The site goes live at:
   `https://<your-username>.github.io/<repo-name>/`

## What it checks

- `---` is only allowed as a card's opening/closing metadata delimiter; any
  stray `---` is an error, and every opening `---` must have a closing `---`.
- Metadata: `title`, `duration`, `card_type` are **mandatory** (errors if
  missing). `description` is optional (warning if missing).
  All values follow `key: value` form on a single line.
- `title`: no `:`, no `---`, no emojis; allows letters, digits, spaces,
  hyphens, and `. , ? ' " & ( ) [ ] + * /`.
- `duration`: positive integer (seconds).
- `card_type`: exactly `cue_card` or `quiz_card`.
- Cue card: has body content with a heading.
- Quiz card: `# Question` (with content) + `# Choices`; ≥2 choices; exactly one
  correct; correct mark is lowercase `[x]` (capital `[X]` is an error).
- Quiz card must end at its choices — content after the last choice is dropped
  on ingestion and is flagged as an error.
