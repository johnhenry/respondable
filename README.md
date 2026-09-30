# respondable

[![npm version](https://img.shields.io/npm/v/%40johnhenry%2Frespondable.svg)](https://www.npmjs.com/package/@johnhenry/respondable)
[![CI](https://github.com/johnhenry/respondable/actions/workflows/ci.yml/badge.svg)](https://github.com/johnhenry/respondable/actions/workflows/ci.yml)
[![license](https://img.shields.io/npm/l/%40johnhenry%2Frespondable.svg)](LICENSE)

Full documentation: [opensource.johnhenry.me/respondable](https://opensource.johnhenry.me/respondable/)

> **Archived, and renamed on the way back in.** This package is folded
> back into [`@johnhenry/domkit`](https://github.com/johnhenry/domkit) as
> of domkit `0.0.4`, as `@johnhenry/domkit/matchable/<module>/...` — the
> package is renamed `matchable` there (this name read too close to
> "responsive design," a much more common and differently-scoped web
> term; `matchable` names the actual shared mechanism, `matchMedia()`).
> The unscoped npm package `@johnhenry/respondable` is deprecated (not
> removed) and will keep working at its last published version; this repo
> is archived (read-only, not deleted).

> **Provenance:** extracted from [`johnhenry/lib`](https://github.com/johnhenry/lib)'s
> `js/` directory. Briefly part of [`@johnhenry/domkit`](https://github.com/johnhenry/domkit)
> (a toolkit of ~40 independent DOM/HTML-component modules), then split out
> as its own package because these two elements are two duals of the same
> idea -- respond to a media query by swapping vs. by styling -- with a
> shared query-string grammar and a real dependency
> ([`parsel-js`](https://github.com/LeaVerou/parsel)) neither of domkit's
> other widgets needed.

Two custom elements for responding to CSS media queries declaratively,
without writing `matchMedia()`/`ResizeObserver` JavaScript by hand:

| Module | What it does |
|---|---|
| [`query-container.component`](src/query-container.component/readme.md) | `<query-component query="[(min-width:600px)] ol.wide">` -- swaps the rendered child element entirely by media query. |
| [`attribute-provider.component`](src/attribute-provider.component/readme.md) | `<attribute-provider classes="[(min-width:512px)] wide">` -- applies classes/styles/attributes to an existing child by media query, instead of swapping it. |

Both parse the same pipe (`|`)-delimited `[media query] value` grammar via
[`parsel-js`](https://github.com/LeaVerou/parsel) — a real npm dependency,
not a vendored copy.

## Which one do I want?

| I want to... | Use |
|---|---|
| Show an entirely different element by breakpoint | `query-container.component` |
| Style/class/attribute an existing element by breakpoint, without replacing it | `attribute-provider.component` |

## Install

```sh
npm install @johnhenry/respondable
```

or, in a browser with no build step, via a CDN (bootstrapped through
[`@johnhenry/definable`](https://github.com/johnhenry/definable)'s
`define-component.component`, since neither module here has its own
`global.mjs` — see each module's own readme for the full pattern):

```html
<script
  type="module"
  src="https://esm.sh/@johnhenry/definable/define-component.component/global.mjs"
></script>
<define-component
  name="query-component"
  src="https://esm.sh/@johnhenry/respondable/query-container.component/index.mjs"
></define-component>
```

## Family

- [`@johnhenry/definable`](https://github.com/johnhenry/definable) --
  both modules' own demos bootstrap themselves via its
  `define-component.component` (`<define-component>`), since neither has a
  self-registering `global.mjs` of its own.
- [`@johnhenry/domkit`](https://github.com/johnhenry/domkit) -- the toolkit
  this package was originally part of.

## License

MIT
