# PolyCAD 0.9.5 guide

PolyCAD is a local Windows x64 mechanical CAD application. All current tools are free. This release expands the Part → Assembly → Drawing workflow; it does not claim complete parity with Inventor.

## Sketch with model context

Select a planar face and choose **Start Sketch**, or choose an origin/work plane. The supporting model remains visible beneath the grid while sketch geometry stays in its actual local coordinate frame. Use **Show model in Sketch** to hide the background. Finish Sketch returns to 3D without changing that frame.

Use **Project Geometry**, then click a visible model edge in the Sketch viewport. Supported projected lines, circles and arcs are linked construction references. They participate in snapping but are excluded from automatic solid profiles. Select a reference and detach it before using it as editable profile geometry. Projection onto an oblique plane can produce an ellipse; unsupported ellipse projections report an error instead of approximating the CAD curve.

Sketch constraints, driving dimensions and **Parameters** work together. Fix geometry or a selected point, or place a point at the origin, in the Constraints panel. The Sketch status reports remaining degrees of freedom for supported line/circle/arc components. Convert supported polylines to individual geometry before applying those constraints. Projection references remain fixed to the source.

## Part features

The **Modeling** menu groups advanced tools. Select an input body/sketch and open the desired operation. Pick faces in the original model with Preview off, then add them to the operation. Enable Preview to inspect the result. Changing parameters turns Preview off until requested again. **Apply** computes a transaction in the background. Cancel or a failed operation leaves the original document unchanged. A result cannot overwrite a document changed while calculation was running.

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
