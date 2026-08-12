Aspect-ratio wrapper for the Carlinkit T2C CarPlay adapter in the Tesla browser — fixes the cropped right edge


# tespush-fit

A one-file static wrapper that fixes the cropped display of the
Carlinkit T2C CarPlay adapter (`tespush.com`) in the Tesla browser.

## Problem

The T2C interface lays out wider than the Tesla browser's viewport,
so roughly the right third of the screen is cut off with no way to
scroll or zoom to it.

## How it works

`index.html` loads `tespush.com` in an iframe sized to the source's
native resolution (1920×1080), then applies independent X and Y CSS
transforms to squash that box onto the Tesla viewport. Nothing is
cropped; the full interface is visible.

The wrapper never touches the video path — frames still stream over
the adapter's local Wi-Fi. It only controls the frame's geometry.

## Usage

Open the published Pages URL in the Tesla browser and bookmark it,
instead of navigating to `tespush.com` directly.

## Tuning

Two constants at the top of the script:

- `SOURCE_W` / `SOURCE_H` — layout size given to the inner page.
  If an edge is still cut off, raise `SOURCE_W`.

To preserve exact geometry with letterbox bars instead of a slight
vertical stretch, change both scale factors to `Math.min(sx, sy)`.

## Notes

- Requires internet in the car to fetch this page (the CarPlay stream
  itself stays local). Bookmarking as a `data:` URL avoids that.
- Unofficial workaround, not affiliated with Carlinkit. A firmware-side
  viewport fix would make this unnecessary.
