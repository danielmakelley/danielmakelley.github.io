# AGENTS.md — danielmakelley.com

This file is a guide for AI coding agents working on this project. The project is a minimal, hand-written static personal site.

## Project overview

- **Name:** danielmakelley.com (working directory `oldschool-site`)
- **Purpose:** A small personal homepage with a writing index, an about page, and individual posts.
- **Technology stack:** Plain HTML5 and a single CSS file. No JavaScript, no build tools, no package manager, no server-side code.
- **Design philosophy:** Small, fast, durable. Lots of whitespace, Inter typeface, no tracking or analytics.

## File structure

```
oldschool-site/
├── index.html                      # Homepage + latest post list
├── blog.html                       # Writing index
├── about.html                      # About page + contact + PGP key link
├── style.css                       # Single stylesheet for every page
├── pubkey.asc                      # Public PGP key block
├── CNAME                           # GitHub Pages custom domain (danielkelley.me)
├── README.md                       # Human-facing setup/publish notes
└── posts/
    └── finding-vulnerabilities.html  # One published post
```

There are no `package.json`, `pyproject.toml`, `Cargo.toml`, `Makefile`, or similar configuration files. The site is served directly as static files.

## External dependencies

- **Google Fonts:** Loads the Inter typeface (`https://fonts.googleapis.com`). Each HTML page includes the same `<link>` block in `<head>`.
- **Self-hosting fallback:** `style.css` already falls back to system UI fonts, so the site is readable even if Google Fonts fails to load.

## Build process

There is no build step. Files are edited by hand and served as-is.

## Local preview

Use any static file server. The README suggests:

```bash
cd oldschool-site
python3 -m http.server 8000
# open http://localhost:8000
```

## Code style guidelines

- **Indentation:** Two-space soft tabs in HTML and CSS.
- **HTML:**
  - Use `<!doctype html>` and standard HTML5 boilerplate.
  - Keep `<head>` consistent across pages: charset, viewport, title, description, font links, stylesheet, optional RSS alternate.
  - Wrap page content in `<div class="wrap">`.
  - Use semantic elements: `<header class="masthead">`, `<main>`, `<article>`, `<footer>`, `<nav>`.
  - Posts live in `posts/` and reference `../style.css` and `../index.html` etc. with `../` paths.
  - Root pages reference `style.css`, `feed.xml`, and sibling pages without a prefix.
- **CSS:**
  - One shared stylesheet for the whole site.
  - CSS custom properties live in `:root` (`--bg`, `--ink`, `--muted`, `--rule`, `--link`, `--accent`, `--col`).
  - Prefer rems for sizing.
  - Keep the visual minimal: no animations except subtle link hover transitions.
- **Links:**
  - Body links are underlined via `border-bottom` (not `text-decoration: underline`).
  - Navigation and footer links have muted colour and no underline.

## Adding or editing content

### New posts

1. Create a new file in `posts/<slug>.html` by copying an existing post.
2. Update `<title>`, `<meta name="description">`, the `<h1>`, the `.meta` date, and the article body.
3. Add a `<li>` entry to `blog.html`.
4. Add a `<li>` entry to `index.html` if it should appear on the homepage.

### Updating navigation / contact links

- Social and email links appear in `index.html` and `about.html`.
- The site name "danielmakelley" is used consistently in titles and mastheads.

## Testing instructions

There is no automated test suite. Manual checks:

1. Start a local static server and open each page.
2. Verify all internal links work, especially from `posts/` back to root pages (they must use `../`).
3. Confirm `style.css` loads on root pages and on post pages.
4. Check that the RSS `<link rel="alternate">` matches the intended feed location.
5. Verify the page renders on narrow viewports (the CSS is mobile-first).

## Deployment

Any static host works. Common options mentioned in the README:

- **Neocities:** drag the entire folder into the file manager.
- **GitHub Pages:** push to a repo named `danielmakelley.github.io`. Include the `CNAME` file containing `danielkelley.me` and configure DNS at the registrar with GitHub Pages' A/AAAA records.
- **Shell account:** `scp -r oldschool-site/* user@host:~/html/`

## Known caveats

- `feed.xml` is referenced in `<link rel="alternate">` tags but is not present in the repository. Either create it or remove the references.
- `blog.html` and `README.md` reference a sample post `posts/shell-account.html` that does not exist; the only published post is `posts/finding-vulnerabilities.html`.

## Security considerations

- No JavaScript means no XSS surface from scripts on these pages.
- No cookies, analytics, or third-party trackers are loaded.
- The only external network request is to Google Fonts. If stronger privacy is required, self-host Inter and replace the Google Fonts `<link>` tags with a local `@font-face` declaration.
- `pubkey.asc` contains a public PGP key block used for contact encryption. Do not modify or replace it unless you are intentionally rotating keys.
