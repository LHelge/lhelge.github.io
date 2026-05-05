---
title: Aphid
category: Projects
tags:
  - rust
  - web
---

Aphid is a fast, opinionated static site generator built in Rust with first-class support for
blogs, wikis, and standalone pages — all powered by Markdown files. It's what builds this site.

# Features

- **Blog** with tags, pagination, and RSS/Atom feeds
- **Wiki** pages with `[[wiki-links]]` that resolve across all content types
- **Standalone pages** for things like About or Contact
- **Tera templates** — swap the entire look by pointing `theme_dir` in `aphid.toml`
- **Syntax highlighting** with CSS-class-based token markup
- **Mermaid diagrams** rendered client-side
- **GitHub-style alert blocks** (note, tip, warning, caution)
- **Table of contents** generated from headings
- **Draft flag** to keep unpublished content out of builds
- **Dev server** with WebSocket hot-reload - blazing fast rebuilds

# Content structure

```
content/
  home.md
  blog/
    2025-03-01_my-post.md
  wiki/
    some-topic.md
  pages/
    about.md
```

All content files use Markdown with YAML frontmatter. Wiki-links (`[[slug]]` or
`[[slug|Display text]]`) resolve across blog, wiki, and pages by filename stem.


# Installation

```sh
cargo install aphid --locked
```

# CLI usage

```sh
aphid build              # render to dist/
aphid serve              # dev server on :3000 with live reload
aphid blog new "Title"   # scaffold a dated blog post
aphid wiki new "Title"   # scaffold a wiki page
aphid page new "Title"   # scaffold a standalone page
```

# Performance

Built on Rayon and Tokio for multithreaded rendering. Incremental rebuilds during development
are near-instant even on larger sites.

# Links

- [Documentation](https://aphid.lhelge.se)
- [Source code](https://github.com/LHelge/aphid)
