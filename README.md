# Tachyon — Beyond Space (v2.0)

A dark-only, cinematic House Points Calculator for the Tachyon House Cup. Four houses, live rankings, a WebGL black-hole hero, layered liquid-glass panels and optional synthesized sound. No framework, no backend, no paid API.

"4D/5D" in the design language describes a visual illusion built from perspective, parallax, layered glow and shader lensing. It is not a literal extra dimension.

## Features

**Scoring**
- Houses: ALPHA (violet), INFER (green), MATRIX (cyan), LAYER (amber).
- Validated entry: rejects empty, negative, decimal, non-numeric, unsafe-integer and overflow values, and invalid house values, each with a specific message.
- Competition ranking for ties (1, 1, 3, 4). Tied leaders are shown together; an all-zero board shows `NO WINNER YET`.
- Leader, tied and selected states are communicated with text and icons, not colour alone.
- Activity log (latest 8 shown, 100 stored), with independent "Clear history" and a full reset, both behind confirmation dialogs.
- Celebration (toast, restrained confetti, scene pulse, optional sound) fires only when the *sole leader changes identity* — not on unrelated re-renders, ties, or reloads.

**Visual / motion**
- Three glass tiers (panels, cards, rows) from shared CSS design tokens; backdrop blur only on large surfaces.
- House cards: lift, pointer-driven tilt, cursor-following specular highlight, house-coloured glow, inner depth shift.
- Buttons: light sweep, glow, icon nudge, press feedback. Ranking rows animate to new positions (FLIP) and the row that moved up is highlighted.
- WebGL hero: point-lens gravitational lensing of a three-layer star field and nebula, tilted accretion disk with Doppler brightening, lensed arcs, photon ring, dust, parallax. Resolution adapts to performance; the loop pauses off-screen and in background tabs.
- Falls back to a CSS scene without WebGL or after context loss, and recovers if the context is restored.
- `prefers-reduced-motion`: static shader frame, no tilt, no confetti, no count-up, entrance animations disabled.

**Accessibility**
- Semantic landmarks, skip link, labelled form, `aria-invalid` and live-region messages, visible focus rings.
- House cards are real `<button>`s with `aria-pressed`.
- Modal: initial focus on Cancel, focus trap, Escape to dismiss, background `inert`, focus returns to the trigger.
- Hover effects only under `(hover: hover) and (pointer: fine)`; touch gets press feedback and nothing depends on hover.

**Data**
- Same storage keys as earlier versions, so existing scores carry over: `tachyon-house-points-v1` (scores + history) and `tachyon-house-points-sound-v1`.
- Missing or partly invalid history no longer discards valid scores. Unreadable data is copied to `tachyon-house-points-v1-corrupt-backup` before anything is overwritten.
- Other tabs' changes are picked up via the `storage` event.

## Project structure

```text
Tachyon_Beyond_Space/
├── index.html
├── style.css
├── script.js
├── README.md
└── screenshots/
    ├── README.txt
    └── *.png
```

## Run locally

Open `index.html` in a current Chrome, Edge, Firefox or Safari. Alternatively serve the folder (for example `python3 -m http.server` or VS Code Live Server) and open the printed address. Google Fonts load from the network; without it the fallback fonts are used.

## Deploy to GitHub Pages

1. Create a repository and put the contents of this folder at its root (so `index.html` is at the top level).
2. Commit and push to `main`.
3. In the repository, open **Settings → Pages**, set **Source** to *Deploy from a branch*, choose `main` and `/ (root)`, and save.
4. After a minute or two the site is live at `https://<your-username>.github.io/<repository>/`.

All asset paths are relative, so it also works from a sub-path.

## Browser compatibility

Built for current evergreen browsers. It uses CSS `color-mix()`, container query units, `backdrop-filter`, the Web Animations API, `inert` and WebGL 1. Without `backdrop-filter` panels use a solid dark fill; without WebGL the CSS scene is shown. Older browsers lacking `color-mix()` or container units will lose some accent tinting and fluid score sizing.

## Known limitations

- Scores live in each browser's `localStorage`: they are per device and per browser profile, with no sync.
- Zero-point submissions are accepted (preserved from v1) and appear in the log as `+0 PTS`.
- The WebGL scene was visually checked only with software rendering; real GPU smoothness and mobile thermal behaviour were not measured.
- Audio was only checked for when the audio context is created; actual sound output was not auditioned.
- Date and time in the log use the browser's locale; entries saved by v1 keep their original text.
- Safari and Firefox were not tested (Chromium only).
