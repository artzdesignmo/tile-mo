# Tile Mo — Seamless Pattern Studio

A single-file web app for designing seamless repeating patterns. Draw motifs
in one tile, watch them wrap across edges, and preview the live tiling next
to the editor. Built with [Paper.js](http://paperjs.org/) (0.12.18).

No build step. Open `index.html` in a browser, or host it on any static host
(such as GitHub Pages). An internet connection is needed for the Paper.js CDN
and the Google Fonts; if Paper.js fails to load, the page shows an error
banner instead of a blank canvas.

## Features

- **Seamless tiling with wrap-around.** Any shape crossing a tile edge is
  duplicated on the opposite edge. The live preview tiles the editor tile
  with straight, half-drop, brick, or mirror repeat.
- **Symmetry.** Left-right mirror, up-down mirror, four-way mirror, and a
  3–12 petal kaleidoscope (mirrored wedges).
- **Deformation.** Twist, wave, swirl, and stretch sliders applied to the
  whole motif.
- **Motif library.** Dot, diamond, star, ring, triangle, hexagon, leaf,
  heart, moon, cross, flower. Per-element colour, size, angle, and count
  editing; elements are draggable on the canvas.
- **Hand pen.** Draw free paths on the canvas, then `Smooth` (Paper.js
  `smooth()`) or `Simplify` (Paper.js `simplify()`).
- **Boolean ops.** Unite, subtract, intersect (Paper.js native) on two
  selected shapes or paths.
- **Symbols.** Define a motif once, place many instances; editing the
  definition updates every instance.
- **SVG upload.** Import an SVG file as a motif via Paper.js `importSVG`.
- **JSON save / load / share.** Save the pattern as JSON, reload it, or copy
  a share link (pattern encoded in the URL hash, loaded automatically).
- **Gradients, blends, shadows.** Gradient fill, multiply / screen / overlay
  blend modes, drop shadow.
- **Image tools.** Upload an image, extract a 5-colour palette from it, or
  place the image itself as a motif (Paper.js `Raster`).
- **Batch variants + seed.** Seeded randomisation; generate 4 variant tiles
  and tap one to apply it.
- **Animated preview.** Paper.js `onFrame` rotate / breathe on the editor
  canvas, with the tiled preview following.
- **Export.** SVG via `project.exportSVG` (true vector, editable in
  Illustrator), PNG tile, 2048px HD PNG, and batch PNG export across all
  4 palettes.

## Free vs Pro

Free (about 20%): straight repeat + 3×3 preview + tile size slider;
left-right mirror only; dot, diamond, star motifs only; palette 1 only;
standard PNG + SVG single-tile export; basic per-element editing
(move, size, angle, count, palette-1 colours).

Pro (everything else): half-drop, brick, mirror repeat; 5×5 preview;
up-down and four-way mirror; kaleidoscope; all deform sliders; the rest of
the motif library; hand pen + smoothing; boolean ops; Symbol linkage; SVG
upload; JSON save/share; gradients / blends / shadows; image extraction +
image motif; batch variants + seed; animated preview; 2048px HD + batch
multi-palette export.

Locked controls show a Pro state; clicking one opens the Pro dialog.
A valid license key unlocks Pro and is remembered in `localStorage`
(`tilemo_pro`) on that browser only.

## Pro checkout — TEST wiring (temporary)

The store is awaiting Lemon Squeezy approval, so the app currently wires
**TEST checkout links**, clearly labelled as test purchases in the Pro
dialog (no real money is charged):

- Monthly (test): `https://openx.lemonsqueezy.com/checkout/buy/2301559`
- Lifetime (test): `https://openx.lemonsqueezy.com/checkout/buy/2301570`

License keys validate client-side via the Lemon Squeezy License API:

```
POST https://api.lemonsqueezy.com/v1/licenses/validate
Body: { "license_key": "<key>", "instance_name": "tile-mo" }
```

Only an explicit `valid: true` response unlocks Pro. Network errors, CORS
failures, and invalid keys show an honest error and never grant access.
No API key, secret, or credential is stored in this file — the two variant
IDs above are public buy-link IDs.

### Going live (2-line change)

When the store is approved, replace only the two checkout URLs in the
`CONFIG` block at the top of the script in `index.html` with the live
variant buy links, and re-verify with a live-mode API key. Nothing else
needs to change. Do not present the test links as production checkout.

## Design

- Titles in Dela Gothic One (Noto Sans TC fallback for Chinese).
- Default language English, top-right EN / 繁中 toggle (persisted).
- Default light silver-gray theme; top-bar icon cycles white / light
  silver-gray / black (persisted in `localStorage`).
- All icons 2D monochrome silver-gray (`#8a867e`).
- Small top-right Buy Me a Coffee icon links to
  https://buymeacoffee.com/whynotartmoney
- Controls in a side panel, canvas as hero. Sliders and touch drawing work
  on iPhone (`touch-action: none` on canvases).
- All sample content is generic and fictional.

## Known limits (need real-browser checking)

- Visual rendering, touch drawing, and the actual Lemon Squeezy test
  purchase + license validation flow have not been run in a real browser
  yet — syntax and logic were verified, but a live pass is still needed.
- SVG export with image motifs waits briefly for rasters to load; very
  large images may still export before loading completes.
- Share links with image motifs embed the image data URL and can exceed
  URL length limits; prefer JSON save for image-heavy patterns.
- Batch export downloads 4 files in sequence; the browser may ask
  permission for multiple downloads.
- Gradient + HD export combination is untested in a real browser.

## License

MIT — see `LICENSE`.
