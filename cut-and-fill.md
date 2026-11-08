# Cut and fill volumes: my checklist

How I calculate earthwork volumes from a survey and a grading design, so the numbers hold up when the contractor starts hauling. I did this on site for years as a surveyor; the steps are the same in Civil 3D, other software or a spreadsheet.

## 1. Check the inputs
- **Existing ground**: survey points (PNEZD) or contours? Which coordinate system and vertical datum, which units (metres, international feet or US survey feet), and how old is the survey.
- **Breaklines**: tops and toes of banks, ditch flowlines, edges of pavement. Without them the surface cuts across features and the volume is wrong.
- **Design**: finished grade or subgrade? Volumes are measured to **subgrade**: finished floor minus slab and base, pavement surface minus the pavement section.
- **Limits**: the boundary of the work (site boundary or daylight line) and what is included: building pad, parking, ponds, trenches.

## 2. Build the surfaces
- **Existing surface (TIN)** from points and breaklines.
- Look for spikes: a wrong rod height or a wrong code gives one point far above or below its neighbours.
- Remove long triangles outside the surveyed area (boundary or maximum triangle length), or they add volume that is not there.
- **Proposed surface**: pad and parking at subgrade, side slopes (for example 3:1) running out to existing ground. The daylight line is where they meet.

## 3. Calculate three ways
| Method | How | What it is for |
| --- | --- | --- |
| **TIN to TIN** (volume surface) | Difference between the two surfaces | Main result |
| **Grid** | Depth at each grid corner (for example 25 ft or 10 m), averaged, times cell area | Quick check, easy to read in Excel |
| **Average end area** | Cut and fill areas on sections every 50 ft or 20 m along a baseline | Check, and a basis for the haul plan |

The three should agree within a few percent. If they do not, look for missing breaklines, a wrong boundary or a slope that does not reach existing ground.

## 4. Adjust
- **Topsoil strip** is a separate line: depth times disturbed area. Topsoil is not reused as structural fill.
- **Shrink and swell**: take the factors from the geotechnical report and state them. Without a report, state the assumed factor and ask.
- **Net import or export**: after the strip and the shrink factor, not before.

## 5. Deliver
- Cut/fill map with the 0-line (where cut changes to fill) and depth bands.
- Volume table: cut, fill, net, topsoil, factors used, import or export.
- Typical sections.
- A list of assumptions and questions: datum, subgrade depths, factors, rock, haul-off allowed or not.

Worked example: [earthwork cut and fill](https://github.com/Grishutov/takeoff-samples#7-earthwork-cut-and-fill---commercial-site-us-units).
