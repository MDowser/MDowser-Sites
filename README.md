# MDowser-Sites

Curated site list behind the MDowser omnibox suggestions.
MDowser vendors this file as `assets/builtin_sites.txt` via an explicit manual sync (`make sync-sites` in MDowser).

## Format

One entry per line:

`<url><TAB><title>`

- Blank lines and lines starting with `#` are ignored.
- `URL` must be a page MDowser can open (`https://`, or local `file://`).
- Use normalized store form: trailing `/` for HTTPS roots (e.g. `https://example.com/`).
- Append new entries at the end: display order = file order.
- Titles are short human names (max ~60 chars).

Example:

    https://example.com/<TAB>Example
    https://docs.example.com/<TAB>Example Docs

(where `<TAB>` is a literal tab character)

## Contribute

1. Append one line at the end of `builtin_sites.txt` in the same format.
2. Keep display order stable: don't reorder or edit existing lines unless the URL is dead.
3. Open a PR. No automated checks run here.

## Validation

The maintainer validates every PR manually before syncing into MDowser. A URL is accepted when the MDowser browser can open it, i.e. at least one route candidate answers as markdown:

- candidates: `URL`, `URL/`, `URL.md`, `URL/index.md`, `URL/README.md` (root: `/`, `/index.md`, `/README.md`)
- request sent with `Accept: text/markdown;q=0.8`
- response must be `2xx` with a markdown `Content-Type` (`text/markdown` or its `text/x-markdown` / `application/markdown` / `application/x-markdown` aliases), UTF-8 body, parsable frontmatter.

There is intentionally no CI/workflow in this repo: validation is a manual maintainer step in MDowser.
