# Images

The five `gbe-*.png` files are **grey placeholders**. Replace each with a real
screenshot at the same path and filename — no HTML changes are needed.

Shoot at the listed size (or any image with the same aspect ratio) and they will
double as your Chrome Web Store listing images, which want 1280×800.

| File | Size | What to capture |
|---|---|---|
| `gbe-hero.png` | 1280×800 | Gmail inbox, several emails selected, toolbar visible. The main shot — used on both the home and product pages. |
| `gbe-toolbar.png` | 1280×520 | Close-up of the toolbar: PDF, Attachments, ZIP, Merge, with the Pro lock/star badge clearly visible. |
| `gbe-popup.png` | 1000×820 | The extension popup showing plan, trial state and weekly usage. |
| `gbe-merged.png` | 1280×800 | Result shot — a merged PDF open in Chrome's PDF viewer (or the Downloads folder of exported files). |
| `gbe-naming.png` | 1000×820 | *Optional, currently unused.* Pro naming-template settings in the popup. |

Use a demo account or blur real names and addresses — these are public.

## Generated assets (do not hand-edit)

| File | Source | Regenerate with |
|---|---|---|
| `og-image.png` | `og-source.html` | see below |
| `apple-touch-icon.png` | `logo.svg` | see below |
| `logo.svg` | — | the master brand mark; hand-edited |
| `gbe-icon.png` | copied from the extension repo `public/icons/icon128.png` | re-copy if the icon changes |

```sh
CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"

# social preview (1200×630)
"$CHROME" --headless --disable-gpu --hide-scrollbars --force-device-scale-factor=1 \
  --screenshot=og-image.png --window-size=1200,630 "file://$PWD/og-source.html"
```
