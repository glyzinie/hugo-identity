# hugo-identity

## Requirements

This theme requires Hugo 0.146.0 or later and [Dart Sass](https://gohugo.io/functions/css/sass/#dart-sass).
Ensure the standalone Dart Sass `sass` executable is on `PATH` when building locally or in CI.

## Stylesheets

Hugo compiles `assets/main.scss` with Dart Sass and inlines the minified CSS
in the base layout. The `toCSS` call explicitly selects the `dartsass` transpiler.

- `assets/libs/_vars.scss`: colors, fonts, sizes, and animation durations.
- `assets/libs/_functions.scss`: accessors for the configuration maps.
- `assets/libs/_mixins.scss`: shared icon and spacing styles.
- `assets/libs/_breakpoints.scss`: named width ranges and media query helpers.
- `assets/base/`: page defaults and typography.
- `assets/components/`: icon and social link selectors.
- `assets/layout/`: wrapper, profile, and footer selectors.

Load configuration and helpers before base, component, and layout styles.
Keep shared functions and mixins in `libs` so components do not depend on
each other's import order. Preserve selector order when refactoring styles.
