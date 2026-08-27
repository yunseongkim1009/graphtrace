# GraphTrace

Turn an image into [Desmos](https://www.desmos.com/calculator) equations. Upload a picture, drop it onto a coordinate plane, and either **auto-trace** it in one click or place points by hand. GraphTrace fits the curves and gives you paste-ready Desmos (with domain restrictions so segments stay bounded).

Single file, no dependencies, no build step. Just open `index.html`.

## Auto-trace

Hit **✨ Auto-trace** and GraphTrace reads the image itself. The pipeline: threshold the ink → **skeletonize** it to 1px centerlines (Zhang–Suen thinning) → **trace** each stroke as an ordered path → simplify (Ramer–Douglas–Peucker) → split each path at its turning points into function-of-x pieces → least-squares-fit each piece as a line, parabola, or cubic. Round closed loops are recognised as **circles/ellipses**, and near-vertical strokes become `x = c` lines.

Because it follows the actual strokes (not columns), it handles multi-stroke drawings, curves that double back, and closed shapes. Tune it with the **Ink threshold** slider (what counts as ink), the **Detail** slider (faithful vs. smooth), and the **Light drawing on dark** toggle. Position the image where you want it first, then trace.

## Forms (manual tools)

| Tool | Equation | Clicks |
|---|---|---|
| Slope-intercept | `y = mx + b` | 2 points on the line |
| Standard *(parabola)* | `y = ax² + bx + c` | 3 points on the parabola |
| Vertex *(parabola)* | `y = a(x−h)² + k` | vertex, then 1 point |
| Intercept *(parabola)* | `y = a(x−p)(x−q)` | 2 x-intercepts, then a through-point |
| Inverse | `y = a/(x−h) + k` | 3 points on one branch |
| Circle | `(x−h)² + (y−k)² = r²` | center, then a point on the edge |
| Cubic | `y = ax³ + bx² + cx + d` | 4 points along the curve |
| Absolute value | `y = a\|x−h\| + k` | corner, then a point on an arm |
| Square root | `y = a√(x−h) + k` | start point, then a point to the right |
| Ellipse | `(x−h)²/a² + (y−k)²/b² = 1` | center, then a corner |

## Using it

1. Open `index.html` in a browser (or serve it: `python3 -m http.server 5370`).
2. Upload / drag / paste an image. Adjust its opacity and size; use **Move image** to reposition.
3. **Auto-trace**, or pick a form and click the points it asks for. Fitted curves draw live and appear in the panel.
4. Copy one equation, or **Copy all for Desmos** — paste the block into Desmos and each line becomes its own expression.

## Shortcuts

`1`–`0` select tools · `V` pan · `M` move image · `U` undo · `Esc` cancel · wheel = zoom · right-drag = pan.

## Notes

The function forms all pass the vertical-line test, so they trace outlines, arcs, and swooshes one equation at a time; build a closed shape from several segments. Circles and ellipses are the closed implicit forms, plotted whole. Domain restrictions are copied as Desmos LaTeX (`\left\{…\right\}`) so they paste correctly.
