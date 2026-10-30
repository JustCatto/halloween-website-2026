# Development

Prerequisites: Node.js `>=22.23.4` (from `package.json`) and pnpm. Install with `pnpm install` from the repository root; the dependency tree is locked in `pnpm-lock.yaml`. `pnpm-workspace.yaml` permits build scripts for esbuild and workerd.

| Task | Command |
| --- | --- |
| Install | `pnpm install` |
| Start development server in background | `pnpm astro dev --background` |
| Inspect background server | `pnpm astro dev status` / `pnpm astro dev logs` |
| Stop background server | `pnpm astro dev stop` |
| Build static site | `pnpm build` |
| Preview build locally | `pnpm preview` |

Use background mode when starting the dev server; avoid leaving a foreground process running. `dist/` and `.astro/` are generated and git-ignored. There is no test suite, lint script, or configured CI; use `pnpm build` as the available automated check, and manually exercise timing, audio fallback, mobile layout, and reduced-motion changes when relevant. Build success alone does not validate browser behavior.

The two route files contain their own DOM scripts and styles. Before changing routes, components, or styling, use the relevant [Astro documentation](https://docs.astro.build); see the targeted guide links in [AGENTS.md](../AGENTS.md). For asset, host, and deploy assumptions, see [deployment](deployment.md).
