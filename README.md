# Catto Industries — Halloween ID Verification

This website was 100% vibecoded. It is a fictional Halloween prop: a classified-looking Catto Industries personnel file that turns a credential check into a Rickroll.

The story follows RICK [REDACTED], a Level 7 personnel record marked **Presumed Deceased** with a warning that the subject may be infected. A security monitor reports an impossible sighting. Visitors can dismiss and reopen the alert, inspect the dossier, and scan the QR code on larger screens or click the verification button (the QR is hidden on mobile). The `/verify` page stages a fake hash submission and credential check, then grants access to a “View Verification Hash” button. Opening it flags the session as unauthorised access, dispatches fictional security personnel, and reveals the GIF, audio, and a simulated session audit trail.

**This is not a real ID, government service, security system, or verification process.** No hash is submitted and no credentials are checked.

## Built with

- Astro 7 and plain CSS/JavaScript; no frontend framework or QR runtime dependency.
- A static SVG QR code that points to `https://id.cattoindustries.com/verify`.
- Locally hosted GIF and MP3 assets for the reveal page.
- A Cloudflare Workers static-assets configuration in `wrangler.jsonc`.

For agent orientation and implementation details, start with [AGENTS.md](AGENTS.md) and the [architecture](docs/architecture.md), [development](docs/development.md), [deployment](docs/deployment.md), [security](docs/security.md), [conventions](docs/conventions.md), and [decisions](docs/decisions.md) notes.

The homepage clock uses the visitor's local time. “Last Seen” initially shows a simulated time 15–25 minutes before page load; after the visitor scrolls and the `PRESUMED DECEASED` status stays in view for a random 1–3 seconds, when the security monitor appears (once per page load), “Last Seen” and its matching “Last Access” update to that moment and stay fixed. Scrolling away before the delay ends cancels it; returning starts a fresh countdown. The updated “Last Seen” turns red and gains a flashing beacon (static with reduced motion). The alert and verification sequence are theatrical UI. The access warning appears immediately; each popup auto-dismisses five seconds after it appears and can be reopened. The reveal page generates a temporary session ID and timestamps events using the visitor's device clock. These entries are not sent to a server, retained, authenticated, or suitable as legal evidence.

## Run locally

Requires Node.js **22.23.4+** and pnpm.

```sh
pnpm install
pnpm astro dev --background
```

Use `pnpm astro dev status`, `pnpm astro dev logs`, and `pnpm astro dev stop` to manage the background server. Build the static site with `pnpm build`; the output goes to `dist/`.

## Routes and assets

| Path | Purpose |
| --- | --- |
| `/` | Fictional personnel dossier, security alert, QR code, and verification link. |
| `/verify` | Staged access grant, verification hash button, and Rickroll security-alert reveal. |
| `public/catto-industries-mark.svg` | Unframed C/ears/I mark used as a color-matched mask inside the homepage header's existing hexagon. |
| `public/favicon.svg`, `public/favicon.ico` | Self-contained version of the new mark with its hexagon; SVG and multi-size ICO fallback. |
| `public/verification-qr.svg` | QR code for the deployed `/verify` URL. |
| `public/rickroll.gif`, `public/rickroll.mp3` | Locally served reveal media. |
| `public/rickroll-still.png` | Still frame shown instead of the GIF for reduced-motion visitors. |

The header mark takes its color from `.brand-mark { color: ... }` in `src/pages/index.astro`. The standalone SVG defaults to mint; when inlined in markup, set `--mark-color` on the SVG or an ancestor to recolor it. An SVG loaded via `<img>` or `<image>` does not inherit the page's CSS variables. The favicons embed a copy of the mark so they can render independently: after changing its shape, update `public/favicon.svg` too. With ImageMagick installed, regenerate the ICO with `magick -background none -density 384 public/favicon.svg -resize 256x256 -define icon:auto-resize=64,48,32,16 public/favicon.ico`.

If the site moves to a different domain, regenerate `public/verification-qr.svg` with the new **absolute** `/verify` URL. The on-page links use the relative `/verify` path and do not need changing. With `qrencode` installed, for example:

```sh
qrencode -t SVG -l M -m 2 -s 7 -o public/verification-qr.svg 'https://example.com/verify'
```

## Media and autoplay

The GIF was downloaded from [Giphy](https://media.giphy.com/media/Ju7l5y9osyymQ/giphy.gif), and the roughly 17-second audio clip from [Myinstants](https://www.myinstants.com/media/sounds/rick-roll.mp3). Their usage rights have **not** been verified; check licensing and permissions before publishing or distributing the site.

The reveal page calls `audio.play()` directly from the **View Verification Hash** click, which gives browsers a user gesture and makes sound playback more likely. It also provides audio controls and a **Tap to play audio** fallback if playback is blocked. No implementation can guarantee unmuted playback on every device.
