# 3d-printing

Guide and tips for 3D printing with 0.4mm nozzle

## Slicer settings (based on Cura)

### Quality

 - *Initial layer height [mm]:* thicker layer helps bed adhesion. Recommendation: **0.3 - 0.35mm**.
 - *Line width [mm]:* Lower line width may improve dimensional accuracy in some cases (higher resolution) but will require more lines thus take longer. Higher line width can improve (bed) adhesion (the sides of the nozzle will "squish" down material). Many slicers will adapt the line width (especially infill), sometimes creating lines thinner than the specified width. If the line width is large e.g. 2mm there will be gaps between lines. Setting line width to a "common" factor (e.g. 0.5 or 0.45 instead of 0.4637) can make design easier/more predictable, e.g. creating a 2mm thick wall will result in 4 x 0.5mm lines. Recommendation: **0.5mm**
 - *Initial layer line width [%]:* A wider initial layer may improve bed adhesion. In rare cases it is desirable to use 100% for consistency with above layers. Recommendation: **120%**
