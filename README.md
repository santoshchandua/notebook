# NoteNest — offline foundation

A dependency-free responsive notebook app. Run `npm start` with Node.js installed and open http://127.0.0.1:4173. No dependency installation is needed. For hosting, serve `dist` over HTTPS. Notes use IndexedDB; a service worker caches the application for subsequent offline launches. No notes are uploaded.

Implemented: workspace naming, notebooks with coloured covers and a library, typing with device autosave, search, local text history, paper styles and writable margins, TXT/Markdown import, text/Markdown/print-to-PDF export, additive notebook/workspace backup restore, and password-based per-note encryption (PBKDF2 SHA-256, 250,000 iterations; AES-256-GCM).

Also implemented: stylus/mouse handwriting, ink colours and thickness, highlighter, eraser, ink undo/redo, local correction ink, lines, arrows, rectangles, ellipses and triangles. Equations support editable Unicode symbols and handwriting. Typed content paginates automatically, with a fresh blank page at the end. Drawing on the last blank page adds another. Typed top-margin headings automatically populate a linked notebook index. Deleted notes can be restored from Storage & backup.

Unlocked notes are stored in plaintext. Re-lock to encrypt them again. Encryption includes text, margins, ink and history and has no password recovery. Browser storage can be cleared, so export backups. PDF uses the browser print dialog; enable background graphics when retaining notebook lines. Text exports do not preserve drawings; PDF and NoteNest backups do.

Not yet implemented: account authentication, cloud sync, multi-user permissions, comments/reviewer workflows, submission locks, attachments, payments, app-wide automatic locking, native mobile packages. Sharing controls explain this explicitly.

Next phase: select and provision a usage-based backend, implement authenticated synchronization with conflict preservation and server-enforced access permissions, then add review submissions and retained cloud revisions. Sharing must not rely on client-side roles.

## Prototype limitations

Handwriting recognition, searchable handwritten text, a full mathematical layout engine, pressure-sensitive strokes and advanced object selection are not implemented. Handwritten headings require a typed heading for automatic indexing. Pen input uses browser Pointer Events; mouse input was tested, but real tablet/stylus hardware still needs testing. Finger touch is reserved for scrolling.

Margins and ink attach to page positions. Editing earlier text can move text under existing ink, so stable text/ink anchoring needs further development. Page counts exclude locked content in the index. Correction ink is a local annotation tool, not a separate authenticated reviewer session. Print layout depends on browser page size, scale and background settings. This is a first working prototype, not a completed production app.

## Validation

Browser checks passed for covers, page overflow and spare pages, margin index links, colours/shapes/eraser/undo/redo, equation insertion, encryption and wrong-password rejection, backup import, print output with all text pages and ink, trash restore, offline reload, mobile viewport overflow and absence of JavaScript errors. Layout screenshots were inspected. Checks used isolated test data, not user notebooks.

Notebook removal is non-destructive: Remove from library hides its cover and sidebar entry while retaining all local data. Hidden notebooks can be restored or exported from Library or Storage & backup. Existing files on disk are never removed. Importing a backup creates a visible copy.

