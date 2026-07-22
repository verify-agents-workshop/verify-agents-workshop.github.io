# Website Design Explorations

A private gallery of website designs I liked but didn't ship — kept here for future
projects. Each design is a single self-contained `index.html` (inline CSS, Google Fonts,
no build step): open it in a browser, or serve the folder with
`python3 -m http.server`.

Origin: design exploration for the *Who Verifies the Agents?* NeurIPS 2026 workshop
site (July 2026). The content in each mockup is that workshop's, but every design is
easy to retheme — swap the text and the `:root` color variables.

## The designs

| Folder | Design | One-liner |
| --- | --- | --- |
| `broadsheet/` | **Broadsheet** | The page as a newspaper front page: masthead, dateline rule, multi-column justified lead story with drop caps, agate dates sidebar, boxed "public notice" CFP. Pure typography, zero illustration. Fonts: Playfair Display + EB Garamond. |
| `blueprint/` | **Blueprint** | A cyanotype engineering drawing: graph-grid background, drafted schematic with dimension lines and dashed leaders, numbered sheets, and a real engineering title block (project / sheet / scale / drawn by). Fonts: IBM Plex Mono + Inter. |
| `gallery/` | **Exhibition** | A museum at night: near-black walls, spotlight gradients, content as brass-framed line artworks with museum placards (exhibit no., title, medium), dates as "Visitor Information". Fonts: Cormorant Garamond + Inter. |
| `pastel-watercolor/` | **Watercolor Pastel** | Soft lilac/blush/sky watercolor washes with hand-painted edges, brush-stroke underlines, and pigment-blob icons — all pure SVG (turbulence + displacement filters), no image assets. Fonts: Cormorant Garamond + Inter. |

## Notes

- Each page has a small "Design Preview" bar at the top left over from the original
  staging site; its links point at that site's `/dev/` paths and can be deleted along
  with the `.variant-bar` CSS block.
- The watercolor/pencil texture technique (SVG `feTurbulence` + `feDisplacementMap`
  filters) in `pastel-watercolor/` is reusable for any hand-made look: painted washes,
  brush strokes, rough stamps, pencil lines.
