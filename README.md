# GraphTrace

Trace an image into [Desmos](https://www.desmos.com/calculator) equations using a small, deliberate set of algebra forms. Upload a picture, drop it onto a coordinate plane, click points, and GraphTrace fits the curve and gives you paste-ready Desmos equations (with domain restrictions so segments stay bounded).

Single file, no dependencies, no build step. Just open `index.html`.

## Forms

| Tool | Equation | Clicks |
|---|---|---|
| Slope-intercept | `y = mx + b` | 2 points on the line |
| Standard *(parabola)* | `y = ax² + bx + c` | 3 points on the parabola |
| Vertex *(parabola)* | `y = a(x−h)² + k` | vertex, then 1 point |
| Intercept *(parabola)* | `y = a(x−p)(x−q)` | 2 x-intercepts, then a through-point |
| Inverse | `y = a/(x−h) + k` | 3 points on one branch |
| Circle | `(x−h)² + (y−k)² = r²` | center, then a point on the edge |

## Using it

1. Open `index.html` in a browser (or serve it: `python3 -m http.server 5370`).
2. Upload / drag / paste an image. Adjust its opacity and size; use **Move image** to reposition.
3. Pick a form, click the points it asks for. The fitted curve draws live and appears in the panel.
4. Copy one equation, or **Copy all for Desmos** — paste the block into Desmos and each line becomes its own expression.

## Shortcuts

`1`–`6` select tools · `V` pan · `M` move image · `U` undo · `Esc` cancel · wheel = zoom · right-drag = pan.

## Notes

The function forms all pass the vertical-line test, so they trace outlines, arcs, and swooshes one equation at a time; build a closed shape from several segments. Circles are the one closed implicit form, plotted whole.
