# AGENTS.md

Guidance for AI agents working on **ufuk.dev** — the personal Jekyll site of
Ufuk Kayserilioglu. This is the canonical agent reference; `CLAUDE.md` points
here. See `README.md` for the human-facing overview.

## Commands

```sh
bundle install                  # install dependencies
bundle exec jekyll serve        # dev server at http://127.0.0.1:4000
bundle exec jekyll build        # build to _site/
bundle exec rake og_image       # regenerate assets/images/og-image.png
```

`_config.yml` is read only at boot — restart `jekyll serve` after editing it.
There is no test suite; verify changes by building and viewing pages in both
light and dark mode.

## Project layout

```
_config.yml            Site config + identity (name, role, tagline, avatar, domain, socials)
index.md               Home page bio (uses the `about` layout)
_layouts/
  default.html         Base HTML: head, header, nav, footer, theme script, analytics
  about.html           Home: $ whoami hero + def speaking / def podcasts / def writing
  post.html            Single post / page prose
_includes/
  favicon.html         Favicon link tags
  navigation.html      Nav links (from _config `navigation`) + theme toggle
  social-footer.html   Footer social links (from _config `social`)
_talks/*.md            Talk entries (collection, output: false)
_podcasts/*.md         Podcast appearances (collection, output: false)
_posts/*.md            Blog posts (standard Jekyll; posts/index.html paginates)
_pages/                talks.md, podcasts.md, 404.html
archive.html           Full post archive grouped by month
assets/css/main.css    The entire stylesheet — plain CSS, served as-is
assets/images/         avatar.jpg, og-image.png (generated), favicons
_og/template.html.erb  Source template for the OG image
Rakefile               `og_image` task
design-options/        Historical design mockups (excluded from the build)
```

## Design language

The theme is "terminal-flavored editorial": proportional sans for all prose
and titles, monospace reserved strictly for terminal/code-flavored chrome
(header, nav, prompts, `def`/`end` markers, dates, meta lines, footer links).
**Do not let mono creep into prose or headings.** Single accent color is Ruby
red.

Styling rules:

- All colors/fonts are CSS custom properties in the tokens section at the top
  of `assets/css/main.css` (`:root` = light, `[data-theme="dark"]` = dark).
  Components must only use `var(--*)`, never hardcoded values.
- The stylesheet is **plain CSS with no preprocessor** — keep it that way, and
  write selectors flat (no nesting).
- Light/dark mode follows `prefers-color-scheme`, is toggleable from the
  header, persists to `localStorage`, and is applied before first paint by an
  inline script in `default.html` (no flash).

Structural motifs — reuse these for new sections/pages:

- Section = `def <name>` … `end` block (`.def-block` / `.section-head` /
  `.section-body` / `.section-end`)
- List entries = cards (`.entry`), grouped under `# <year>` markers
  (`.list-marker`), long text collapsed in `<details class="entry-abstract">`
- Bracket-style mono links: `[video]`, `[slides]` (`.entry-links`)

## Content model

- **Identity** (name, role, tagline, avatar, domain, socials) lives in
  `_config.yml` — edit there, not in templates.
- **Talks** (`_talks/*.md`): `title`, `event`, `date`, and optional `video`,
  `slides`, `site`. **Podcasts** (`_podcasts/*.md`): `title`, `podcast`,
  optional `episode`, `date`, `link`, `video`.
- Talks and podcasts render as year-grouped cards with collapsed
  abstracts/show notes. Each card's id is `{{ title | slugify }}`, and the
  home page deep-links to those anchors — keep the slug logic identical on the
  home layout and the listing pages.
- The `tagline` is a career pipeline written with `" → "` separators; the hero
  and OG image both split on it and accent the arrows plus the final segment.

## Open Graph image

`assets/images/og-image.png` (1200×630) is generated from
`_og/template.html.erb`, populated from `_config.yml` via `rake og_image`
(Ferrum-driven headless Chrome; set `CHROME_BIN` to override the browser).
After changing `domain`, `title`, `tagline`, `description`, `avatar`, or
`navigation`, rerun the task and commit the regenerated PNG. It is wired
site-wide through front-matter defaults, with the Twitter card set to
`summary_large_image`.

## Gotchas

- `domain` (not `host`) holds the bare hostname for display. `host` is a
  reserved Jekyll key — the `jekyll serve` bind address — and setting it to a
  domain makes the dev server fail with `EADDRNOTAVAIL`. `site.url` is
  rewritten to localhost by `jekyll serve`, which is why display uses
  `site.domain`.
- The `analytics` config key contains a verbatim HTML snippet emitted by
  `default.html`; there is no analytics include. Blank key = analytics off.
- Talks/podcasts collections have `output: false` but their `content` still
  renders as HTML on the listing pages — don't add `markdownify`.
- The dark theme keeps code blocks monokai-dark in *both* modes (intentional);
  inline code adapts via `--bg-raised`.
- `design-options/` holds historical mockups and is excluded from the build.
  The shipped design is `option-2d-combined.html`.

## Deployment

Pushes to `main` build and deploy to GitHub Pages via
`.github/workflows/jekyll.yml` (publishes `_site/` to `gh-pages`; `CNAME`
points ufuk.dev at it). The lockfile records the `x86_64-linux` platform so CI
can resolve native gems — keep it when running `bundle lock` or `bundle
update`.
