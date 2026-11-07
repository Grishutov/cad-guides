# Georeferencing a DWG (BricsCAD / AutoCAD)

How to put a drawing that sits at "0,0" onto real-world coordinates and tag it with its coordinate reference system (CRS). Example CRS: **EPSG:31255, MGI / Austria GK Central**. The method is the same for any projected CRS.

Two separate things happen, and people often mix them up:

| Step | What it does | Command |
| --- | --- | --- |
| **Move the geometry** | Moves, rotates (and if needed scales) the drawing so its points sit on their real coordinates | `ALIGN` (or `MOVE` + `ROTATE`) |
| **Tag the CRS** | Writes into the DWG which coordinate system those numbers belong to | `GEOGRAPHICLOCATION` |

Tagging alone does **not** move anything. A drawing tagged with EPSG:31255 but still sitting at 0,0 is in the wrong place.

## 0. Before you start
- Save a copy of the original DWG.
- `UNITS`: drawing units must be **metres** for a metric CRS. If the drawing is in millimetres, scale it by 0.001 first (`SCALE`, base point 0,0).
- `ID` on a few corners: note where the drawing currently sits.

## 1. Get control points
You need **at least 2 points** that exist both in the drawing and in the real world with known coordinates, and preferably **3** (the third one is your check).

Good sources:
- a survey of the site (best)
- cadastral boundary points (Austrian DKM data is published in Gauss-Krüger zones; check it is the same zone and EPSG code)
- points read from an orthophoto or basemap in QGIS, set to the same CRS (accuracy about 0.5–1 m)

Pick points far apart: opposite corners of the building or the site.

> EPSG:31255 numbers look like this: easting (X) roughly −110 000 to +110 000, northing (Y) roughly 140 000 to 430 000. In CAD, X = easting and Y = northing.

## 2. Move the drawing onto the coordinates: `ALIGN`
1. `ALIGN` → select everything (`ALL`) → Enter.
2. **First source point**: click control point 1 in the drawing.
3. **First destination point**: type its real coordinates, e.g. `-12345.678,345678.901`.
4. **Second source point**: click control point 2. **Second destination point**: type its coordinates.
5. Third point: Enter to finish.
6. **Scale objects based on alignment points?** → **No**, if the drawing is already in metres at 1:1. Answer Yes only if you know the drawing scale is wrong.

## 3. Check the result
- `ID` on control point 3: compare with its known coordinates. The difference is your accuracy, so write it down (e.g. "check point 3: 0.04 m").
- If the error is large: wrong point picked, wrong units, or easting and northing swapped.

## 4. Tag the coordinate system
**BricsCAD**
1. `GEOGRAPHICLOCATION` → **GIS Coordinate System** → browse → search `31255` or "Austria GK Central".
2. If it is not in the list, install the extended CS-MAP coordinate system library (described in the BricsCAD help for GEOGRAPHICLOCATION), restart and search again.
3. Leave the geographic marker inherited from the CRS; north direction 0 (the drawing is now on grid north).

**AutoCAD Map 3D / Civil 3D**: `MAPCSASSIGN` (or the Geolocation tab) → search the library for 31255. Plain AutoCAD: `GEOGRAPHICLOCATION` → set the location from map and choose the coordinate system.

## 5. Verify on a map
Open the DWG (or a DXF export) in QGIS with project CRS EPSG:31255 and add a basemap or orthophoto. Buildings and boundaries should sit on top of the image.

## 6. Hand-over note
Write in the title block or a note: CRS, control points used, check point error, date. Whoever opens the file later will know how far to trust it.
