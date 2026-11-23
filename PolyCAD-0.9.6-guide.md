# PolyCAD 0.9.6 guide

PolyCAD is a local Windows x64 mechanical CAD application. All current tools are free. This release improves sketch trimming, contour diagnostics, polyline conversion and automatic feature previews. The Part → Assembly → Drawing workflow remains available.

## Sketch with model context

Select a planar face and choose **Start Sketch**, or choose an origin/work plane. The supporting model remains visible beneath the grid while sketch geometry stays in its actual local coordinate frame. Use **Show model in Sketch** to hide the background. Finish Sketch returns to 3D without changing that frame.

Use **Project Geometry**, then click a visible model edge in the Sketch viewport. Supported projected lines, circles and arcs are linked construction references. They participate in snapping but are excluded from automatic solid profiles. Select a reference and detach it before using it as editable profile geometry. Projection onto an oblique plane can produce an ellipse; unsupported ellipse projections report an error instead of approximating the CAD curve.

Sketch constraints, driving dimensions and **Parameters** work together. Fix geometry or a selected point, or place a point at the origin, in the Constraints panel. The Sketch status reports remaining degrees of freedom for supported line/circle/arc components. Convert supported polylines to individual geometry before applying those constraints. Projection references remain fixed to the source.

## Trim circles, arcs and paths

Choose **Trim** on the Sketch ribbon. No initial selection or cutting boundary is required. Hover the unwanted interval between visible intersections: the removed geometry is highlighted red. Click to stage the result, then press **Enter** or **Apply**. Trim remains active for the next segment. **Escape** cancels an unconfirmed modification or finishes the tool. Undo restores each confirmed trim.

Trim supports complete circles, clockwise/counterclockwise arcs, lines, polylines and mixed line/arc paths. A circle needs at least two distinct cutting intersections or tangencies. A single tangent does not determine an unambiguous interval. For a particular boundary, **Shift-click** that boundary, then hover/click the target. **All intersections** returns to automatic boundaries. Only geometry visible in the same Sketch or compatible drawing plane participates; the shaded supporting 3D model must first be projected if you want its edges as boundaries.

For a rounded lower-right corner like a circle tangent to the bottom and right edges: hover the large inner portion of the circle and confirm its removal. Then trim the two short straight pieces between the circle's tangent points and the old sharp corner. The remaining quarter-circle and outer contour form the rounded profile.

Locked/projected targets are protected. Constraints, driving dimensions and dependent solid features remain validated. Trim reports conflicts instead of silently deleting those references. Editing a profile that already drives a solid can reject intermediate open contours; this release does not introduce deferred regeneration for unfinished sketches.

## Convert polylines and diagnose contours

Select a rectangle/polyline, then choose **Modify → Explode**, or **Convert to sketch lines** in Constraints. The original entity ID stays on the first segment. Existing supported extrusion inputs, groups and an explicitly selected Revolve contour follow the conversion. Connected endpoints and existing right angles receive constraints; Undo restores the original polyline. Trimming constrained endpoints may require deliberately removing or changing those constraints.

An explicitly selected Revolve line/arc now identifies its connected contour, rather than unrelated profiles elsewhere in the Sketch. Files using this capability require 0.9.6 or later. Keep the original file if you need to work in an older version.

**Check Profile** reports open endpoints and branched junctions with red markers, including line/arc paths when the native CAD kernel is active. It focuses the problem area. Close gaps or remove extra segments before extrusion. Overlap/self-intersection failures without identifiable endpoints retain the kernel error and a separate repair message.

## Part features

The **Modeling** menu groups advanced tools. Select an input body/sketch and open the desired operation. **Auto Preview** is on by default in advanced feature panels. Changing parameters refreshes the preview after a short delay. Superseded results are discarded. Turn Auto Preview off when choosing original faces, add them, then turn it on again. **Apply** computes a transaction in the background. Cancel or a failed operation leaves the original document unchanged. A result cannot overwrite a document changed while calculation was running.

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
