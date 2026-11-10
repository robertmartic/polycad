# PolyCAD 0.7.0

Standalone Windows x64 2D CAD editor. Free to use; no account, subscription, activation or telemetry.

[Download the installer](https://downloads.polystudio.tools/polycad/0.7.0/PolyCAD-0.7.0-setup.exe).
Download PolyCAD-0.7.0-setup.exe. Portable ZIP is also available.

Create, open and save native .polycad drawings. Draw Lines, Circles, straight Polylines and Rectangles with live preview,
endpoint/midpoint/center/grid snapping and Ortho. Select objects (Ctrl-click to add/remove), Delete,
Undo and Redo. Save/Don't save/Cancel protects unsaved work before New, Open, Close or Update.
Saving verifies a temporary file before replacement and detects external document changes.

For Polyline, accept each vertex then press Enter with an empty input or choose Finish to keep it
open. Choose Close (or accept the first vertex again) to close a Polyline with at least three vertices.
Escape discards the entire unfinished preview. Rectangle accepts two opposite corners.

Select objects, choose Move or Copy, accept a base point, then accept the destination.
Use @dx,dy for an exact offset or a positive distance along the preview direction.
Move keeps original identities; Copy creates independent objects. One Undo reverses the whole group.
Drag left-to-right to select fully contained objects, or right-to-left to select crossing geometry.
Shift/Ctrl+drag adds objects; Shift/Ctrl+click toggles one object.

Choose a drawing tool, then click points or enter numbers in the input field:
absolute x,y, relative @dx,dy, or a positive length/radius. All numeric input and snap grid
spacing use millimeters. Press Enter to accept, Escape to cancel the pending preview.
L: Line. C: Circle. A: Arc. P: Polyline. R: Rectangle. M/K: Move/Copy. T/S/I: Rotate/Scale/Mirror. V: Select. F8: Ortho. F10: Polar. Ctrl+A: select all.
Ctrl+N/O/S: New/Open/Save. Ctrl+Shift+S: Save As. Ctrl+Z/Y: Undo/Redo.
F: Zoom Extents. G: visual grid. Mouse wheel: zoom at pointer. Middle-drag: pan.
Choose light/dark themes and optional GPU display in the application.

Recent lists up to twelve successfully opened or saved drawings, with Remove and Remove missing.
Recovery captures committed changes after the first edit and every 60 seconds while changes remain.
Each window/document has independent snapshots under LocalAppData/PolyCAD/Recovery.
Two generations are retained where cleanup is available. Live sessions in other windows are excluded.
After an unexpected exit, startup offers verified abandoned snapshots. Recover also opens this list.
Later keeps snapshots; Discard snapshot removes only the selected session after confirmation.
Recovery opens a separate unsaved drawing requiring Save As; it never silently overwrites the original.
Unreadable newest snapshots fall back to an earlier verified generation when one is available.
An unsaved tool preview is not committed geometry and is not included in snapshots.
Changes since the last completed snapshot may be lost. Recovery is not a substitute for regular Save.
Successful Save or explicit discard/normal close clears that document's snapshots.
Recovery failures are shown in Document safety; manual saving remains available.
Ortho, snap choices and snap-grid spacing are remembered, independently of document geometry.

Dimensions are not implemented yet. Basic DXF exchange is described below.


Windows 10 build 19041 or newer / Windows 11, x64. Self-contained; no separate .NET installation.
About contains Overview, offline Changelog and Updates. Installed copies can download and verify
updates, with cancellation, retry, full/delta selection and rollback. Startup checks can be disabled.
Portable copies can check availability; use the conventional installer to enable replacement.

Processing stays on your PC; drawings are never uploaded. Update checks contact the signed PolyStudio channel.
RSA-PSS/SHA-256 signatures authenticate metadata; Cloudflare packages are verified by exact address, size and SHA-256.
Windows installer publisher code signing is not yet provided. GitHub v0.2.1 remains a bridge for older clients.

See docs/INSTALLATION.md, docs/UPDATES.md, LICENSE, THIRD-PARTY-NOTICES.txt and licenses/.
Source and development documentation are private. Public tags identify distribution metadata commits.
PolyCAD artwork was supplied by the project owner. This independent project is not affiliated with
other similarly named products.

PolyHUB integration: PolyHUB 0.1.3+ lists PolyCAD and can launch its supported updater with
PolyCAD 0.0.6+. Download controls and Save/Don't save/Cancel remain in PolyCAD. Recovery,
Recent and preferences remain local. PolyHUB monitors the result and independently verifies
installed files before confirming success. PolyCAD remains fully standalone.
Existing 0.0.5 and earlier installations need a one-time update using PolyCAD About > Updates.

Vector command icons include accessible names and shortcut tooltips. The active drawing tool is highlighted. At smaller window widths, More holds secondary commands while file and drawing tools remain visible.

Turning off Ortho or a snap restores the original pointer position. Ctrl+Z/Ctrl+Y edits numeric text while that field has focus, and drawing history while the canvas has focus. Repeating the active tool shortcut preserves its unfinished preview.

Arc: choose its center, then a start point (or positive radius along the pointer direction).
Choose an end direction for a counterclockwise arc, or enter a signed sweep in degrees.
Positive sweeps run counterclockwise; negative sweeps run clockwise. Full circles use Circle.
Arc endpoints, angular midpoint, center and cardinal quadrants support object snapping.

Rotate: select objects, choose a pivot, then enter signed degrees. Alternatively pick a
reference point and a destination direction. Scale: choose a base point and a positive
uniform factor, or pick reference and destination distances from that base point.
Mirror: choose two distinct axis points; the selected originals are reflected.
Transforms preview before the final point, preserve entity/vertex IDs, and undo as one group.
Escape discards a pending transform. Copy makes fresh IDs, including for Arcs.

Polar (F10) constrains Line, Polyline, Move and Copy directions to the selected 15/30/45/90
degree increment. Ortho (F8) takes precedence. Explicit x,y and @dx,dy override constraints;
@distance<degrees enters an exact polar offset from the current anchor. Angles are degrees
counterclockwise from +X; distances are millimeters. Precision preferences are remembered.

Native format remains v1 with declared capabilities. This release reads existing drawings.
Documents containing Arcs require an Arc-capable reader; older PolyCAD versions reject them
without modifying the file. Files with only Line/Circle/Polyline remain readable in 0.0.8.
Dimensions, text, DXF exchange and 3D are future work.
Search commands: use the magnifying-glass Commands button or Ctrl+Shift+P. Search by name,
shortcut or description, choose with Up/Down, then Enter or Run. Unavailable commands stay
labelled and cannot run. Escape closes the palette while keeping unfinished geometry and
typed parameter text. New/Open/Save and other document commands keep their existing safeguards.

Selection: Alt+click cycles overlapping objects; Shift/Ctrl+Alt+click toggles the next hit.
Use "Select all Line/Circle/Arc/Polyline objects" in Commands to select by type, or Clear selection.
Invisible and locked geometry remains excluded. Selection changes do not modify the drawing.

Additional snaps are optional, initially off, and remembered in preferences:
- Intersection: isolated intersections of finite line/polyline segments, circles and arcs.
  Coincident overlaps and numerically uncertain cases do not supply a unique snap. Very dense
  local searches pause with an on-screen hint; zoom in or disable Intersection.
- Perpendicular: a foot from the current anchor to a finite segment or circular curve.
- Nearest: the nearest curve point, used as a fallback after feature snaps.
All modes use a screen-space aperture and respect Ortho/Polar direction constraints.
Enable them in the Precision sidebar or search their names in Commands.

The parameter field shows the expected value, units and a short example for the current step:
coordinates/distances in millimeters, rotation/Arc sweep in degrees, and uniform Scale as a factor.
The native format and current drawing tools remain compatible with existing releases.
Layers and properties (0.2):
- Manage layers from the sidebar or Commands. Add a unique name, rename a layer, change
  visibility/locking, or delete an empty layer. Layer 0 keeps its name and identity.
  To delete a nonempty layer, first move its objects elsewhere.
- Choose a visible unlocked Active layer for new objects. Select objects, choose a target
  active layer, then Move selection to layer. The group moves as one Undo operation.
- Hidden layers do not render or participate in selection/snapping. Locked layers remain
  visible but cannot be selected or edited. Layer metadata changes support Undo/Redo.
- Select one object and use Object properties (Ctrl+1). Edit Line endpoints, Circle center/radius,
  Arc center/radius/start/sweep, or Polyline vertex coordinates and closed/open state.
  Use Load vertex before editing another vertex; staged edits apply together. Values use
  millimeters and degrees. Apply validates the complete object; Cancel leaves it unchanged.
- Layer and property edits preserve entity/vertex IDs. Successful metadata/property edits
  cancel an unfinished tool preview. Cancelling a properties dialog keeps that preview.
- The active-layer choice belongs to the current window and is not stored in the native file.
  Reopened/recovered drawings use the first visible unlocked layer. If the active layer becomes
  unavailable, another writable layer is used; if none exists, manage layers or Undo to re-enable drawing.
Layer tables, visibility, locks and edited geometry save/recover in native v1 without migration.
The 0.1.5 reader accepts these files, including Arcs. DXF remains a later release.
3D model and work planes — 0.7.0
--------------------------------
Find 3D Model on the toolbar or under More. The same commands appear in Ctrl+Shift+P.

- Show 3D Model opens the orthographic viewport. Drag with the middle mouse button to orbit,
  hold Shift while dragging to pan, scroll to zoom and press F to fit. Choose a Standard 3D View
  for Isometric, Top, Bottom, Front, Back, Right or Left.
- Open a sketch work plane to draw or edit on XY, XZ or YZ with the existing 2D tools.
  Sketch layers stay on their own planes. Sketch curves appear in the 3D viewport.
- Create a solid box or cylinder by entering the dimensions, base plane and world origin.
  The box origin is a base corner and the cylinder origin is its base center. Height follows the
  plane normal (positive Z on XY, negative Y on XZ and positive X on YZ).
- Click a solid to inspect it. Double-click it or use Object properties to edit it. Edits and
  deletions are undoable. Save the model as .polycad. Files with solids or additional work planes
  require PolyCAD 0.7.0 or later. Existing 2D files open in their XY drawing view.

DXF and plot sheets cover the XY drawing. DXF reports omitted solids and non-XY sketch objects.

Sketches, reusable geometry and sheets — 0.6.0
---------------------------------------------
Open Sketch & Sheets on the toolbar or in More. Commands are also available via Ctrl+Shift+P.

- Select two lines and choose Sketch constraints. Add coincident endpoints, parallel or perpendicular lines.
  Select a rectangle or straight polyline to convert it to joined sketch lines. Existing right angles
  become perpendicular constraints. The solver supports up to 24 lines per connected component.
  Edit a driving line dimension to update the component. Conflicts leave the sketch unchanged.
- Define a named block from selected line, arc, circle or straight polyline geometry. Insert it at
  an explicit model point. Redefining the block from another selection updates every instance.
- Group selected objects for shared selection, movement and copying. Ungroup to edit members individually.
- Hatch a closed polyline, circular contour or a closed chain of straight objects. Set line angle and spacing.
  A hatch stores a contour snapshot. Circular contours are approximated with straight edges.
- Save a named plot sheet with paper size, view center and scale. A scale of 1 means 1:1.
  Export vector PDF or send the sheet to a Windows printer. Check the printer's paper setup and
  print a PDF at Actual size to retain the chosen scale.

DXF exchanges supported text and dimensions as measurements. Constraints, blocks, hatch patterns
and native sheets stay in the .polycad workflow. Files using 0.6.0 capabilities require 0.6.0 or later.

Dimensions and notes — 0.5.0
---------------------------
Find Dimension and Text in Annotate (More on smaller windows) or search with Ctrl+Shift+P.
Pick a line, circle or arc and place the dimension. Pick Driving to set the size or Reference to
show the current measurement in parentheses. Double-click a dimension or use Object properties to edit it.
Changing the length of a line holds its start point and direction. A radius or diameter edit holds
the center, and an arc retains its angles. One driving dimension can control each source.
Set text height, arrow size and decimals per dimension. Deleting a source leaves a Missing reference label.
Text notes support multiple lines, model-space height, rotation and left, center or right alignment.
Save annotations to .polycad. Files with annotations require 0.5.0 or later.

Geometry editing — 0.4.0
------------------------
Find these tools by their icons in Modify (More on smaller windows) or search with Ctrl+Shift+P.

- Trim and Extend: pick a visible boundary, then pick the portion to remove or the end to extend on a line or open arc. Lines, circles, arcs and straight polylines can serve as boundaries.
- Offset: pick a line, circle or arc. Click on the desired side at the target distance, or point to that side and type an exact distance in millimeters.
- Break: pick a line, circle, open arc or polyline at the first cut. Pick a second point or enter its coordinates to remove a gap. Press Enter at the first point to preview a single cut. On a closed contour, the gap follows the contour direction (counterclockwise on circles).
- Join: select connected lines and open polylines on the same layer, then choose Join. The selection must form one unbranched chain or loop.

Review the result and choose Apply (Enter) to commit one Undo step. Escape discards the preview.

DXF exchange — 0.3.0
-------------------
Choose Import DXF / Export DXF in the DXF toolbar group (More on smaller windows),
or search for these commands with Ctrl+Shift+P. You can also choose the DXF export format in Save As.
Supported exchange profile: AutoCAD 2013 ASCII DXF, version AC1027, UTF-8 text.
Other DXF versions, binary DXF and DWG are not supported in this release.

Import reads model-space XY LINE, CIRCLE, ARC, LWPOLYLINE and classic 2D POLYLINE.
Polylines contain straight segments; closed polylines need at least three usable vertices.
Layer names, visibility and locks are transferred. Hidden/locked layers stay hidden/locked;
use Manage layers to reveal/unlock them. Units mm/cm/m/in/ft are converted to millimeters.
If source units are missing, unitless or unsupported, choose what one drawing unit means.
Review the complete report, then choose Import as new drawing. Existing unsaved work
still receives Save / Don't save / Cancel. Save the import as a new .polycad document.
The source DXF is never overwritten by import.

Unsupported dimension or text variants, INSERT/block references, hatches, splines, 3D/non-XY/thick geometry,
bulged polylines, hidden entities and paper-space objects are skipped and counted.
Block definitions are not expanded and external references are never opened.
Visual styles, colors, lineweights and polyline widths are not retained; the report
identifies omitted appearance data. A partial import is explicitly reported.
Malformed, degenerate or out-of-range supported geometry fails without replacing
the current drawing. The exchange limit is 32 MiB and one million non-comment groups.

Export includes every committed object, including hidden/locked layers, in millimeters.
It does not include unfinished tool previews and does not mark the native document saved.
DXF standard Arcs are counterclockwise: clockwise native Arcs swap endpoints while
preserving their curve, and full-turn Arcs become Circles. These changes are reported.
Layer names must be valid and unique in DXF; rename incompatible names before export.
The complete export is checked by reading it back, then written through a verified
temporary file. Existing destinations are protected against conflicting changes.
