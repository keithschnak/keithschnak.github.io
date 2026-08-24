# site/

A hand-written replacement for the Wix site. Nothing here is live — the repo's
root `index.html` still redirects to sites.wustl.edu, and this folder is ignored
by GitHub Pages until you move it.

## Files

    index.html       home: bio, recent work, teaching
    research.html    full publication list + working papers
    volleyball.html  unchanged text, both original links
    style.css        all styling for all three pages
    images/          the five tournament photos

## Editing

Everything visual lives in the `:root` block at the top of `style.css`.
The palette is WashU's: `--brand` is WashU Red (#BA0C2F, used only for the
3px rule at the top of the page), `--accent` is WashU Dark Red (#971B2F,
used for links and section headings), `--secondary` is a muted WashU teal
used only for publication status tags.

Adding an abstract to a paper — drop this inside its `<div class="entry">`:

    <details><summary>Abstract</summary><p class="abstract">...</p></details>

The CSS for it is already in `style.css`.

## Photos

`images/` holds the five shirt photos pulled off the Wix site, renamed from Wix's
hashes: `champions-blue`, `beach-365`, `champions-maroon`, `sandbar-navy`,
`sandbar-green`. They are the original AVIF files, untouched — no re-encoding,
about 255 KB for all five. AVIF works in every current browser but not in
Safari 15 or earlier; if that matters, JPEG fallbacks can be added.

They keep their own proportions in the grid rather than being cropped square.
To reorder them, reorder the `<img>` tags in `volleyball.html`.

## Links that still need attention

- "Democratic Accountability with Citizen Coproduction" has no journal link yet.
- `pdf/POL363.pdf` is in the repo but not linked from anywhere.

## Fonts

The pages load Literata and Public Sans from Google Fonts. To self-host instead
(one fewer third-party request, and the site keeps working if Google's CDN is
blocked), run this from inside `site/`:

    mkdir -p fonts && cd fonts
    curl -o literata.woff2 "$(curl -s -H 'User-Agent: Mozilla/5.0' \
      'https://fonts.googleapis.com/css2?family=Literata:opsz,wght@7..72,400..600' \
      | grep -o 'https://[^)]*\.woff2' | head -1)"

then add an `@font-face` rule to `style.css` and delete the three `<link>`
tags from each page's `<head>`.

## Going live

When you want this to be the site, from the repo root:

    git mv site/index.html site/research.html site/volleyball.html site/style.css .
    rmdir site   # after moving README.md wherever you want it

No path edits needed — the syllabus and CV links are absolute
(`https://keithschnak.github.io/pdf/...`), so the pages work from any folder.
