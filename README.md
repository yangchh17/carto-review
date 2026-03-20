# Map Cartography Review Tracker

A self-contained HTML tool for structured, multi-round cartographic map reviews — built for GIS teams that pass files back and forth between mappers and reviewers without a shared project management system.

No installation. No server. No login. Open the file, fill it in, save it.

![Map Review Tracker]([carto-review.png])

---

## The problem it solves

Map review in small GIS teams typically looks like this:

1. Mapper sends a PDF or layout file
2. Reviewer opens it, jots notes in an email or a shared sheet
3. Mapper makes changes, sends a new version
4. Nobody can remember what was flagged in Round 1 vs Round 2
5. Comments get overwritten, status gets lost, the Excel sheet becomes unreliable

This tool makes the review file the source of truth. Every round of comments is preserved. The file travels with the work.

---

## Features

### Core workflow
- **Mapper / Reviewer mode toggle** — set who is currently filling out the form; saved into the HTML so the file remembers when re-opened
- **Save HTML** — checkpoints the entire state (all maps, all notes, all history) into a self-restoring HTML file you can email or commit
- **Save Excel** — exports a structured workbook with one sheet per map, a Project Overview, and a running Change Log

### Per-element tracking
- 7 review sections covering **19 cartographic elements** across Text & Labels, Legend, Base Layer, Symbology, Scale & North Arrow, Layout & Composition, and Export Quality
- **Dynamic symbology section** — add data layers on the fly with name, geometry type (point / line / polygon / raster), spec selectors, and notes
- **Status per element**: Mapper to fix · Need guidance · Good · Unset
- **Specs reviewed** — multi-select pill selector scoped to each element's relevant properties
- **N/A toggle** — locks the row completely (grey background, disabled inputs) while keeping it visible

### Audit history
- **Per-round history sub-row** under each element — collapsed by default, expands to show every export round with timestamp, note, and status chip
- **Direction label per round** — "Sent for review" (mapper mode) vs "Reviewer comments" (reviewer mode), with the person's name pulled from the meta fields
- **General comment box** per map with its own history of previous rounds
- **Changes summary strip** — live count of flagged items (excludes Good), with a Rectified button that removes from the summary while preserving history

### Multi-map support
- Unlimited map tabs per project
- Sections are drag-to-reorder per map
- Attach a reference PDF or image per map (renders inline in a floating panel)
- Progress bar per map (checked items / total non-N/A items)

### Excel export
- **Project Overview sheet** — one row per map with Mapper, Reviewer, progress
- **One sheet per map** — columns: ✓ | Section | Element | Type | Status | Specs Reviewed | Current Note | then audit history columns that grow automatically with each export
- **Audit column headers** show the submission direction and person name: `1st Mapper Submission · [Name]` / `1st Review Comments · [Name]`
- **N/A rows** rendered in grey across all columns
- **Change Log sheet** — every export appends a timestamped block showing which elements changed, what the status was set to, and the note — colour-coded by mapper (orange) vs reviewer (blue)

---

## How to use

### First time
1. Download `map_review_vX.html`
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari)
3. Enter your project code in the top bar
4. Set the mode to **Mapper** or **Reviewer**
5. Add a map tab, fill in the meta fields (mapper name, reviewer name, date, version)
6. Work through the checklist sections

### Passing the file between mapper and reviewer
1. **Mapper** fills in notes, sets statuses, clicks **Save HTML**
2. Sends the saved `.html` file to the reviewer
3. **Reviewer** opens it in a browser, switches mode to **Reviewer**, adds comments
4. Reviewer clicks **Save Excel** to generate the audit record, then **Save HTML** to pass back
5. Mapper opens the returned file — all previous rounds are visible in the per-element history

### Reading the history
Click the clock icon ⊙ under any element row to expand its history. Each round shows:
- Round number and timestamp
- The note that was written at time of export
- Status at that point (Mapper to fix → Need guidance → Good)
- Who submitted it and in which direction

---

## Checklist sections and elements

| Section | Elements |
|---|---|
| Text & Labels | Map title, Subtitle / description, Feature labels & annotations, Disclaimer |
| Legend | Legend text, Legend symbology, Legend layout |
| Base layer | ESRI base layer, Terrain base layer, Administrative boundaries, Other base layers |
| Symbology — data layers | Dynamic — add one row per data layer |
| Scale & North Arrow | Scale bar, North arrow, Zoom level / scale |
| Layout & composition | Page setup & margins, Visual hierarchy, Inset map (if present) |
| Export quality | Resolution, Export format |

---

## Technical notes

- **Single file, zero dependencies at runtime** — the XLSX export library is loaded from a CDN (`cdn.jsdelivr.net`); everything else is vanilla HTML/CSS/JS
- **No data leaves the browser** — all state is stored in memory and serialised into the saved HTML file; nothing is sent to any server
- **State persistence** — `Save HTML` serialises the full application state (all maps, rows, history, mode, section order, attached files) into a `<script>` block in the saved file; on re-open the init block restores everything
- **Attached files** are base64-encoded into the saved HTML; large PDFs will increase file size significantly
- Tested in Chrome 120+, Edge 120+, Firefox 121+

---

## Background

Built by a GIS practitioner at a consulting firm working with First Nations communities in British Columbia. The review workflow emerged from real project needs — multiple maps per project, multiple revision rounds, two or three people involved, no shared PM system.

The tool is intentionally file-based rather than cloud-based: it works offline, it travels with the project folder, and it doesn't require anyone to have an account.

---

## License

MIT — use it, adapt it, share it.

If you build on it or find it useful, a mention or a star is appreciated.

---

## Possible future additions

- PDF export of the checklist (browser print currently works but is unstyled)
- Template system for saving a blank checklist configuration
- Section-level notes field
- Support for custom checklist sections
