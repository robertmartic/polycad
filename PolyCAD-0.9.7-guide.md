# PolyCAD 0.9.7 guide

PolyCAD is a local Windows x64 mechanical CAD application. All current tools are free. Save native **.polycad** files to preserve Sketches, constraints, feature definitions and links.

## Compact contextual tools

The ribbon uses small vector icons in named groups. Hover an icon for its English name; active tools are highlighted. Narrow windows retain the remaining groups under **More**, without a horizontal ribbon scrollbar. Sketch, Part Modeling and Assembly each expose their relevant tools. The original Work Features editor, drawing-plane choices, inspection, layers and plotting remain available through the corresponding groups.

## Draw and immediately dimension

After completing a **Line**, **Rectangle**, **Circle** or **Arc**, a small dimension window opens with the first numeric field selected. Type directly, then press **Enter** or **Apply**. Line uses length; Rectangle uses width/height; Circle supports radius/diameter; Arc supports radius and sweep angle. The resulting dimensions drive the geometry. **Keep start point / centre** preserves the initial placement during this input. Rectangle dimensioning converts its contour to connected constrained lines while retaining supported references.

**Keep drawn geometry** or **Escape** dismisses the input without adding dimensions. The drawing tool stays available. A right click finishes the active drafting tool and keeps completed geometry; it also cancels an unfinished contour. Escape remains available for ending tools.

## Dimensions and constraints

Use the **Dimensions** group for **Dimension** or **Position Dimension**. Select geometry first, or launch the tool and select geometry. Position dimensions measure horizontal or vertical signed distances from the local Sketch origin or another supported entity endpoint/centre. Choose the appropriate start/end reference in the panel. For a rectangle, position dimensioning first converts the contour to connected lines. Apply separate horizontal and vertical dimensions to locate a corner. Double-click a displayed dimension label to edit its driving value.

Endpoint Snap creates a **Coincident** relation when a new line/arc endpoint lands on an existing line/arc endpoint. Horizontal and Vertical relations are added to exactly aligned new lines. Applied relations and aligned-line hints are visible in the canvas; the Constraints group and manager allow inspection/removal. Connected geometry follows dimension edits subject to its other constraints. Use position dimensions or anchors to remove remaining freedoms. Conflicting requests are rejected without changing the document.

The **Parameters** table can bind variables/formulas to the new dimensions, including signed position distances and arc angles. A bound measurement is edited through its parameter. Existing annotation dimensions and their bindings remain supported. Sketch status explicitly identifies contours excluded from its degree-of-freedom analysis rather than calling them fully constrained.

## Trim and edit existing feature Sketches

Choose **Trim**, hover the unwanted segment, then click: removal is immediate and does not need Enter/Apply. Trim stays active; each click is one Undo action. Right click or Escape ends Trim. Shift-click selects an optional boundary; **All Intersections** restores automatic boundaries. Complete circles need at least two distinct intersections/tangencies. Line/arc/path intervals, including a complete rectangle edge between endpoint intersections, can be removed. Locked projected geometry remains protected.

**Edit Sketch** permits temporary open contours even when an Extrusion or another feature uses that Sketch. **Finish Sketch** rebuilds the model. A failed feature has a red **X** and a message in Model Browser; dependent failures are also reported. If a previous successful solid is available, it is shown with a clear stale-model warning. It cannot silently serve as a valid updated modeling result. The edited Sketch and error state can be saved and reopened. Repair the Sketch and finish it again to regenerate.

Constraints still apply during editing. Removing or changing constrained geometry can require removing an incompatible dimension/constraint; temporary profile openness itself is permitted. Undo/Redo preserves the associated geometry and feature state.

## One Extrude for new geometry and cuts

Launch **Extrude** in Part Modeling, with or without an existing Sketch selection. Choose the Sketch in the Browser, the panel list, or using **Pick Sketch in Browser / viewport**. The distance field is immediately selected when the input is ready.

- **New Body** creates an independent solid.
- **Join** adds to the chosen body. A disconnected addition is rejected; use New Body for a separate solid.
- **Cut** removes material. A single visible result body is selected automatically; choose a different target from the list or **Pick target body in Browser / viewport** when needed.

Enter a distance and choose **Forward**, **Reverse**, **Symmetric** or **Two-sided**. Cut Forward points inward relative to the Sketch normal. **Through All** is available for Cut and spans the target on both sides of the Sketch plane. A non-intersecting cut reports that no material would be removed.

**Advanced extent options** retains backward distance, symmetric extents and Up To Face. Two-sided extents use the primary forward distance and the backward distance in that section. Inspect the preview, then Apply or Enter. Escape/Cancel leaves the document unchanged. The separate Cut creation button is removed; older saved Cut definitions remain readable/editable.

## Sketch selection and edge finishing

Selecting a Sketch in Model Browser highlights its actual contour above the model surface. Hidden portions are dashed and muted, visible portions are solid; selecting a hidden Sketch temporarily shows its contour. Its visibility setting is preserved after deselection.

**Fillet** and **Chamfer** can be opened before choosing edges. Select a valid edge, including a circular edge of a Revolve result, to see the preview. Hold Ctrl to add/remove more edges; **Select edges** re-enters picking. Geometry limits still apply: excessive sizes or unsupported/invalid edge combinations report a kernel error without altering the model.

The Sketch Modify group also includes **Sketch Fillet** and **Sketch Chamfer**. Select two adjacent lines with Ctrl, or select a polyline corner. Fillet uses a radius; Chamfer supports two distances or a distance and angle. Existing incompatible driving constraints must be adjusted before changing a corner.

## Copy Sketch and work planes

Right-click a Sketch in Model Browser and choose **Copy Sketch**. Right-click an origin/user plane, or a supported planar model face, and choose **Paste Sketch**. Preview placement with local X/Y offsets and rotation, then Apply. The copy has independent IDs and preserves supported internal dimensions, constraints, anchors and groups. Projected geometry becomes an independent snapshot; external relations are not silently linked to unrelated objects. Notices explain these cases before Apply. Axis-specific constraints/coordinate dimensions need right-angle rotations to retain their axis interpretation. Position values follow the destination origin and pasted placement. Explode blocks/hatches before copying them.

Right-click an existing plane and choose **Create Work Plane**. Set the normal offset, tilt angle and a local base-plane axis, inspect the preview, then Apply. The new named plane is listed under Work Features and its **Sketch** action starts a Sketch there. This creation dialog stores the resulting placement; it does not create a live dependency on a subsequently edited parent work plane. The existing **Work Features** editor remains available for editing planes, axes and points.

## Assembly interaction

Assembly has its own component, position, constraint and inspection groups. Part creation tools are not shown. Click any part surface or edge to select the whole component. Face selection is enabled specifically while defining Assembly constraints.

Hold the left mouse button and drag a free component to move it parallel to the view plane. Release to commit; the entire drag is one Undo action. Escape cancels. Placement constraints remain enforced and an invalid move keeps the last valid preview. Fixed components stay in place; their Browser rows show **Fixed**, and **Fixed / Free** changes this setting. The first inserted component remains fixed by default. Use Placement for exact translation/rotation, and the existing Assembly panel for links, mates, interference and BOM.

## Compatibility

Existing projects and legacy C# geometry remain supported. Files using the new driving-dimension, regeneration, connected-path or reverse-extrusion capabilities require 0.9.7 or later; older applications reject unsupported capabilities. Keep a backup before replacing an older project. STEP preserves solids and DXF preserves its documented supported exchange data; native files remain necessary for parametric Sketch history and the new driving dimensions.

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
