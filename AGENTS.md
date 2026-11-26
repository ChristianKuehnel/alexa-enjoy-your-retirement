# Working on this blog

This is a Jekyll blog on GitHub Pages about replacing Amazon Echo with Home Assistant Voice, one use case at a time. Keep it compatible with GitHub Pages and the existing Minima theme and `jekyll-feed` plugin.

## Repository layout

- `index.md` is the blog homepage; `README.md` is the GitHub repository landing page.
- `_posts/` contains dated Markdown posts.
- `assets/images/` contains images used by the site.
- `_config.yml` controls Jekyll settings. Keep repository-only docs out of the published site.

## Writing and editing

- Name new posts `YYYY-MM-DD-short-descriptive-slug.md` and start them with YAML front matter (`layout: post` and an explicit `title`). Use the front-matter title instead of repeating it as an H1 in the body. Use the intended publication date and don't rename published posts unless there's a plan to preserve their URLs.
- Keep the author's first-person voice. Distinguish what was tested from what is planned, and include relevant hardware and software versions when they affect the results.
- Use descriptive headings, link text, and image alt text. Compress images before committing them and check screenshots and configuration examples for secrets or private household details.
- Use Jekyll's `relative_url` filter for local assets (for example, `{{ '/assets/images/example.png' | relative_url }}`) and `post_url` for links to posts. Avoid hard-coded root-relative paths: this site is hosted under `/alexa-enjoy-your-retirement/`.

## Before opening a pull request

- Follow the [README preview setup](README.md#preview-locally). Check changed pages in the browser, including links and images under the project URL prefix. For post changes, also check the home listing and RSS feed.
- Run `git diff --check`. Keep generated files such as `_site/` and local dependency files out of commits.
- Keep pull requests focused. Summarize what readers will see change and what you verified.
