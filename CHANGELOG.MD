# Changelog

This file records the documented development milestones for Prop Evidence Desk.

Version numbers refer to local development milestones. They do not necessarily indicate published GitHub releases.

## v0.8 — Persistent snapshot-linked original PDFs

Status: Local acceptance test passed  
Checkpoint date: October 23, 2026

### Added

- Persistent storage of original PDFs after successful report imports.
- SHA-256-based lookup between text snapshots and original PDFs.
- Loading the matching original when a saved snapshot is selected.
- Original-PDF availability after application restart.
- Integrity checks before displaying archived originals.
- Warnings for missing originals without fallback to an unrelated report.
- Automatic selection of a newly imported snapshot.

### Preserved

- Existing saved text snapshots.
- Existing prop-review data.
- Separate PDF upload for standalone inspection.
- Manual interpretation of player statuses.

### Validation

- Local acceptance test reported as passed.
- Development-time checks covered syntax, storage, duplicate handling,
  missing files, invalid identifiers, corruption rejection, installer
  backups, and repeat installation.

### Known limitations

- Older text-only snapshots need the matching original PDF.
- No automatic archive cleanup.
- No automatic player-status inference.
- No automatic evidence attachment to saved prop reviews.
- Full clean-machine and automated browser testing remain outstanding.

## v0.7 — Shared PDF bridge

Status: Local workflow test passed

### Added

- Shared PDF access between the report reader and layout viewer.
- Viewing a successfully retrieved/imported report without a separate upload.
- Display of source and retrieval metadata for the shared PDF.

### Limitations at that milestone

- The shared original existed only in the current application session.
- The viewer used the most recent successful retrieval/import.
- Selecting a historical text snapshot did not switch the original PDF.

These limitations motivated v0.8.

## v0.6 — Original PDF layout viewer

Status: Local original-page display check passed

### Added

- Rendering of original PDF pages.
- Side-by-side layout-aware text extraction.
- Multipage navigation.
- Download of the original PDF and extracted page text.
- Optional local archiving with provenance notes.

### Design decision

Original PDF pages remain the reference when extracted text loses
alignment or produces ambiguous player/status relationships.

## v0.5 — Injury-report reader baseline

Status: Existing baseline used for subsequent development

### Capabilities

- Retrieval from supported direct official PDF URLs.
- Local PDF import.
- Text extraction and JSON snapshot storage.
- Report-header string extraction.
- Source, retrieval-time, and SHA-256 metadata.
- Search across extracted pages.
- Warnings against treating a missing text match as proof of availability.

### Limitation

Original PDF bytes were not retained automatically.

## Planned — Evidence references in saved prop reviews

Not implemented.

### Proposed scope

- Attach the selected report snapshot identifier.
- Preserve the original PDF hash.
- Record source and retrieval timestamp.
- Record the supporting page number.
- Save manually confirmed player status and notes.

### Prerequisite

Inspect the current prop-review persistence code before designing the
integration.
