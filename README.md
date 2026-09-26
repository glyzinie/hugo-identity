# hugo-identity

## Stylesheets

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
