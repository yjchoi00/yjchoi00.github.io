# yjchoi.dev

Personal site for Youngjun Choi — <https://yjchoi.dev>

A single hand-written static page. No build step, no dependencies, no
generator: `index.html` contains the markup, the CSS, and the small script for
the light/dark toggle. Every asset is local, so the page makes zero external
requests.

## Layout

```
index.html    the entire site — markup, styles, and script
logos/        institution marks used in Experience and Education
CNAME         custom domain (yjchoi.dev)
.nojekyll     tells GitHub Pages to serve the files as-is, without Jekyll
```

## Editing

Open `index.html` in an editor, then open the same file in a browser to see the
change. There is nothing to compile or serve.

## Deploying

GitHub Pages serves the `main` branch root directly, so pushing is deploying:

```bash
git pull
# edit
git add -A && git commit -m "..." && git push
```

The site is live about a minute later.

## History

This repo previously held an [al-folio](https://github.com/alshedivat/al-folio)
Jekyll site. That version, and its MIT license, remain in the git history before
the "Replace al-folio with a single static page" commit.
