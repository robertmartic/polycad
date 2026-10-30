# PolyCAD updates

Open About → Updates to check manually or enable startup checks in Settings.
Updates preserve documents, preferences, recovery data, installation paths and shortcut choices.
Save or discard unsaved work before closing for an update; cancellation keeps the application open.

From 0.2.1, update information comes from https://updates.polystudio.tools/polycad/stable.json.
The application verifies the RSA-PSS/SHA-256 signature using its embedded PolyStudio public keys.
Signed information binds PolyCAD, the stable channel, the canonical version and every package's exact HTTPS address, size and SHA-256 hash.
Packages come only from https://downloads.polystudio.tools/polycad/ at immutable versioned paths.
Unexpected redirects, damaged downloads, invalid signatures, mismatched identities and downgrades are rejected.

0.2.1 includes a changed-file delta from 0.2.0. Older or modified installations use the full package.
GitHub v0.2.1 is a transition release so existing 0.2.0 clients can obtain the new updater.
Setup, maintenance installer, portable ZIP, update manifest and delta contain the same verified application files.
A failed update reports failure and preserves the backup; a registration failure restores the previous installation.
About → Updates reports the last update result and offers local update-storage cleanup.

No account, upload or telemetry is required. Portable copies use the conventional installer before in-app updates.
Release packages do not yet carry a Windows publisher code-signing certificate; channel signatures authenticate update metadata independently.