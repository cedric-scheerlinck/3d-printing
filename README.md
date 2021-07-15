# 3d-printing

Guide and tips for 3D printing with 0.4mm nozzle, 1.75mm filament.

## Glossary

 - *Bed:* the surface that is printed onto. Can be heated.
 - *Extrude:* the extruder (component of a 3D printer) will extrude (squeeze out) an extrusion (some material).
 - *Filament:* raw (unprinted) material.
 - *Line:* one continuous extrusion of filament (does not have to be straight).
 - *Part/print:* the thing that gets printed.
 - *Slicer:* software that converts a 3D object file (e.g. STL) into a list of instructions for the 3D printer (e.g. set temperature, move here, extrude filament).

## Slicer settings (based on Cura)

### Quality

 - *Initial layer height [mm]:* thicker layer helps bed adhesion. Recommendation: **0.3 - 0.35mm**.
 - *Line width [mm]:* Lower line width may improve dimensional accuracy in some cases (higher resolution) but will require more lines thus take longer. Higher line width can improve (bed) adhesion (the sides of the nozzle will "squish" down material). Many slicers will adapt the line width (especially infill), sometimes creating lines thinner than the specified width. If the line width is large e.g. 2mm there will be gaps between lines. Setting line width to a "common" factor (e.g. 0.5 or 0.45 instead of 0.4637) can make design easier/more predictable, e.g. creating a 2mm thick wall will result in 4 x 0.5mm lines. Recommendation: **0.5mm**.
 - *Initial layer line width [%]:* A wider initial layer may improve bed adhesion. In rare cases it is desirable to use 100% for consistency with above layers. Recommendation: **120%**.

### Walls

 - *Wall line count [n]:* Fewer walls can reduce print time but decrease part strength/stability. Smaller parts can get away with less walls. Recommendation: **3**.
 - *Z-seam alignment:* Starting point of each path in a layer (can produce an ugly 'seam' due to too much/little material at that point if it lines with other layers). *Random* can disperse this effect by starting at a random point each layer. *Shaprest corner* can hide the seam by placing it on a corner. *Shortest* can reduce print time. Recommendation: **Shortest**.

### Top/Bottom

 - *Top layers [n]:* Number of layers on the top surface of a print. Fewer layers can reduce print time but decrease strength/flatness/finish quality. Note this is not the final few layers of the entire print, rather the last few layers before any exposed surface on the print (can and usually does occur lower down as well). Recommendation: **3**
 - *Bottom layers [n]:* Similar to top layers (follow advice above). More bottom layers can improve flatness and therefore increase chances of success for printing layers above. Recommendation: **3**.
 - *Enable ironing:* The (hot) nozzle will "slide" (iron) over the top surface of the print, slightly melting the print and possibly extruding a tiny amount of material to fill tiny gaps to obtain a smoother finish. Recommendation: **off**, but if you want to use it (requires tweaking):
    - *Ironing pattern:* Zig zag
    - *Ironing line spacing:* 0.1mm
    - *Ironing flow:* 10%
    - *Ironing speed, acceleration, jerk:* not too fast e.g. 50mm/s, 400mm/s^2, 5mm/s.

### Infill

 - *Infill density [%]:* Infill acts like support inside the part. Lower infill saves material at the cost of strength. When a print transitions from infill to top layer it may have to "bridge" the gap between infill lines (so you don't want them too far apart with too low density). Recommendation: **10%**.
 - *Infill pattern:* Many opinions about this online. Lines prints fast. Recommendation: **Lines (aka rectilinear)**.

### Material
Obviously depends on the material.
 - *Printing temperature [C]:* Quick calibration - set to the lowest temperature that you can manually push filmanet through easily. Better calibration - print a [temperature tower](https://www.thingiverse.com/thing:2729076).
 - *Flow [%]:* Worth [calibrating](https://3dprintbeginner.com/artillery-sidewinder-x1-calibration-guide). Recommendation: **100%**.
#### PLA+
 - *Printing temperature:* **200C**.
 - *Build plate (bed) temperature [C]:* Too high and the part can warp due to temperature difference of cooler layers and hot bed. Too low and first layer may not adhere well to bed.  Recommendation: **60C**.
#### ABS
- *Printing temperature:* **215C**
- *Build plate temperature:* Too low and the part will warp and not stick. Recommendation: **110C**.
#### PETG
- *Printing temperature:* **235C**
- *Build plate temperature:* **70C**

