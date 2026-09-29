# Changelog

All notable changes to this project will be documented in this file.

## [0.0.0] - 2026-09-29

Initial release. Extracted from [`@johnhenry/domkit`](https://github.com/johnhenry/domkit)
(originally from [`johnhenry/lib`](https://github.com/johnhenry/lib)'s `js/`
directory) -- `query-container.component` and `attribute-provider.component`,
split into their own package because they're two duals of the same idea
(respond to a media query by swapping vs. by styling), sharing a query-string
grammar and a real `parsel-js` dependency neither of domkit's other widgets
needed.

- Both modules moved in with their code, CSS, and demo files unchanged.
- Demo files (`demo.htm`) previously referenced two modules that were never
  actually migrated into `domkit` during its original extraction from
  `lib` (`css-model-window`, which drives a live window-width/height CSS
  custom-property display, and depends in turn on an undocumented
  `css-model` module) -- rather than chase that whole chain for what is
  purely decorative demo chrome (not part of either component's actual
  API), the width/height live-display styling was left in place but its
  driver was dropped; `#width::before`/`#height::before` now simply render
  no content instead of a live value. The core media-query-swap/style
  behavior each demo exists to show is unaffected.
- Demo files' `until-window-load`/`define-component`/
  `define-component-by-content` script references, previously relative
  paths into `domkit`'s own `js/`-equivalent tree, now point at
  [`@johnhenry/definable`](https://github.com/johnhenry/definable) via
  esm.sh, since those modules live there now.
- `attribute-provider.component/demo.htm`'s reference to `lib`'s
  `css/blank-slate` stylesheet was left as the original
  `johnhenry.github.io/lib/...` URL -- a generic CSS reset unrelated to
  this consolidation's scope, still live and published under `lib`'s own
  no-deletion policy.
