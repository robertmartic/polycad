# PolyCAD 0.0.2

Early Windows x64 CAD editor. Free to use; no account, subscription, activation or telemetry.

[Download the installer](https://github.com/robertmartic/polycad/releases/latest).
Choose PolyCAD-0.0.2-setup.exe under Assets. Portable ZIP is also available.

Create, open and save native .polycad drawings. Draw Lines and Circles with live preview,
endpoint/center/grid snapping and Ortho. Select objects (Ctrl-click to add/remove), Delete,
Undo and Redo. Save/Don't save/Cancel protects unsaved work before New, Open, Close or Update.
Saving verifies a temporary file before replacement and detects external document changes.

Choose Line or Circle, then click points or enter numbers in the input field:
absolute x,y, relative @dx,dy, or a positive length/radius. All numeric input and snap grid
spacing use millimeters. Press Enter to accept, Escape to cancel the pending preview.
L: Line. C: Circle. V: Select. F8: Ortho. Ctrl+A: select all.
Ctrl+N/O/S: New/Open/Save. Ctrl+Shift+S: Save As. Ctrl+Z/Y: Undo/Redo.
F: Zoom Extents. G: visual grid. Mouse wheel: zoom at pointer. Middle-drag: pan.
Choose light/dark themes and optional GPU display in the application.

Polyline creation, Rectangle, Move/Copy, window selection, midpoint snap, recent files,
dimensions, DXF and document recovery are not implemented yet. Save your work regularly.
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
