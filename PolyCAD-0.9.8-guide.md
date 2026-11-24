# PolyCAD 0.9.8 guide

PolyCAD is a free, local Windows x64 mechanical CAD application. Save native **.polycad** files to preserve Sketches, dimensions, constraints, feature definitions and links.

## Smart Dimension

While editing a Sketch, choose **Dimension** in the Dimensions ribbon group. **Position Dimension** opens the same unified picker.

- Click a line, then move into empty space and click to place its length dimension.
- Click two line interiors, then place an angle dimension. Endpoint clicks select points instead, so use the line interiors for angles.
- Click a circle or arc curve, then place a radius dimension. Enable **Diameter for circles/arcs** to use diameter.
- Click two points, then move and click to place their distance. Supported points include line/arc endpoints, polyline vertices, circular centres and the Sketch origin.

The origin is marked at the axes intersection and is directly selectable. Picked references and hovered points are highlighted. A live dimension preview follows the pointer. **Auto** chooses horizontal distance when the pointer is within the points' horizontal span, vertical distance within their vertical span, and aligned distance elsewhere. **H**, **V** and **Aligned** explicitly fix that choice.

After placing a dimension, its value is immediately selected for typing. Enter/Apply commits; Escape/Cancel leaves the document unchanged. A double-click on an existing dimension opens the same focused input next to it.

For a rectangle already dimensioned in width and height, position one corner from the origin with separate H and V dimensions. Set both to **0 mm** to put that corner at the origin. Signed horizontal/vertical distances distinguish the sides of the origin; aligned distance is non-negative. Other dimensions and constraints remain enforced. Picking vertices of a contour converts it to connected Sketch lines when a driving point dimension requires that representation.

## Reference dimensions

Enable **Reference (measurement only)** before placing a dimension, or in its edit window. Reference dimensions appear muted and in parentheses. Their displayed value follows the geometry and they do not remove degrees of freedom. They cannot drive a Parameters binding. Turning a reference dimension back into a driving dimension is subject to the normal constraint checks.

## Coincident with origin

Choose **Coincident** from Constraints, then click the Sketch point and the origin, or another supported point. This adds zero horizontal and vertical driving relations, making the points coincident. For a dimensioned rectangle this locates the chosen corner while preserving its size. Existing line/arc endpoint relations and automatic drawing connections remain supported.

## Drag geometry and dimensions

With **Select** active, drag an endpoint to move that point, or drag a curve away from its endpoints to translate its connected geometry. The preview is separate from the document until release. Existing dimensions, fixation, projected references and constraints remain enforced. Invalid motion retains the last valid preview. Release commits one Undo step; Escape cancels.

Drag a dimension label to reposition the dimension line outside the contour. Hold **Alt** while dragging to move only its text, with a leader. This changes layout, not the geometric measurement. Existing legacy Position Dimensions retain their text-placement behavior.

## Sketch status and conflicts

Supported free Sketch geometry is blue and fully constrained geometry is green, with theme-adjusted contrast. Selected geometry uses the selection accent. The status reports remaining freedoms and explicitly identifies unsupported contours excluded from the analysis.

A conflicting dimension edit is rejected atomically. Its references and related dimensions/relations are highlighted in red while the editor stays open. A bounded diagnostic also names individual existing dimensions or relations whose removal makes the proposed edit solvable, when such a cause can be isolated. Multiple interacting constraints can still require manual inspection in Constraints. Cancel clears the error highlighting.

## Center Rectangle

The Draw group includes **Center Rectangle**, with a local vector icon. Click its centre, then an opposite corner. The following focused numeric window sets width and height. The centre remains fixed at the picked position while those dimensions change; clicking the origin first creates a rectangle centred about the origin. Use ordinary Rectangle for corner-first drawing.

## Existing workflows and compatibility

Post-draw input for Line, Rectangle, Circle and Arc remains available. Sketch Trim applies immediately per click; right-click or Escape ends drafting tools. Editable source Sketches regenerate their features on Finish Sketch; invalid features keep explicit error/stale-result indications. Unified Extrude New Body/Join/Cut, Copy/Paste Sketch, contextual Work Planes, selected-Sketch visibility, Sketch Fillet/Chamfer and Assembly dragging remain available.

New point/line-angle dimensions, reference mode, centre relations and independent text placement require **0.9.8**. Older native projects remain supported; older applications reject capabilities they cannot interpret. Keep a backup before saving an older project. Dimensions and their layout survive native save/open, Undo/Redo and supported Sketch copying. As before, axis-dependent relations on a copy rotated by a non-right angle are omitted with a notice. Unsupported or ambiguous references are reported.

Update through **File → Updates**, saving work first. Official packages contain the standalone native application and CAD runtime; no .NET runtime is required.

## Part features

The **Modeling**, **Modify** and **Reference** ribbon groups expose the corresponding tools. Use **More** when groups are collapsed on a narrow window. Select an input body/sketch and open the desired operation. **Auto Preview** is on by default in advanced feature panels. Changing parameters refreshes the preview after a short delay. Superseded results are discarded. Turn Auto Preview off when choosing original faces, add them, then turn it on again. **Apply** computes a transaction in the background. Cancel or a failed operation leaves the original document unchanged. A result cannot overwrite a document changed while calculation was running.

- **Extrude Options** supports Create, Join and Cut, forward/back distances, symmetric total distance, Through All and Up To Face. Choose the real target body and the supported stopping face. Use a closed valid profile; Sweep/Loft have stricter single-region requirements.
- **Hole** uses a planar face, its local center coordinates, diameter and blind depth or through extent.
- **Shell** removes the selected opening faces and uses inward wall thickness. **Draft** uses selected faces, pull direction, neutral plane and angle.
- **Loft** uses ordered closed sketch sections without inner holes. **Sweep** uses a closed profile and a separate connected open line/arc path. These tools report unsupported/self-intersecting configurations.
- **Mirror Body** and **Move Body** use explicit planes or translation/rotation. An associative work plane can drive Mirror.
- **Rectangular/Circular Pattern** includes the seed in the instance count and supports up to 256 instances. **Repeat feature changes only** repeats the additive/subtractive solid changes of a modifying seed, such as Hole, Cut, Fillet or joined Extrude, on its existing body. Leave this off for whole-body copies. A base body has no prior modifying delta and uses a body pattern.

Edit a feature from Model Browser or Properties. Suppression is available for modifying features, with normal dependency validation. Base features cannot be suppressed if no replacement input body exists. Delete dependent operations first. Invalid/missing/ambiguous references produce an error; PolyCAD does not silently select another edge.

**Work Features** creates named planes, axes and points. Plane offset/orientation drives associated sketches. Parameters can bind supported advanced measurements, pattern counts and work-plane offsets. Parameter units and integer counts are checked before committing.

## Inspection and materials

**Inspect** opens a read-only section view with an origin-plane direction, offset and reverse side. Turn Section view off before selecting geometry for modeling. Section topology is temporary and never becomes a modeling reference. Select model edges to measure exact curve length, circular radius/diameter, minimum edge-to-edge distance and the angle between straight edges.

Properties provides volume, surface area and centroid. Assign Material sets density in kg/m³; mass uses the solid volume in mm³. These are geometric/density calculations, not a structural or manufacturing simulation. Assembly BOM mass is unknown when a source Part has mixed or unassigned materials.

## Assemblies

Create an Assembly from File. Insert saved native Parts or STEP files and duplicate/place instances. The first inserted component is fixed; adjust fixed/free placement and local translation/rotation in the Assembly panel.

Add Plane, Axis, Distance or Angle constraints between component references. Select planar faces for Plane/face-distance constraints, cylindrical faces for axes, or enter local points/axes. The solver reports actual remaining rigid degrees of freedom. Conflicting constraints are rejected transactionally.

Refresh links explicitly after saving source changes. Changed source identities or ambiguous references are rejected. Run Interference to calculate intersecting solid volume; use BOM for quantities and available material/mass values. Nested assemblies and a complete persistent topology naming system are not supported in this release.

## Engineering drawings

Save a Part/Assembly first, then create an engineering Drawing from it. Drawing stores a linked source snapshot. Refresh it after saving source changes. Add sheets, adjust title/revision, and configure orthographic or isometric views, scale, hidden edges and center marks.

Add section views with a true solid cut and hatch, or cropped detail views. Select generated model-edge geometry for linked length/radius/diameter/angle dimensions. Values come from the model, not paper scale. Use a view normal to a circular edge for radius/diameter. Missing or ambiguous source references are reported on refresh.

Generated view geometry is protected. Add ordinary notes on the sheet's editable notes layer. For Assemblies, add BOM tables and balloons referencing actual component instances. Export all sheets to one PDF; print the active sheet with the existing physical-scale/orientation checks. DXF exchanges supported generated drawing geometry and does not preserve the linked feature model.

## Save, exchange and portable projects

Save **.polycad** for sketch/feature history, parameters, links and drawing definitions. Older versions reject capabilities they do not understand; keep a backup before replacing an older native file. STEP preserves precise solids without the PolyCAD feature tree. Multi-solid STEP imports as separate body entries. DXF solid output remains triangulated.

**File → Pack project with linked files** makes a ZIP without modifying original files. Refresh/save linked changes first: packing rejects outdated fingerprints and cyclic/unsupported links. Extract the entire ZIP into a new folder and open **Project.polycad**. Keep its **Links** folder beside it. The ZIP contains local CAD documents, not application source code.

Use **File → Updates** to install the official update. Save work before updating. The installer and updater preserve the PolyCAD application identity and do not update other Poly applications.
