# PolyCAD updates

About > Updates provides manual checks, optional startup checks, release notes, download progress,
cancellation, retry, update storage management and the last recorded update result.
A visible Update available action appears when a newer version is found.

Updates come only from robertmartic/polycad GitHub Releases. No private token is embedded in the app.
Drawings and personal data are never uploaded. Version comparisons are numeric; downgrades are rejected.
Version 0.0.2 provides a full package and a changed-file delta from the published 0.0.1 baseline.

Installed copies download the update manifest, full portable package or matching file-level delta,
and a small maintenance installer. GitHub's SHA-256 release digests and every manifest file hash are
checked. A delta contains whole changed files, not byte patches. A mismatched base uses the full package.
Unsigned packages trust the official GitHub channel; hashes are not an independent digital signature.

Installation starts only after Update now. The helper waits for the application to exit, rejects other
running instances, stages the new tree, verifies target files, switches directories and refreshes Windows
registration. Registration or verification failures restore the old installation. Preferences, documents,
install path and shortcut choices are preserved. Unsaved drawings require Save, Don't save or Cancel before an update. Cancelling or failing to save keeps the app open and prevents installation.

Keep sibling .PolyCAD-backup-* folders after an interrupted update. A handled error can roll back;
power loss or forced termination during directory replacement may require the official full installer.
Never infer success from process exit alone. Open the existing shortcut and inspect About > Updates.

Ended downloads can be cleaned after 7 days; old backups after 30 days. The latest verified backup,
prepared/active operations and folders with additional files are retained. Storage cleanup is explicit
and never removes personal drawings or document recovery.

A real update of the owner's installed application requires confirmation. Development checks use
separate fixture installations and do not update the owner's apps.