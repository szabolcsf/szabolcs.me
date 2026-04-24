# szabolcs.me

Source for [szabolcs.me](https://szabolcs.me), my personal site and blog.

## Stack

- [Zola](https://www.getzola.org/) static site generator
- `pulse` theme (a fork of [tabi](https://github.com/welpo/tabi) living under `themes/pulse`)

## Local development

```bash
zola serve
```

Opens a live-reloading preview at <http://127.0.0.1:1111>.

## Layout

```
content/     Markdown posts and pages
templates/   Tera templates (overrides on top of the pulse theme)
sass/        Custom styles compiled by Zola
static/      Assets copied verbatim to the site root
themes/      pulse (in use) and tabi (reference)
config.toml  Zola config
```

## License

Content (everything under `content/`) is © Szabolcs Fazekas, all rights reserved. Code (templates, styles, config) is MIT.
