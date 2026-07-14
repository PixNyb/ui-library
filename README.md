# UI Library

Reusable Sass primitives extracted from `roelc.me` and tuned so they can be consumed from other projects without assuming a fixed asset path.

## Usage

Import the entrypoint and include the mixins you need. The root file is now a thin facade over smaller partials in `sass/`

Use the facade if you want everything, or import individual partials if a project only needs a subset.

For projects that do not want to compile Sass, build the distributable CSS and consume the generated file instead:

```bash
npm run build:all
```

That compiles `sass/build.scss` into `dist/ui-library.css` and `dist/ui-library.min.css`, which can be referenced directly from a website, copied into an asset pipeline, or published as part of an npm package.

Because the package ships as a standard npm package, it can be installed by npm-compatible managers such as `npm`, `pnpm`, `yarn`, and `bun` without any extra packaging work.

Release tags should follow the `vX.Y.Z` format. The GitHub Actions release and publish workflows strip the `v` prefix and use the tag value as the package version during CI.

```scss
@use "ui-library/sass" as ui with (
  $font-family: "Inter", Arial, sans-serif,
  $font-family-variable: "Inter Variable", Arial, sans-serif
);

@include ui.install();
```

If you want to keep fonts in your own project, use the helper mixin instead of hardcoding paths in shared Sass:

```scss
@include ui.font-face("Inter", "/assets/fonts/Inter/Inter-Regular.ttf", 400);
@include ui.font-face("Inter", "/assets/fonts/Inter/Inter-Bold.ttf", 700);
```

## What is included

- Theme tokens and CSS custom properties for light and dark mode.
- Base element styling for typography, tables, code, blockquotes, lists, and images.
- Common UI primitives such as buttons, cards, forms, dialogs, flex helpers, a scroller utility, and Rouge syntax highlighting.
- No site-specific layout assumptions such as fixed headers, footers, or blog navigation.

## Installation patterns

- Sass projects: depend on the package and `@use` the Sass entrypoint.
- Non-Sass projects: install the package and load `dist/ui-library.css`, or build the CSS once and ship the generated `dist/` asset.
- Mixed setups: use the Sass source during development and the compiled CSS for distribution.