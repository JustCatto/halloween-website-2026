# Code conventions

- Route files are `src/pages/*.astro`; each owns its HTML, inline browser script, and scoped `<style>`. There is no shared component system or runtime framework. Prefer minimal local changes over new infrastructure for this small site.
- Browser behavior uses DOM element queries, `hidden`, CSS state classes, timers, and `Intl.DateTimeFormat`. Keep related accessibility behavior: buttons for actions, `aria-*` state, focus transfer when dismissing/reopening panels, and status announcements where already used.
- Astro CSS is scoped by default. Global selectors use `:global(...)`; DOM-created audit `<li>` and `<time>` elements in `verify.astro` require `:global()` selectors to receive scoped styles.
- Animations are guarded by `prefers-reduced-motion`; the verify media has a still-image alternative. Keep timing and visual states coherent on mobile (`max-width: 600px` in both pages).
- Assets are referenced by root-relative URL from `public/`. The QR's encoded absolute domain is distinct from the homepage's relative link; see [deployment](deployment.md).
- The copy deliberately presents a fictional security story. Retain clear joke/fiction framing and do not describe simulated UI as real controls; see [security](security.md).

Formatting is not enforced by a configured linter or formatter. Match adjacent code style (including existing indentation and naming) rather than reformatting whole pages. No automated tests are configured; run the build and manually check browser-dependent changes.
