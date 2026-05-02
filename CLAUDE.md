# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Personal homepage of LHelge, built with [aphid](https://aphid.lhelge.se) — a Rust-based static
site generator for blogs and wikis with wiki-link support. The site documents small personal
projects (larger ones like the EV conversion [Aphid EV](https://bladlus.se) have their own sites).

## Build and develop

```sh
aphid build            # render site to dist/
aphid serve            # dev server on http://localhost:3000 with live reload
aphid serve -p 8080    # serve on a custom port
```

Output goes to `dist/` which is git-ignored. Configuration is in `aphid.toml`.

## Scaffold new content

```sh
aphid blog new "Post title"    # creates content/blog/YYYY-MM-DD_<slug>.md
aphid wiki new "Page title"    # creates content/wiki/<slug>.md
aphid page new "Page title"    # creates content/pages/<slug>.md
```

## Content authoring

Content lives under `content/` in three subdirectories:

- `content/blog/` — dated blog posts
- `content/wiki/` — reference/wiki pages
- `content/pages/` — standalone pages (About, Contact, etc.)

A special `content/home.md` (no frontmatter required) provides the homepage body.

Every content file is Markdown with YAML frontmatter delimited by `---`.

### Blog posts (`content/blog/`)

Required frontmatter: `title`, `slug`, `author`, `created` (YYYY-MM-DD).
Optional: `updated`, `image`, `description`, `tags` (list of strings).
The slug must be unique across all content. Use lowercase words separated by hyphens.
Filename pattern: `YYYY-MM-DD_slug.md`. Posts live at `/blog/<slug>/`.

### Wiki pages (`content/wiki/`)

All frontmatter fields are optional: `title`, `category`, `created`, `updated`, `tags`.
If `title` is omitted the filename stem is used. `category` groups pages on the wiki index.
Wiki pages live at `/wiki/<stem>/`.

### Standalone pages (`content/pages/`)

Required frontmatter: `title`. Optional: `order` (sort position in nav, lower = earlier).
Pages live at `/<stem>/`.

### Heading rules

The page title comes from frontmatter and is rendered as `<h1>` by the template. The markdown
pipeline shifts all heading levels up by one, so:

- Use `#` for top-level sections (becomes `<h2>`)
- Use `##` for subsections (becomes `<h3>`), and so on
- Never use `#` for the page title — that comes from frontmatter

### Wiki-links

Cross-link to any other page with `[[page-slug]]` or `[[page-slug|Display text]]`. The slug
is the filename without the `.md` extension. Wiki-links resolve across blog, wiki, and pages —
any slug that exists anywhere in `content/` is a valid target. Check what pages exist before
linking.

### Images and static files

Place files in `static/` and reference them with absolute paths:
`![alt](/static/images/photo.png)`.

### Supported markdown extensions

Tables, strikethrough (`~~text~~`), task lists (`- [x]`), footnotes (`[^1]`), and fenced code
blocks with syntax highlighting (specify the language after the opening fence).

### Writing style

- Blog posts: open with a concise introduction, use `#` sections, link to wiki pages where
  relevant, keep `description` to one or two sentences.
- Wiki pages: neutral reference tone, start with a summary paragraph, cross-link liberally.
- Keep content files focused — if a topic grows large, split it into its own page and link.

## Theme and templates

The theme lives in `theme/` (set via `theme_dir` in `aphid.toml`). For theme design details,
template variables, and the Tera template structure, use the `/aphid-design` skill.
