# Architecture

This is a static, two-route Halloween prop built with Astro. `astro.config.mjs` uses Astro's default static output; there is no server-side application, API, database, framework island, or persistent session store.

| Source | Route | Responsibility |
| --- | --- | --- |
| `src/pages/index.astro` | `/` | Fictional personnel dossier, live local clock, simulated last-seen/access times, security monitor and access warning, verification entry point. |
| `src/pages/verify.astro` | `/verify` | Timed mock gateway, fake access grant, click-to-reveal Rickroll and browser-only audit trail. |
| `public/` | Static asset URLs | QR SVG, favicon, GIF, MP3 and reduced-motion still image. |

Each page contains its own markup, browser script, and scoped CSS. The homepage uses `/verify` for clickable links; the static QR SVG encodes `https://id.cattoindustries.com/verify`, so moving domains requires regenerating the SVG. On screens at most 600px wide, the verification panel appears ahead of the dossier and the QR/scan copy is hidden.

The homepage sets `Last Seen` to a random time 15–25 minutes before page load; its separate live clock refreshes each second. The security monitor starts hidden. Once at least half of the `PRESUMED DECEASED` status block enters the viewport, an `IntersectionObserver` starts a random 1–3 second delay. Leaving the block before the delay ends cancels it; returning starts a fresh delay. The monitor appears only while the block is still in view, resets `Last Seen` to that moment, and fires at most once per page load. It does not appear solely because time passed before the status was viewed. The monitor's `Last Access` displays the same time. Only at that update, `Last Seen` turns red and gains a flashing red beacon (static under reduced motion); it is not highlighted before the alert. Both timestamps then remain fixed for the visit (reopening the monitor does not refresh them). The access warning appears immediately. Once visible, each popup auto-dismisses after five seconds (250 ms exit animation unless reduced motion is requested) and can be reopened.

On `/verify`, JavaScript advances mock hash and credential steps after 1.1, 1.35, and 1.1 seconds (~3.55 seconds total). The user then clicks **View Verification Hash** to reveal the unauthorized-access scene. The MP3 is played inside that click handler; browsers may still block playback, so audio controls and a fallback button remain. The GIF is replaced visually by `rickroll-still.png` under reduced motion. A session ID and audit entries are created in the browser using its clock and appended to the DOM; they are not submitted or persisted by site code. See [security](security.md) for the trust boundary and [decisions](decisions.md) for evidenced choices.
