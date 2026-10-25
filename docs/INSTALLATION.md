# Installing PolyCAD 0.0.5

Choose PolyCAD-0.0.5-setup.exe from the official robertmartic/polycad GitHub release.
Create and save native drawings with Line/Circle/Polyline/Rectangle tools and Move/Copy, selection and Undo/Redo.

Setup installs for the current Windows user without administrator privileges. Choose a dedicated empty
folder and optional desktop/Start menu shortcuts. The default folder is LocalAppData/Programs/PolyCAD.
Close all PolyCAD windows before setup, update or uninstall. Other Poly applications are independent.

Native .polycad files are registered for Open with. Setup does not force the Windows default association.
An Open with command opens the native document for editing. Save writes only when requested.

Reinstall/update preserves the registered path and shortcut choices unless you explicitly change the
shortcut options. Downgrades and changing an existing managed installation's path are rejected.
Use the normal uninstaller before relocating; preferences and personal files are preserved.

Uninstall through Windows installed apps or Uninstall.exe. Only owned application files and registration
are removed. Personal files, preferences and recovery storage are preserved.
Preferences and update state live under LocalAppData/PolyCAD. Recovery snapshots are stored separately under LocalAppData/PolyCAD/Recovery. Startup or Recover offers abandoned snapshots as new unsaved drawings.

For portable use extract the complete PolyCAD-0.0.5-win-x64.zip folder and run PolyCAD.exe.
Keep every runtime and native dependency beside the executable. Portable folders are not automatically
adopted as managed installations. Use setup for in-app replacement.

Packages are unsigned. Verify the official repository and release assets. An unrecognised-app prompt
from Windows does not substitute for verifying the download source.