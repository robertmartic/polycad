# Changelog

## 0.1.5

- Add a searchable Commands palette with Ctrl+Shift+P, keyboard navigation and command availability.
- Keep unfinished drawing steps and typed parameters when cancelling command search.
- Cycle overlapping objects with Alt+click and select visible unlocked objects by geometry type.
- Add optional Intersection, Perpendicular and Nearest snaps, respecting current direction constraints.
- Show an expected parameter, units and example for every drawing/transform step.
- Remember new snap preferences and retain the existing native format.
- Deliver the productivity package previously planned for 0.2 as version 0.1.5.

## 0.1.1

- Fix unreadable tooltip text in the dark theme.
- Keep tooltip text, background and border matched to the active theme, including when switching themes with a tooltip open.

## 0.1.0

- Expanded basic 2D CAD release with Arc, Polar, Rotate, uniform Scale and Mirror.
- Create native circular arcs from a center, start and end direction, or a signed sweep in degrees.
- Rotate and scale a selection by exact angle/factor or reference points; mirror across a two-point axis.
- Preview transforms, cancel with Escape and undo each complete group in one step while preserving object identities.
- Use Polar direction steps, exact @distance<degrees input, Arc endpoint/midpoint/center snaps and circular quadrant snaps.
- Preserve exact Arc angles during transforms at large local coordinates; identity transforms keep saved drawings clean.
- Keep new precision preferences, accessible vector commands and usable narrow-window overflow.
- Read existing native drawings; older versions safely reject files that require Arc support.
- Verify document recovery, mixed-geometry workflows and the update from 0.0.8.

## 0.0.8

- Restore the original pointer position when turning off Ortho or snapping, without requiring another mouse movement.
- Keep Ctrl+Z/Ctrl+Y within numeric text input; drawing Undo/Redo remains available when working on the canvas.
- Preserve an unfinished drawing step when pressing the shortcut for the already active tool.
- Verify the complete 2D drawing workflow, including exact coordinates, snapping, grouped Move/Copy, selection, history and native Save/Open.

## 0.0.7

- Vector icons for file, drawing, selection, move/copy, history and view commands.
- Clear single active tool, keyboard focus, accessible command names and shortcut hints.
- Responsive More menu keeps essential CAD tools visible in smaller windows, in light and dark themes.

## 0.0.6
- Connect to PolyHUB 0.1.3+ for application discovery, launch and delegated update monitoring.
- Keep update download controls, Save/Don't save/Cancel and recovery protection in PolyCAD.
- Report download, preparation, cancellation, verified installation and failure states to PolyHUB.
- Preserve standalone operation, installation choices, documents, Recent and preferences.
- Existing installations acquire integration through a one-time update in About > Updates.

## 0.0.5
- Local document recovery, recent drawings and editor stabilization.
- Open recent drawings, remove selected entries or clear missing paths; the local list keeps up to twelve drawings.
- Capture committed unsaved changes locally after the first edit and every 60 seconds thereafter, including untitled drawings.
- Keep two recovery generations where cleanup is available, verify native contents and hashes, and fall back to a previous valid snapshot if the newest is unreadable.
- Offer abandoned snapshots at startup or through Recover. Open a recovered drawing as a separate unsaved document requiring Save As.
- Exclude sessions active in another window/process; Later keeps snapshots and Discard removes only the chosen recovery session.
- Preserve original files and retain recovery when storage is unavailable. Show actionable recovery errors.
- Remember Ortho, snap choices and snap-grid spacing alongside the existing theme preference.
- Keep invalid numeric-input messages visible while moving the pointer; snap to pending Polyline vertices for easier closing.
- Preserve document state, settings and recovery storage during the verified update from 0.0.3.

## 0.0.3
- Draw straight Polylines with live preview; Finish keeps them open, Close joins the last vertex to the first, and Escape discards the pending preview.
- Create Rectangles from opposite corners as editable closed Polylines.
- Move and Copy selected Lines, Circles and Polylines with a live preview and exact coordinates, relative offsets or distance.
- Undo and Redo each completed shape or group transform as a single action. Move preserves object and vertex identities.
- Select by dragging left-to-right for complete containment, or right-to-left for crossing geometry; Shift/Ctrl adds to the selection.
- Snap to segment midpoints, including a closed Polyline's closing edge.
- Keep existing native .polycad files compatible and update from 0.0.2 using a verified changed-file package.
- Recent files and document recovery remain planned.

## 0.0.2
- Draw Lines and Circles with live preview and Escape cancellation.
- Enter absolute x,y, relative @dx,dy, length or radius in millimeters.
- Snap to endpoints, circle centers or a fixed grid; constrain drawing with Ortho.
- Select one or multiple objects, Delete, Undo and Redo.
- New, Open, Save and Save As native .polycad documents with verified safe saving and Save/Don't save/Cancel protection.
- Show selected geometry properties and use the owner's new PolyCAD logo throughout the app and installer.
- Update from 0.0.1 using a verified changed-file package while preserving installation choices and personal files.
- Polyline creation, Rectangle, Move/Copy, window selection, midpoint snap, recent files and document recovery remain planned.
## 0.0.1
- Initial early CAD geometry preview for Windows.
- Inspect Line, Circle and Polyline test scenes with pan, cursor-centered zoom, grid and axes.
- Switch between light/dark themes and software/GPU display.
- Open native .polycad drawings read-only.
- Install with optional desktop and Start menu shortcuts, and uninstall while preserving personal files and preferences.
- Check, download and verify in-app updates with progress, cancellation, retry and rollback.

Drawing/editing tools, Save, Undo/Redo, snapping and document recovery are not included in this early release.