# ahl-tea-html5

Static-HTML port of `ahl-tea-tap-appscript`. Same UI, same dynamic NETS QR
reconstruction, but served as a top-level page so custom URL schemes
(`paylah://`) and `<a download>` work without the Apps Script iframe
sandbox in the way.

## Files

- `index.html` — self-contained. Inlines `qrcode-lib` (qrcodejs), `jsQR`
  loads from CDN, NETS template is hardcoded near the top of the main
  `<script>` block (`window.BAKED_NETS_QR`).

## Updating the shop QR

Open `index.html`, find `window.BAKED_NETS_QR` (~line 950) and replace
the string. That's the raw EMV/SGQR payload extracted from the shop's
sticker by `ahl-tea-tap-appscript` (use the "Copy NETS config" button in
the Apps Script version's Settings to grab a fresh one).

## Modes

- Default: `LOCKED_MODE` — Settings gear hidden, baked NETS used.
- `?config=1` — Settings gear visible, localStorage overrides allowed.

## Hosting

Any static host. No build step, no server. Examples:

- GitHub Pages — drop `index.html` in a repo, enable Pages.
- Cloudflare Pages / Netlify — point at a repo.
- Drop into an existing static site (e.g. `paynow.sankhacooray.com`).

## Source of truth

The Apps Script project (`ahl-tea-tap-appscript`) is no longer the
canonical build. Edits live here directly. If you rebuild from the Apps
Script source, use `/tmp/build_ahl_tea_html5.py` as a starting point —
it does the scriptlet substitutions in one pass.
