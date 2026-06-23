# danielmakelley.com

A minimal personal site: homepage, writing, about, and one sample post.
Inter, lots of whitespace, no JavaScript, no tracking. Pure HTML + CSS, no
build step. Drops straight onto Neocities, GitHub Pages, or a shell account.

## Files

```
index.html               homepage
blog.html                writing index
about.html               about
posts/shell-account.html one full sample post (copy this for new posts)
style.css                the whole look
```

## Customise

1. **Links.** The GitHub and email links use `danielmakelley` /
   `hello@danielmakelley.com` placeholders — set your real ones in
   `index.html` and `about.html`.
2. **Write posts.** Copy `posts/shell-account.html` to
   `posts/your-slug.html`, change the title/date/body, then add a `<li>` to
   `blog.html`. (Posts use `../` paths because they sit one folder down.)

## Font

Inter is loaded from Google Fonts (one external request). If you'd rather not
hit Google at all, self-host Inter from <https://rsms.me/inter/> and swap the
`<link>` tags for a local `@font-face`. The CSS already falls back to the
system UI font, so the site looks fine even if the webfont never loads.

## Preview locally

```bash
cd oldschool-site
python3 -m http.server 8000
# open http://localhost:8000
```

## Publish

- **Neocities:** drag the whole folder into the file manager.
- **GitHub Pages:** push to a repo named `danielmakelley.github.io`. The `CNAME`
  file in this folder tells Pages to serve on `danielkelley.me`. Configure DNS at
  your registrar with GitHub Pages' A and AAAA records.
- **Shell account:** `scp -r oldschool-site/* danielmakelley@sdf.org:~/html/`

## Notes

- `feed.xml` is referenced but not included; add it when you want RSS, or
  remove the links.
