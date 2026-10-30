# Agent guide

Read this file **before modifying the repository**, then consult the relevant linked docs. This is a fictional Halloween personnel dossier and Rickroll verification prop, not a real security service.

## Map and stack

- Astro 7 static site; plain page-local CSS and browser TypeScript/JavaScript, no backend or database. `src/pages/index.astro` serves `/`; `src/pages/verify.astro` serves `/verify`. Assets are in `public/`.
- `astro.config.mjs` uses default static output; `wrangler.jsonc` serves `dist/` through Cloudflare static assets. `package.json` and `pnpm-lock.yaml` define dependencies; Node `>=22.23.4` and pnpm are prerequisites.
- Read [architecture](docs/architecture.md) for UI states/data flow, [conventions](docs/conventions.md) for local patterns, [security](docs/security.md) for trust boundaries, [deployment](docs/deployment.md) for hosting/QR behavior, and [decisions](docs/decisions.md) for evidenced implementation choices.

## Work safely

- Start development only in background: `pnpm astro dev --background`; manage it with `pnpm astro dev status`, `pnpm astro dev logs`, and `pnpm astro dev stop`. Run `pnpm build` to validate static output; `pnpm preview` previews a build. There is no configured test or lint suite. See [development](docs/development.md).
- Preserve the page-local DOM/CSS patterns, accessibility and reduced-motion handling; avoid touching unrelated files or generated `dist/`. Review existing work before editing.
- Never present the mock hash, authentication, encryption, location, or audit UI as real controls or legal evidence. There is no application audit backend. Do not commit secrets or imply no external requests: both pages load Google Fonts. Media rights are unverified.

## Documentation contract

1. Read this guide before repository edits and consult affected `docs/` files first.
2. Follow established architecture and coding conventions; validate the specific change and run `pnpm build` when applicable.
3. Update documentation when behavior, architecture, configuration, or workflows change.
4. Record significant new architectural decisions with evidence and rationale in [decisions](docs/decisions.md).
5. Avoid duplication; keep documentation accurate, concise, consistent with code, and never describe planned functionality as implemented.

## Astro references

Consult relevant official guides before related work: [routing](https://docs.astro.build/en/guides/routing/), [components](https://docs.astro.build/en/basics/astro-components/), [framework components](https://docs.astro.build/en/guides/framework-components/), [content collections](https://docs.astro.build/en/guides/content-collections/), [styling](https://docs.astro.build/en/guides/styling/), [internationalization](https://docs.astro.build/en/guides/internationalization/). [Full documentation](https://docs.astro.build).
