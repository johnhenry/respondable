# Agent playbook

`@johnhenry/respondable` -- two custom elements for responding to CSS media
queries declaratively: `query-container.component` (swap by query) and
`attribute-provider.component` (style/class/attribute by query). One npm
package, one subpath export per module (`"./*": "./src/*"`) -- no shared
barrel, no build step.

`CLAUDE.md` in this directory is a symlink to this file.

## The verification loop (before every push)

1. `node --check` every `.mjs`/`.js` file you touched.
2. No DOM test environment is configured -- verify a change against the
   module's own `demo.htm` in a real browser (`npx serve .` from the repo
   root, then open `src/<module>/demo.htm`), and actually resize the
   window/devtools viewport to confirm the query breakpoints fire.
3. `npm pack --dry-run` -- confirm the file list is complete.
4. A genuinely fresh clone: `git clone . /tmp/respondable-verifyN && cd $_ && npm ci && npm test`.

## Repo-specific gotchas

- **Both modules depend on the real `parsel-js` npm package** for parsing
  the `[media query] value` grammar -- not a vendored copy. If you touch
  the query-parsing logic, check `parsel-js`'s actual `tokenize()` output
  shape rather than assuming.
- **Neither module has a `global.mjs`** -- both are meant to be bootstrapped
  via [`@johnhenry/definable`](https://github.com/johnhenry/definable)'s
  `define-component.component` (`<define-component name="..." src="...">`),
  matching their own demo files. Don't add a `global.mjs` without checking
  whether that's actually wanted first -- it was an intentional omission
  in the original `lib` source, not an oversight.
- **The demo files intentionally do NOT show a live window-width/height
  value** in the `#width`/`#height` decorative elements. They used to, via
  a `css-model-window` module that was never actually migrated out of
  `lib` during domkit's original extraction -- rather than chase that
  dependency chain (`css-model-window` → an undocumented `css-model`
  module) for something purely decorative, it was dropped. If you want
  that back, `lib`'s `js/css-model-window/0.0.0/` and `js/css-model/0.0.0/`
  are the source to port.

## Definition of done (adding or changing a module)

- `node --check` passes.
- The module's own `readme.md` is accurate.
- Any cross-package reference (to `@johnhenry/definable`, `@johnhenry/domkit`)
  uses the real published package name/CDN URL, not a stale relative path
  from when this was still inside domkit.

## Non-goals

- No bundling/build step is planned -- modules ship as source.
- No test environment (jsdom/happy-dom) exists yet, matching domkit's own
  current state.

## Releases

Bump `version` in `package.json` in a PR, add a `CHANGELOG.md` entry,
merge, then `gh release create v<version>` (fires
`.github/workflows/publish.yml`, gated on the full CI suite).
