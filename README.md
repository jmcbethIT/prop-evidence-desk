# Prop Evidence Desk

A local Windows/Python/Streamlit dashboard for organizing prop-review research and inspecting NBA injury-report evidence.

The current development milestone is v0.8: persistent original PDFs linked to saved report snapshots.

## Project status

- Current working milestone: v0.8
- Latest local acceptance test: Passed
- Last documented checkpoint: October 23, 2026
- Development status: Paused at a working baseline
- Next planned feature: Attach a report-evidence reference to a saved prop review

This is a personal development project, not an NBA-affiliated product or an automated betting recommendation service.

## Purpose

The injury-report workflow addresses a practical evidence-handling problem:

Extracted PDF text can lose the visual alignment between a player, team, status, and explanation. A text search alone may therefore be insufficient to interpret a report accurately.

The application keeps the original PDF available alongside extracted text and links saved text snapshots to the exact original document used to create them.

The goal is traceable research, not automatic injury clearance or guaranteed betting outcomes.

## Current capabilities

### Report retrieval and import

- Retrieve a report from a supported direct NBA injury-report PDF URL.
- Import a locally downloaded PDF.
- Save extracted text as a local JSON snapshot.
- Record source information, retrieval time, extracted report-header strings, and a SHA-256 identifier.
- Search report text by surname, team, matchup, or other text.

### Original PDF inspection

- Render an image of the original PDF page.
- Display layout-aware extracted text beside the page image.
- Select individual pages in a multipage report.
- Download the original PDF or extracted page text.
- Show warnings when extraction or document interpretation requires caution.

### Persistent snapshot-linked originals

- Retain original PDFs locally after successful report imports.
- Store originals under their full SHA-256 identifier.
- Associate saved text snapshots with matching originals.
- Reopen the corresponding original after restarting the application.
- Reuse a stored PDF when the same document is imported again.
- Reject an archived original that fails its integrity check.

### Explicit handling of missing evidence

If the matching original PDF is unavailable, the application displays a warning instead of silently showing a different report.

Older text-only snapshots remain usable as text, but they cannot reconstruct a missing original PDF.

## Workflow

1. Retrieve a supported official PDF or import a local copy.
2. Save the report text snapshot and original PDF.
3. Select a saved snapshot.
4. Search the extracted text.
5. Open the matching original in the layout viewer.
6. Verify the player, team, status, report timestamp, and matchup date against the original page.
7. Manually record the relevant evidence in the prop-review workflow.

Automatic evidence attachment to a saved review is planned but not yet implemented.

## Evidence flow

```text
Supported PDF URL or local upload
                |
                v
       PDF validation and parsing
                |
         +------+------+
         |             |
         v             v
   Text snapshot   Original PDF
   injury_reports/ injury_originals/
         |             |
         +------+------+
                |
       Matching SHA-256
                |
                v
      Selected snapshot viewer
                |
                v
       Manual evidence review
```

A matching SHA-256 identifies matching file contents. It does not establish that a report is authentic, current, or appropriate for a particular game.

## Technology

- Python
- Streamlit
- Requests
- pypdf
- pypdfium2
- Pillow
- Local JSON snapshot storage
- SHA-256 content identifiers
- Windows batch launch and update scripts

## Relevant application components

| Component | Purpose |
|---|---|
| `app.py` | Main Streamlit application |
| `injury_reader.py` | Report retrieval/import, text snapshots, search, and snapshot selection |
| `pdf_layout_viewer.py` | Original page rendering and layout-aware text inspection |
| `report_original_store.py` | Persistent PDF storage and hash-verified lookup |
| `START_WINDOWS.bat` | Existing Windows application launcher |
| `injury_reports/` | Generated local text snapshots; excluded from version control |
| `injury_originals/` | Generated original-PDF archive; excluded from version control |

This table documents the working local application. Repository contents may differ until all intended source files have been published.

## Running the existing local installation

The tested environment is the existing Windows application installation, with its virtual environment and dependencies already configured.

1. Open the application folder.
2. Run `START_WINDOWS.bat`.
3. Open the local Streamlit interface.
4. Use the report reader and original-layout viewer.

A complete clean-install procedure for a new computer has not yet been documented and validated. The incremental update packages should not be treated as standalone application installers.

## Local data and backups

The report workflow stores generated data locally:

- `injury_reports/`: JSON text snapshots and metadata
- `injury_originals/`: Original PDFs and any optional archive provenance notes

Back up these folders together if you want to preserve the relationship between saved text and original documents.

The application also has an existing prop-review workflow. Its private database and saved review data are not intended for the public repository.

The current PDF archive does not implement automatic retention limits or cleanup.

## Validation completed

The following local acceptance checks were reported as passed during development:

| Milestone | Acceptance result |
|---|---|
| v0.6 | Original PDF page displayed successfully beside extracted text |
| v0.7 | A retrieved/imported PDF could be viewed without a separate upload |
| v0.8 | Persistent snapshot-linked originals passed the local acceptance test |

The v0.8 acceptance procedure covered switching between saved reports and checking the matching original after restarting the application.

Development-time checks also covered:

- Python syntax validation
- PDF storage and duplicate handling
- Missing-original handling
- Invalid identifier rejection
- Archived-file corruption rejection
- Installer backup creation
- Repeat-install handling

These checks are not equivalent to comprehensive automated end-to-end testing. Full browser automation, cross-platform testing, and clean-machine installation testing remain outside the validated scope.

## Important limitations

- No automatic discovery of the latest published report
- No guarantee that the selected report is current
- No automatic matchup-date verification
- No OCR for scanned documents
- No automatic player-status inference
- No automatic lineup confirmation
- No automatic attachment of report evidence to saved prop reviews
- No betting profitability or prediction-accuracy claim

Additional interpretation rules:

- No text match does not mean a player is healthy or available.
- Retrieval time is not publication time.
- A report can cover multiple game dates.
- “NOT YET SUBMITTED” must be interpreted in the correct team context.
- Original page layout takes precedence when extracted text is ambiguous.
- Uploaded PDFs have unverified source authenticity.
- Older snapshots require their exact original PDF for hash-matched viewing.

## Development approach

This project uses incremental changes and local acceptance testing:

1. Identify a workflow problem.
2. Make a narrowly scoped change.
3. Preserve a rollback path.
4. Test the change locally.
5. Keep the last passing version as the working baseline.

The project was developed with AI assistance for code generation, update packaging, troubleshooting, and documentation. Local installation and acceptance testing were performed by the project owner.

This is a self-directed project, not a claim of professional employment experience.

## Next planned milestone

Attach an evidence reference to a saved prop review.

Planned fields:

- Selected snapshot identifier
- Original PDF SHA-256
- Report source
- Retrieval timestamp
- Supporting page number
- Manually confirmed player status
- Reviewer notes

This feature is planned, not implemented.

Before development resumes, the current prop-review saving code needs to be inspected so the attachment can be integrated without guessing at the database structure.

## Publishing and privacy

The public repository should contain source code, documentation, and sanitized examples.

Do not publish:

- Credentials or API keys
- `.env` files
- Streamlit secrets
- Local review databases
- Private saved reviews
- Virtual environments
- Unreviewed logs
- Generated report archives
- Screenshots containing sensitive information

Use sanitized screenshots or synthetic examples to demonstrate the interface.

## Current checkpoint

Development is paused at v0.8.

Resume from the working persistent-originals baseline. The next development task is to inspect the prop-review persistence code and design an explicit evidence attachment.
