# Implemented choices and evidence

These are implementation facts, not a claim to know every author's intent. Available Git history contains an initial site commit and subsequent monitor-time and verification-page refinements; it does not establish all rejected alternatives.

- **Static QR and relative navigation:** `public/verification-qr.svg` points at `https://id.cattoindustries.com/verify`, while homepage anchors use `/verify`. This enables links to work locally without making the QR domain-relative; the SVG needs regeneration on a domain change. No evidence of a runtime QR dependency.
- **Browser-local theatrical timing:** commit `4da3588` made monitor `Last Access` agree with the dossier's `Last Seen`; current homepage code shares the same calculated timestamp. The subsequent verify-page commits `f985428` and `9f097ca` added/refined the fake access sequence and audit presentation. The audit is not a security log.
- **Reveal media and user-initiated audio:** `README.md` records local Giphy GIF and Myinstants MP3 sources, with unverified rights. `verify.astro` plays audio directly from the hash-button click and retains fallback controls; this is compatible with many browsers' gesture restrictions but cannot guarantee playback. A still frame accommodates reduced motion. The earlier conversation mentions an embed problem, but available commit history does not prove its cause, so no specific rejected embed technology is recorded here.
- **Fiction vs. realism:** the UI presents a mock security incident but includes joke/fiction disclosures. Avoid treating cinematic warnings, generated session IDs, or browser clock values as actual telemetry or legal evidence.

If future changes introduce a meaningful cross-cutting architectural choice, record the evidence, rationale, tradeoffs, and remaining limitations here (or split into focused decision files if this grows). Do not reverse-engineer motivations from code without marking them as inference.
