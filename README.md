# 3d-printing

Guide and tips for 3D printing with 0.4mm nozzle, 1.75mm filament.

## Glossary

 - *Bed:* the surface that is printed onto. Can be heated.
 - *Extrude:* the extruder (component of a 3D printer) will extrude (squeeze out) an extrusion (some material).
 - *Filament:* raw (unprinted) material.
 - *Line:* one continuous extrusion of filament (does not have to be straight).
 - *Part/print:* the thing that gets printed.
 - *Slicer:* software that converts a 3D object file (e.g. STL) into a list of instructions for the 3D printer (e.g. set temperature, move here, extrude filament).

## Resolution
Often you'll have to experiment by tweaking some parameters. I find it helpful to start with coarse adjustments (e.g. increments of 10) before fine adjustments (e.g. 0.01). Here is a guide to the minimum resolution I recommend for adjusting parameters:
 - *Line height/width:* 0.01mm
 - *Temperature:* 5C
 - *Flow:* 5%
 - *Z offset:* 0.01mm
 - *Infill density:* 5%
 - *Speed:* 5mm/s

Rule of thumb: aim to overshoot first when adjusting parameters, e.g. if you encounter overextrusion, set flow to a value you are sure will *under*extrude to calibrate your intuition about where the right level will be.

## Slicer settings (based on Cura)

### Machine settings
When the print finishes, material tends to ooze a little and can ooze at the start of the next print. To alleviate this, I like to retract filament after the print finishes using the g-code `G1 E-13.0 F300 ; retract filament after print to stop oozing`. In Cura, `Settings >> Printer >> Manage Printers... >> Machine Settings >> End G-code` allows you to add custom g-code at the end of a print (e.g. [end g-code](end_gcode.txt)).

### Quality
 - <a name="layer-height">*Layer height [mm]:*</a> lower values may improve print quality and finish but take longer. Recommendation: **0.2mm**. Maximum (for faster printing) **0.3mm**
 - *Initial layer height [mm]:* thicker layer helps bed adhesion. Recommendation: **0.3 - 0.35mm**.
 - <a name="line-width">*Line width [mm]:*</a> Lower line width may improve dimensional accuracy in some cases (higher resolution) but will require more lines thus take longer. Higher line width can improve (bed) adhesion (the sides of the nozzle will "squish" down material). Many slicers will adapt the line width (especially infill), sometimes creating lines thinner than the specified width. If the line width is large e.g. 2mm there will be gaps between lines. Setting line width to a "common" factor (e.g. 0.5 or 0.45 instead of 0.4637) can make design easier/more predictable, e.g. creating a 2mm thick wall will result in 4 x 0.5mm lines. Recommendation: **0.5mm**.
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
 - *Flow [%]:* Worth [calibrating](https://3dprintbeginner.com/artillery-sidewinder-x1-calibration-guide). Important: in practice [print speed](#speed), [line width](#line-width)/[layer height](#layer-height) impacts flow (typically higher speed -> lower effective flow), therefore (re-)calibrate using desired print speed, line width and height. Recommendation: **100%**.
 - *Initial Layer Flow [%]:* Higher initial layer flow can improve bed adhesion by pushing more material into the bed. Recommendation: 10% more e.g. **110%**.
#### PLA+
 - *Printing temperature:* **205C**.
 - *Build plate (bed) temperature [C]:* Too high and the part can warp due to temperature difference of cooler layers and hot bed. Too low and first layer may not adhere well to bed.  Recommendation: **60C**.
#### ABS
- *Printing temperature:* **215C**
- *Build plate temperature:* Too low and the part will warp and not stick. Recommendation: **110C**.
#### PETG
- *Printing temperature:* **240C**. If you get underextrusion, **250C**
- *Build plate temperature:* **70C**. Increase to **80C** if you need more bed adhesion.

### Speed
 - *Print speed [mm/s]:* Slower print speed potentially improves print quality. PETG is sensitive to speed and slower is advised, however too slow (e.g. <10mm/s) can cause blobs and stringing. Recommendation: PETG: **30mm/s**, otherwise: **60mm/s**.
 - *Travel speed [mm/s]:* Usually no issue having it faster, if it's too slow material can ooze during travel resulting in stringing, blobbing and other issues. Recommendation: **120mm/s**.
 - *Acceleration, jerk:* Higher values can make the movements 'jerky' and 'wobbly'. Recommendation: **400mm/s^2, 5mm/s**.
 - *Initial layer speed, travel, acceleration etc.:* Lower values help improve bed adhesion and quality - important since the rest of the print depends heavily on the first layer. Be careful not to lower the speed (<10mm/s) too much for PETG though. Recommendation: **Defaults/lower than other layers**.
 - *Z-hop speed [mm/s]:* Z-hop means extruder moves relatively higher than print while traveling over it to avoid hitting it. Recommendation: **5mm/s**.

### Travel
 - *Retraction distance [mm]:* Pull filament up through extruder (negative extrusion). Too low and material may ooze during travel, too high and material may 'disconnect' inside extruder and not feed back in properly. PETG is particularly stringy and requires more retraction. Calibrate by watching extruder during typical print - set to minimum required to prevent excessive oozing during travel. Recommendation: PETG: **5mm**, otherwise: **4mm**.
 - *Retraction speed [mm/s]:* Higher speed can 'suck up' filament quickly before it gets the chance to ooze, but can cause susceptible materials (e.g. PETG) to 'disconnect'. Recommendation: PETG: **15mm/s**, otherwise: **40mm/s**.
 - *Z-hop height [mm]:* Higher value reduces chance of hitting model (and potentially detaching it from the print bed - disaster) when travelling over it with extruder but makes the printer work harder. Recommendation: **0.6mm**.

### Cooling
 - *Fan speed [%]:* ABS and PETG require little to no cooling, PLA+ benefits from cooling after the first few layers (cooling the first layer(s) may reduce bed adhesion). Recommendation: first layer: **0%** (all materials), ABS: **0%**, PETG: **20%**, PLA+: **100%**.

### Support
 - *Generate support:* Try and avoid using support, often bridges/overhangs can be printed without, and in some cases, small modification to the design/orientation can eliminate the need for support. Recommendation: **off**.
 - *Support structure:* `Tree` can use (overhanging) branches to potentially reach hard-to-reach places but can be harder to remove than `Normal` support structure. Recommendation: **Normal**.

### Build plate adhesion
*Curling/warping* is when the first layer of the print detaches from the bed (in places) and curls up away from the bed due to contractive forces from above layers as they cool and shrink. Curling is most severe at sharp corners and thin features, thus, I recommend modifying parts (where possible) to reduce sharpness of corners (e.g. fillet). Also try minimising thermal shrinkage by printing at a lower temperature and for PLA+ try lowering the bed temperature to minimise the temperature difference between the first layer and (cooled) above layers. 

 - *Build plate adhesion type:* `Skirt` prints a (single-layer) ring(s) around the base of the model and can help you eyeball the rough size of the part, wipe away any excess material from the nozzle, fill/pressurize the extruder before printing the part, 'flushes' out a bit of material (that might be old/manky) before printing the all-important first layer and helps minimize initial oozing since the skirt finishes printing close to the start of the print. `Brim` helps prevent 'curling' up from the bed and improves adhesion but must be removed from the final print and can ruin the look of the finish. `Raft` should be used as a last resort if the part is not sticking (usually due to a thin or small base). Recommendation: **Skirt**.
 - *Z-offset [mm]:* Increase/decrease distance between nozzle and bed. If the nozzle is too close it can smush the print too much, actually reducing bed adhesion, and can scrape the bed (disaster), thus, be careful when using negative values here to decrease distance. If the nozzle is too high then the first layer may not be sufficiently smushed into the bed, reducing bed adhesion. Calibrate by watching the first layer, and testing the adhesion by trying to peel off the first layer - aim for the largest distance that still firmly adheres to the bed.
