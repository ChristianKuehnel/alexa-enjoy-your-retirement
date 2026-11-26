# Alexa, Enjoy Your Retirement!

A blog about replacing Amazon Echo with a self-hosted Home Assistant Voice setup, one use case at a time.

[Read the blog](https://christiankuehnel.github.io/alexa-enjoy-your-retirement/) · [Subscribe via RSS](https://christiankuehnel.github.io/alexa-enjoy-your-retirement/feed.xml)

## Edit the blog

The site uses Jekyll and the Minima theme on GitHub Pages. Edit the homepage in [`index.md`](index.md), add posts to [`_posts/`](_posts/), and put images in [`assets/images/`](assets/images/). See [AGENTS.md](AGENTS.md) for post formatting and review guidelines.

## Preview locally

With [Ruby, Bundler, and the tools to build native gems](https://jekyllrb.com/docs/installation/) installed, run the following from the repository root. The temporary Gemfile uses GitHub Pages' dependencies without adding local setup files to the repository.

```sh
preview_dir=$(mktemp -d)
cat > "$preview_dir/Gemfile" <<'EOF'
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
gem "webrick"
EOF
BUNDLE_GEMFILE="$preview_dir/Gemfile" bundle install
BUNDLE_GEMFILE="$preview_dir/Gemfile" bundle exec jekyll serve --baseurl /alexa-enjoy-your-retirement --destination "$preview_dir/_site"
```

Open [http://localhost:4000/alexa-enjoy-your-retirement/](http://localhost:4000/alexa-enjoy-your-retirement/). To preview a deliberately future-dated post without changing when it goes live, add `--future` to the `serve` command.
