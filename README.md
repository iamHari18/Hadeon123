# Hadeon

Placement preparation and study material for core electronics jobs (analog, digital, Verilog, embedded systems, edge AI).

Live site: https://iamhari18.github.io/hadeon123/

Plain static HTML + one CSS file. No framework, no build step. GitHub Pages serves the files exactly as they are in this repo.

## Folder layout

```
/                       site root (served at /hadeon123/)
├── index.html          home page
├── about.html
├── 404.html            served by GitHub Pages for missing URLs (uses /hadeon123/... absolute links)
├── favicon.svg
├── sitemap.xml         list of every page for Google
├── robots.txt          allows all crawlers, points to sitemap.xml
├── .nojekyll           tells GitHub Pages not to run Jekyll
├── assets/
│   └── style.css       the only stylesheet, used by every page
├── placement/
│   ├── index.html                                   placement hub (rounds, roadmap)
│   ├── analog-electronics-interview-questions.html
│   ├── digital-electronics-interview-questions.html
│   ├── verilog-interview-questions.html
│   ├── embedded-systems-interview-questions.html
│   ├── edge-ai-interview-questions.html
│   └── aptitude-and-hr.html
├── study/
│   └── index.html      subject list (notes marked "Coming soon" until published)
└── updates/
    └── index.html      update log
```

All links between pages are relative (`../assets/style.css`, `placement/`), so the site works under `/hadeon123/` and would also work if moved to a custom domain. The exception is `404.html`, which uses `/hadeon123/...` links because GitHub Pages can show it at any depth. If the repository is renamed, update those links, every `canonical` / `og:url` / JSON-LD URL, `sitemap.xml` and `robots.txt`.

## Add an update

1. Open `updates/index.html`.
2. Copy the example `<li>` block from the HTML comment above `<ul class="log">`.
3. Paste it as the first `<li>` in the list (newest first) and edit the date (ISO format, `YYYY-MM-DD`, in both `id` and `<time>`), headline, text and source link.
4. Optional: add it to the "Latest updates" list on `index.html` as well.
5. In `sitemap.xml`, set `<lastmod>` for `updates/` (and `/` if you changed the home page) to today's date.

Only publish news with a link to the original source.

## Add a new page

1. Copy an existing page at the same folder depth (for example `placement/aptitude-and-hr.html` for a page inside `placement/`).
2. Change, in `<head>`:
   - `<title>`: unique, 60 characters or fewer.
   - `<meta name="description">`: unique, 155 characters or fewer.
   - `<link rel="canonical">` and `og:url`: the page's full URL, e.g. `https://iamhari18.github.io/hadeon123/placement/new-page.html`.
   - `og:title`, `og:description`, `twitter:title`, `twitter:description`.
   - The `BreadcrumbList` JSON-LD (names and URLs).
   - For a Q&A page, the `FAQPage` JSON-LD must contain the same questions and answers as the visible page.
3. Keep exactly one `<h1>`, then `<h2>` for sections and `<h3>` for questions/sub-sections. Give each `<h2>` an `id` and list it in the contents box.
4. Link to the new page from at least one existing page (a hub page and the related-pages list).
5. Add a `<url>` entry to `sitemap.xml` with today's date as `<lastmod>`.

## Q&A markup

Each question on a question-bank page looks like this:

```html
<div class="qa" id="q12">
  <h3><span class="qn"><a href="#q12">Q12</a></span>
      <span class="qt">Question text?</span>
      <span class="lvl lvl-m">Medium</span></h3>
  <div class="ans"><p>Answer…</p></div>
</div>
```

Difficulty classes: `lvl-e` (Easy), `lvl-m` (Medium), `lvl-h` (Hard). Question numbers continue across sections on a page; if you insert a question in the middle, renumber the ones after it (ids and text) and update the counts at the top of the page.

## Google Search Console

`index.html` has a comment in `<head>` marking where to paste the `google-site-verification` meta tag. After verifying, submit `https://iamhari18.github.io/hadeon123/sitemap.xml` in Search Console.

## Local preview

```
cd ..            # the folder that contains this repo
mkdir -p preview && cp -r hadeon preview/hadeon123
cd preview && python3 -m http.server 8000
```

Then open http://localhost:8000/hadeon123/.
