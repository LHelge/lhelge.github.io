# CLAUDE.md

Project-specific guidance for working on lhelge.se. The site is built with
[aphid](https://aphid.lhelge.se), a Rust-based static site generator for blogs
and wikis. For aphid mechanics, see the `aphid-content` and `aphid-theme`
skills, which load automatically when relevant.

## Project overview

Personal site for LHelge at https://lhelge.se — a notebook for small projects
and the occasional blog post. Long-running or larger projects live on their
own sites and are represented here by a wiki page that links out:

- Aphid (the static site generator that builds this site) → https://aphid.lhelge.se ([[Aphid]])
- Aphid EV (Beetle → Leaf-drivetrain conversion) → https://bladlus.se ([[Aphid EV]])

The site is intentionally low-traffic and infrequently updated — don't write
posts that assume an audience or a publishing cadence.

## Build

```sh
aphid serve            # dev server on http://localhost:3000 with live reload
aphid build            # render to dist/
aphid blog new "Title" # scaffold a dated blog post
aphid wiki new "Title" # scaffold a wiki page
```

## Writing voice (blog posts and home.md)

- First person, casual, deliberately understated. Contractions are fine.
- Occasional emoji and italicized asides are welcome (see the hello-world post).
- No marketing language, no "in this post we will explore…", no audience-building framing.
- Frame the site as a personal notebook, not a blog with readers to retain.

Wiki pages use a more neutral reference tone — they should still read like notes
to future-me, but stripped of first-person commentary.

## Anonymity

Keep author details light. Fine to share: I'm a software engineer in Sweden
(matches the framing in `content/home.md`). Don't introduce new specifics
about my employer, location beyond "Sweden", family, daily routine, or other
personal-life details — even when they come up in conversation. Treat what's
already published on the site as the baseline; don't extrapolate beyond it.
If a draft seems to need that kind of biographical detail to land, flag it
instead of inventing or guessing.

## Cross-linking projects

When you mention one of my projects in prose, link to its wiki page with
`[[Name]]`, e.g. `[[Aphid]]` or `[[Aphid EV]]`. External links (source code,
the dedicated project site, crates.io, etc.) live in the wiki page itself
under a `# Links` section — don't paste them inline in blog posts.

## Wiki organisation

The wiki is open-ended — currently mostly project pages under
`category: Projects`, but new categories can be added freely as the notebook
grows. Don't assume "Projects" is the only category.

## Hosting and deploy

Auto-deploys to GitHub Pages from `main` via `.github/workflows/pages.yml`.
PRs are built (but not deployed) by `.github/workflows/check.yml`. Both
workflows pin the `LHelge/aphid@vX.Y.Z` action — **bump the version in both
files together** when upgrading aphid, otherwise PR checks and deploys will
drift apart.

Domain is `lhelge.se`, configured via `static/CNAME`.
