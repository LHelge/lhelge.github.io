# lhelge.github.io

Personal homepage for LHelge, built with [aphid](https://aphid.lhelge.se).

Live site: https://lhelge.se

## Development

Build the site:

```sh
aphid build
```

Run the local dev server:

```sh
aphid serve
```

Custom port:

```sh
aphid serve -p 8080
```

## Project structure

- `content/` - Markdown content (`blog/`, `wiki/`, `pages/`, and `home.md`)
- `theme/` - Templates, CSS, and theme assets
- `static/` - Static files copied to output
- `aphid.toml` - Site configuration

Rendered output is written to `dist/`.
