# PolyCAD 0.0.3

Early Windows x64 CAD editor. Free to use; no account, subscription, activation or telemetry.

[Download the installer](https://github.com/robertmartic/polycad/releases/latest).
Choose PolyCAD-0.0.3-setup.exe under Assets. Portable ZIP is also available.

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
L: Line. C: Circle. P: Polyline. R: Rectangle. M: Move. K: Copy. V: Select. F8: Ortho. Ctrl+A: select all.
Ctrl+N/O/S: New/Open/Save. Ctrl+Shift+S: Save As. Ctrl+Z/Y: Undo/Redo.
F: Zoom Extents. G: visual grid. Mouse wheel: zoom at pointer. Middle-drag: pan.
Choose light/dark themes and optional GPU display in the application.

Recent files, dimensions, DXF and document recovery are not implemented yet. Save your work regularly.
The agreed 0.1.0 workflow remains in development.

Windows 10 build 19041 or newer / Windows 11, x64. Self-contained; no separate .NET installation.
About contains Overview, offline Changelog and Updates. Installed copies can download and verify
updates, with cancellation, retry, full/delta selection and rollback. Startup checks can be disabled.
Portable copies can check availability; use the conventional installer to enable replacement.

Processing stays on your PC. Update checks contact the official public GitHub channel; drawings
are never uploaded. Downloads are verified with SHA-256 using official GitHub release digests.
Packages are not code-signed; these hashes are not an independent publisher signature.

See docs/INSTALLATION.md, docs/UPDATES.md, LICENSE, THIRD-PARTY-NOTICES.txt and licenses/.
Source and development documentation are private. Public tags identify distribution metadata commits.
PolyCAD artwork was supplied by the project owner. This independent project is not affiliated with
other similarly named products.
