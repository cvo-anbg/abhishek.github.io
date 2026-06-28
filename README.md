# ANB Solutions GitHub Pages Site

Static website for [abhishek-austin.github.io](https://abhishek-austin.github.io/).

The home page is a hand-built single page; the **Writing** section is a Jekyll
blog that GitHub Pages builds automatically.

## Publishing a blog post

See **[PUBLISHING.md](PUBLISHING.md)** — a step-by-step, no-tooling guide for
adding a weekly post through the GitHub web UI. Short version: add one Markdown
file to `_posts/` and commit.

## SEO

The site ships search-engine basics out of the box:

- **`sitemap.xml`** and **`feed.xml`** (RSS) are generated automatically by the
  `jekyll-sitemap` and `jekyll-feed` plugins on every build.
- **`robots.txt`** points crawlers at the sitemap.
- **Open Graph / Twitter cards**, canonical URLs, and per-page titles and
  descriptions are set for the home page and every blog page.
- **JSON-LD structured data** (`Person` / `Organization` site-wide, `BlogPosting`
  on each post) helps search engines understand the content.

### Verify the site with Google Search Console (one-time)

Search Console shows which queries surface the site and lets you submit the
sitemap. To verify ownership of `abhishek-austin.github.io`:

1. Go to <https://search.google.com/search-console>, add a **URL prefix**
   property for `https://abhishek-austin.github.io/`.
2. Choose the **HTML file** verification method (simplest for this static site).
   Download the `google<...>.html` file it gives you.
3. Commit that file to the repository root and push. The file is served as-is.
4. Back in Search Console, click **Verify**.
5. Once verified, submit `https://abhishek-austin.github.io/sitemap.xml` under
   **Sitemaps**.

> Alternative: if you verify by **meta tag** instead, paste the token into
> `google_site_verification` in `_config.yml` (covers blog pages) and into the
> marked spot in `index.html` (covers the home page). When the site moves to a
> custom domain, DNS (TXT record) verification is the most durable option.

## Local Preview

The home page alone (no blog build):

```sh
python3 -m http.server 8000 --bind 127.0.0.1   # then open http://127.0.0.1:8000/
```

The full site including the blog (matches what GitHub Pages publishes):

```sh
bundle install
bundle exec jekyll serve   # then open http://127.0.0.1:4000/
```

## Deploy

This repository is deployed by GitHub Pages, which builds the Jekyll site and
publishes it. Pushing to the configured Pages branch triggers a rebuild.

## Structure

- `index.html` - Hand-built single-page home (inline styles/JS). No Jekyll front
  matter, so it is published as-is.
- `blog/index.html` - The Writing index that lists all posts.
- `_posts/` - One Markdown file per post (`YYYY-MM-DD-title.md`).
- `_layouts/`, `_includes/` - Shared page shell, nav, and footer for the blog.
- `assets/css/site.css` - Blog styles (mirrors the home page design system).
- `post-template.md` - Copy this to start a new post.
- `_config.yml` - Jekyll configuration (site metadata, plugins, SEO settings).
- `robots.txt` - Points crawlers at the sitemap.
- `images/` - Web-ready image assets.
- `sitemap.xml`, `feed.xml` - Generated at build time; not committed.

## Notes

- Keep committed images web-sized and stripped of personal camera metadata.
- Check the page locally before pushing, since pushes can trigger deployment.
- `index.html` keeps its own inline styles; the blog's `assets/css/site.css`
  intentionally mirrors that design system. Update both if the brand changes.
