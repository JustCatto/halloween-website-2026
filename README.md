# Catto Industries — Halloween ID Verification

This website was 100% vibecoded. It is a fictional Halloween prop: a classified-looking Catto Industries personnel file that turns a credential check into a Rickroll.

The story follows Rick A., a Level 7 personnel record marked **Presumed Deceased** with a warning that the subject may be infected. A floating security monitor reports an impossible sighting. Visitors can dismiss and reopen the alert, inspect the dossier, and scan the QR code or click the verification button. The `/verify` page stages a fake hash submission and credential check, then grants access to a “View Verification Hash” button. Opening it flags the session as unauthorised access, dispatches fictional security personnel, and reveals the GIF, audio, and a simulated session audit trail.

**This is not a real ID, government service, security system, or verification process.** No hash is submitted and no credentials are checked.

## Built with

- Astro 7 and plain CSS/JavaScript; no frontend framework or QR runtime dependency.
- A static SVG QR code that points to `https://id.cattoindustries.com/verify`.
- Locally hosted GIF and MP3 assets for the reveal page.
- A Cloudflare Workers static-assets configuration in `wrangler.jsonc`.

The homepage clock uses the visitor's local time. “Last Seen” is simulated as 2–6 minutes before the current time, with a random offset chosen on each page load. The status alert and verification sequence are also just theatrical UI. The reveal page generates a temporary session ID and timestamps events using the visitor's device clock. These entries are not sent to a server, retained, authenticated, or suitable as legal evidence.

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
| `public/verification-qr.svg` | QR code for the deployed `/verify` URL. |
| `public/rickroll.gif`, `public/rickroll.mp3` | Locally served reveal media. |
| `public/rickroll-still.png` | Still frame shown instead of the GIF for reduced-motion visitors. |

If the site moves to a different domain, regenerate `public/verification-qr.svg` with the new **absolute** `/verify` URL. The on-page links use the relative `/verify` path and do not need changing. With `qrencode` installed, for example:

```sh
qrencode -t SVG -l M -m 2 -s 7 -o public/verification-qr.svg 'https://example.com/verify'
```

## Media and autoplay

The GIF was downloaded from [Giphy](https://media.giphy.com/media/Ju7l5y9osyymQ/giphy.gif), and the roughly 17-second audio clip from [Myinstants](https://www.myinstants.com/media/sounds/rick-roll.mp3). Their usage rights have **not** been verified; check licensing and permissions before publishing or distributing the site.

The reveal page calls `audio.play()` directly from the **View Verification Hash** click, which gives browsers a user gesture and makes sound playback more likely. It also provides audio controls and a **Tap to play audio** fallback if playback is blocked. No implementation can guarantee unmuted playback on every device.
