# Slot Machine — Public Web Demo

Browser build of a Godot 4 portfolio slot prototype. Spin a seeded 5×3 game, inspect the audit JSON for each round, and run a chunked Monte Carlo RTP check without freezing the page.

> **Live demo:** [https://somnitis.github.io/slot-machine-demo/SlotMachine.html](https://somnitis.github.io/slot-machine-demo/SlotMachine.html)  
> Enable **Settings → Pages → Deploy from branch `main` / root** on this repo if that link 404s.

This repository is **export-only** (HTML / JS / WASM / PCK). The Godot project source stays in a separate private repo.

## What you can try

- **SPIN** — next integer seed; result is fully determined by bet + seed  
- **Replay Seed** — re-run the seed in the field  
- **Round Details** — pretty audit JSON (stops, grid, lines, Hold & Win steps)  
- **Verify Replay** — re-evaluate the audit through the same math core  
- **RTP Simulator** — 10k–1M spins in small frame budgets (web-safe); exact config RTP is **96.8274%**

## Tech

| Piece | Detail |
|--------|--------|
| Engine | Godot **4.7**, **GL Compatibility** (web-friendly) |
| Math | Headless `RefCounted` core — no UI in the payout path |
| Rounds | Optional `seed`; same seed → same stops, grid, wins |
| Export | Official Godot Web export (`SlotMachine.html` + `.pck` + `.wasm`) |

## Embed (Wix / any site)

Use an iframe pointed at the Pages URL. Example:

```html
<iframe
  src="https://somnitis.github.io/slot-machine-demo/SlotMachine.html"
  width="960"
  height="640"
  style="border:0;max-width:100%;"
  allow="autoplay; fullscreen"
  loading="lazy"
  title="Slot Machine Demo">
</iframe>
```

On Wix: **Embed → Embed a site / iframe**, paste that URL (or the full iframe). Prefer HTTPS. Some hosts need cross-origin isolation headers for threads; this build targets the default single-threaded Godot web export.

## Local preview

Serve the folder over HTTP (browsers block `file://` WASM loads):

```bash
# from this repo root
python -m http.server 8080
```

Open [http://localhost:8080/SlotMachine.html](http://localhost:8080/SlotMachine.html).

## Updating the build

1. Export Web from the private Godot project (templates for 4.7, GL Compatibility).  
2. Replace the `SlotMachine.*` files in this repo (keep `README.md`).  
3. Push to `main`. Pages refreshes in a minute or two.

Optional: copy or rename `SlotMachine.html` → `index.html` so the Pages root URL loads the game without the filename.

## Disclaimer

Demo / portfolio only. Not a real-money product, not licensed for gambling, and not a claim of regulatory certification.
