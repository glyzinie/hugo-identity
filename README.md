# hugo-identity

## Requirements

This theme requires Hugo 0.146.0 or later and [Dart Sass](https://gohugo.io/functions/css/sass/#dart-sass).
Ensure the standalone Dart Sass `sass` executable is on `PATH` when building locally or in CI.

## Stylesheets

Hugo compiles `assets/main.scss` with Dart Sass and inlines the minified CSS
in the base layout. The `toCSS` call explicitly selects the `dartsass` transpiler.

- `assets/libs/_vars.scss`: colors, fonts, sizes, and animation durations.
- `assets/libs/_functions.scss`: accessors for the configuration maps.
- `assets/libs/_mixins.scss`: shared spacing styles.
- `assets/libs/_breakpoints.scss`: named width ranges and media query helpers.
- `assets/base/`: page defaults and typography.
- `assets/components/`: icon and social link selectors.
- `assets/layout/`: wrapper, profile, and footer selectors.

Each stylesheet loads its configuration and helpers explicitly with `@use`.
Keep shared functions and mixins in `libs`, and preserve the CSS module order
in `main.scss` when refactoring styles.

Custom SCSS should load the modules it uses, for example `@use 'libs/functions'`
and `@use 'libs/breakpoints'`, then call `functions.palette(highlight)` or
`@include breakpoints.breakpoint('<=xsmall')`. The old `_duration`, `_font`,
`_misc`, `_palette`, and `_size` helpers are now public module functions named
`duration`, `font`, `misc`, `palette`, and `size`.

The configuration maps in `libs/vars` and the `$breakpoints` map in
`libs/breakpoints` accept `@use ... with (...)` configuration. Configure these
modules before loading `main.scss` or any stylesheets that depend on them.

## Icons

The theme uses individual SVGs from [Simple Icons](https://simpleicons.org/)
for brands and [Lucide](https://lucide.dev/) for general icons. Hugo embeds only
the icons used on each page into its HTML. Icon rendering needs no CDN requests,
icon fonts, JavaScript, npm install, or network access during the build.

Set each social link's `icon` to `<library>/<name>` without the `.svg` extension.
The `name` supplies the link's accessible label and tooltip:

```toml
[[params.social]]
name = "GitHub"
url = "https://github.com/example"
icon = "simple-icons/github"

[[params.social]]
name = "Zenn"
url = "https://zenn.dev/example"
icon = "simple-icons/zenn"

[[params.social]]
name = "Hatena Blog"
url = "https://example.hatenablog.com/"
icon = "lucide/book-open"

[[params.social]]
name = "Email"
url = "mailto:hello@example.com"
icon = "lucide/mail"
```

Omit `icon` to display a regular text link instead.

### Included icons

| Purpose | `icon` |
| --- | --- |
| GitHub | `simple-icons/github` |
| Bluesky | `simple-icons/bluesky` |
| Discord | `simple-icons/discord` |
| Zenn | `simple-icons/zenn` |
| Qiita | `simple-icons/qiita` |
| note | `simple-icons/note` |
| X (Twitter) | `simple-icons/x` |
| Email | `lucide/mail` |
| Home | `lucide/house` |
| Link | `lucide/link` |
| Blog / Hatena Blog | `lucide/book-open` |
| RSS | `lucide/rss` |

The bundled Simple Icons release has no dedicated Hatena Blog logo or old
Twitter bird logo. `lucide/book-open` is a generic blog icon; `simple-icons/x`
is the current X logo.

### Migrating from Font Awesome

Replace Font Awesome class strings in your site's configuration, for example:

- `brands fa-github` → `simple-icons/github`
- `solid fa-envelope` → `lucide/mail`
- `solid fa-house` → `lucide/house`

Font Awesome classes and the Sass `icon` / `icon-alt` mixins are no longer used.
Invalid names and missing SVG files produce a Hugo build error identifying the
icon to fix, rather than an empty icon link.

For icons in Markdown content, replace Font Awesome HTML with the `icon`
shortcode and adjacent text:

```text
{{< icon "lucide/mail" >}} Email
```

The SVG is decorative and hidden from screen readers; the adjacent text or
social link's `name` provides its meaning.

### Adding or overriding an icon

Copy an individual SVG into your site's `assets/icons/simple-icons/<name>.svg`
or `assets/icons/lucide/<name>.svg`, then use its `<library>/<name>` identifier.
Names accept lowercase letters, digits, and hyphens. Files in the site override
theme files at the same path. Use Simple Icons assets for filled brand logos
and Lucide assets for stroked general icons.

Bundled SVGs retain their upstream contents. Exact versions, sources, and license
notices are in [licenses/icons](licenses/icons/README.md). Keep the corresponding
upstream notices when adding or updating icons.
