# PDF or image to a clean DWG: my checklist

## 1. Check what you have
- Vector PDF (lines select individually) or scanned/raster (one picture)?
- Is there a scale bar or at least two long dimensions you can trust?
- Sheet size and stated scale (e.g. 1:100 @ A1). A PDF printed "to fit" no longer matches its scale.

## 2. Bring it in
- **Vector PDF**: `PDFIMPORT` (AutoCAD and BricsCAD). Turn on importing as objects and keep layers if the PDF has them.
- **AutoCAD**: `PDFSHXTEXT` turns imported SHX text back into editable text.
- **Raster / scan**: `IMAGEATTACH`, then trace. Never deliver a traced-over image as "CAD".

## 3. Scale it correctly
`SCALE` → select all → base point → **R** (Reference) → pick both ends of a long known dimension → type its real length. Check with a second dimension in the other direction. If they disagree, the PDF is distorted, so note it and ask.

## 4. Redraw cleanly
- Walls, doors and windows on their own layers (A-WALL, A-DOOR, A-GLAZ ...), not everything on "0".
- Real polylines with correct thicknesses, no broken segments. `OVERKILL` removes duplicates.
- Doors and windows as blocks, so they can be counted.
- Dimensions in a proper dimension style, text in a standard style.

## 5. Clean and deliver
- `PURGE`, `AUDIT`, zoom extents, model space at 1:1.
- A layout sheet with title block if the client wants a printable PDF.
- Save down to the version the client uses (e.g. AutoCAD 2018 DWG).
- List anything that was unclear or estimated.

## Worked example
An old blue-line plan, scanned at an angle, redrawn as a layered DWG with door and window blocks and true dimensions: [scan to clean DWG](https://github.com/Grishutov/takeoff-samples#4-scanned-plan-to-a-clean-dwg).
