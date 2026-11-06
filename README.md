# Ember — a cinematic scrim skin for Video.js v10

**Ember** re-skins the Video.js v10 player the way the flagship streaming
services do: there is **no control bar and no floating box at all**. An
edge-to-edge cinematic scrim fades in with the chrome and the controls sit
directly on it — title and time at bottom-left, a hero transport cluster
(−10s / play / +10s) dead centre of the frame, captions, settings, PiP and
fullscreen at bottom-right. One crimson accent (`#E50914`) is spent only
where the eye should go: the seek fill, the sphere thumb, the active menu
indicators and the buffering arc. Buttons have no backgrounds — on hover,
the glyph itself grows.

It is painted onto the standard v10 components, so every control, menu,
hotkey and announcement keeps working exactly as the framework intends.

Built for the **Video.js Skins Design Challenge** (Contra × Mux).
Design file: [Ember — Video.js v10 Skin (Figma)](https://www.figma.com/design/sNC6EfwTYauoRLs92zVwbi) — see the "Variation NEW 1 — Ember" page.

## Run it locally

```sh
npm install
npm run dev        # workbench: test sizes, aspect ratios, colour schemes, RTL, languages
npm run typecheck  # tsc --noEmit
npm run build      # production build
```

The workbench plays real video (a 90-second *Big Buck Bunny* clip, hosted
on Mux) — no placeholder media. Change the preview media in
`apps/preview/src/frame/player`.

## The design system

- **Scrims, not surfaces** — the bottom scrim is a full-width fade
  (`linear-gradient(transparent → rgba(0,0,0,.88))`, ~168px) with a
  matching top fade for the corner actions. It fades in with the chrome
  over ~250ms and never shifts layout. The generic control background
  token is retired to `transparent`; the only true surfaces left are the
  menus, popovers and the error dialog (`#181818` at 96%, 8px radius).
- **Centred transport** — the −10s / play / +10s cluster sits at the
  exact centre of the frame: a 76px hero play disc and 54px seek discs
  on a very subtle dark disc (`rgba(0,0,0,.38)`, 1px ring), so the
  transport reads over any footage without a panel behind it. When the
  video ends, the replay disc earns a crimson ring.
- **The crimson line** — the seek bar is a full-width 4px line (8px
  while hovered, focused or dragged): fill `#E50914`, buffered
  `rgba(255,255,255,.35)`, track `rgba(255,255,255,.25)`, and an 18px
  crimson sphere for a thumb that scales in from 0 on engagement (and
  simply stays put on touch devices).
- **Type:** *Inter* throughout — title 15px/600, time 14px/500 with
  tabular figures so the clock never jitters; secondary text at 70%
  white. Spacing follows the framework's 4px rhythm.
- **Icons:** 24 calm glyphs on a 24×24 grid in `src/video/icons.ts` —
  soft filled play/pause and speaker, rounded 2-weight strokes for the
  rest, and a crimson arc for the buffering spinner.
- **Light scheme** — the scrim inverts to a white fade
  (transparent → `rgba(255,255,255,.92)`), glyphs go ink `#141414`,
  and the crimson stays exactly as it is. The skin syncs to the host
  page's `color-scheme` and to the OS preference.

## Signature moments

- **No chrome boxes, ever** — hover feedback is the glyph scaling to
  1.15 over 150ms (`cubic-bezier(.2,0,0,1)`); an open Settings trigger
  turns crimson instead of filling; captions-on is marked by a short
  crimson rule under the glyph.
- **The ±10s recoil** — pressing a seek disc rolls its circular arrow
  ~30° (mirrored for the backward button), a small physical tick.
- **Cinematic error dialog** — a dark card with a short crimson rule
  under its title, over a plain dark backdrop.
- **Captions** ride above the bottom chrome while controls are up, in a
  solid dark chip in both schemes — broadcast convention, always
  readable.

## Accessibility

- Touch targets are **48×48px** (above the 44px floor); the 2px focus
  outline — white on dark, ink on light — is **never removed**, and the
  chrome *and* the scrims stay visible while anything inside the player
  has keyboard focus.
- Works in **light and dark colour schemes**, syncing to the host
  page's `color-scheme` (and the OS preference).
- `prefers-reduced-motion` removes the fades, the glyph scaling and the
  recoil; `prefers-reduced-transparency` / `prefers-contrast: more`
  deepens the scrims and makes popovers solid.
- **Forced-colors** fallbacks: the scrim retires, the stretched top
  zone stays transparent, fills and the captions rule become the system
  Highlight colour.
- The scaffold's hotkeys (`Space`, `M`, `F`, arrow keys), status
  announcer and error dialog are all kept; controls remain in source
  order for keyboard and screen-reader users.

## Responsive behaviour

- **≥40rem:** PiP and fullscreen anchor to the bottom-right corner of
  the frame, closing the bottom row; below that they return to the top
  corner and AirPlay/Cast yield.
- **<30rem:** the title retires, the scrims shorten, the hero disc
  steps down to 64px and the transport stays dead centre.
- **<26rem:** the time readout collapses to the current time, next to
  the seek line.

## Explored directions

Ember is one of the final directions explored for this challenge,
alongside a consolidated frosted-glass skin (Aurora Glass — the glass
family merged into a single entry), an Apple-capsule study, a
Video.js v10 "Frosted" study, a retro pixel-arcade skin and an
editorial cinema skin — all in the same Figma file. Where the glass
directions float a surface *over* the picture, Ember removes the
surface entirely and lets the picture carry the chrome: the opposite
answer to the same brief.

## Project structure

```
src/video/skin.html   – component markup (unchanged from the Scaffold skin)
src/video/skin.ts     – registers the Ember icon set + colour-scheme sync
src/video/skin.css    – the Ember layer: tokens, scrims, centred transport, states, responsive & a11y blocks
src/video/icons.ts    – the 24-icon calm glyph set (24×24 grid)
src/skin.css          – font import (Inter)
apps/preview/         – the Video.js workbench used for testing and the live demo
```

The skin is a paint layer over fully working controls — no behaviour is
forked, which is what keeps every menu, gesture and keyboard path intact.

## How it was built

Designed first in Figma (tokens, desktop and mobile players, states),
then implemented with an AI coding agent against the version-matched
Video.js v10.3.0 docs: scaffold project, custom icon set, CSS layer,
then a fidelity pass comparing the running preview against the Figma
frames — followed by checks at desktop and mobile widths, both colour
schemes, keyboard-only navigation, reduced motion and forced colours.

## License

Submitted under the challenge terms: Apache License 2.0.

## Credits

Designed & built by **Haseeb P.** — CEO, The Hitek Agency (Houston, USA).
