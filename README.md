# Carto Review

A self-contained HTML tool for structured, multi-round cartographic map reviews — built for GIS teams that pass files back and forth between mappers and reviewers without a shared project management system.

**No installation. No server. No account.** Open the file, fill it in, save it.

🔗 **[Live demo carto-review](https://yangchh17.github.io/carto-review)** · [Download latest release](https://github.com/yangchh17/carto-review/releases/latest) · [Report an issue](https://github.com/yangchh17/carto-review/issues)



![Map Review Tracker](carto-review.png)



---

## The problem it solves

Map review in small GIS teams typically looks like this:

1. Mapper sends a PDF or layout file
2. Reviewer jots notes in an email or shared spreadsheet
3. Mapper makes changes, sends a new version
4. Nobody can remember what was flagged in Round 1 vs Round 2
5. Comments get overwritten, status gets lost, the spreadsheet becomes unreliable

This tool makes the review file the source of truth. Every round of comments is preserved. The file travels with the work.

---
What's new in v1.2
Export filename now follows project naming convention: PROJECT_YYYYMMDD.html / .xlsx
Attached map file now requires confirmation before being removed (prevents accidental deletion)

---
## Features

### Core workflow
- **Mapper / Reviewer mode toggle** — set who is currently filling in the form; the mode is saved into the HTML so the file remembers when re-opened
- **Save HTML** — checkpoints the entire state (all maps, all notes, full history) into a self-restoring file you can email, commit, or share; also stamps a timestamped entry into the note history for every field that has content
- **Save Excel** — exports a formatted workbook with one sheet per map, a Project Overview tab, and an accumulating Change Log
- **Save PDF** — prints the active tab or all tabs, selectable via a dropdown

### Per-element checklist
- 7 built-in review sections covering **19 cartographic elements** across Text & Labels, Legend, Base Layer, Symbology, Scale & North Arrow, Layout & Composition, and Export Quality
- **Dynamic symbology section** — add one row per data layer with name, geometry type (point / line / polygon / raster), spec selectors, and notes
- **Status per element**: Mapper to fix · Need guidance · Good · Unset
- **Specs reviewed** — multi-select pill selector scoped to each element's relevant properties
- **N/A toggle** — sits below the status dropdown; locks the row (grey background, all inputs disabled) while keeping it visible; N/A rows are greyed out in Excel too
- **× button** — top-right of the note field, clears the note and resets the row

### Note history (new in v1.1)
Every note field has a collapsible **Note history** panel that appears as soon as you start typing:

- **Last edited row** (amber) — always reflects whatever is currently in the textarea, live as you type, tagged with the active role (Mapper / Reviewer)
- **Saved entries** — one entry stamped per Save HTML, growing list, newest first, each with timestamp and role tag
- Panel is hidden when the field is empty; auto-expands on first keystroke

The **General comments** box per map works identically — a "Previous notes" toggle with the same live + saved structure.

### Changes summary
- Live count of all flagged or noted rows (excludes Good), shown in a collapsible strip below the general comment
- Shows **Field**, **Status**, **By** (Mapper or Reviewer), and full note text
- Updates live as you type
- **✓ Rectified** button removes a row from the summary while preserving its full history

### Change Log viewer (new in v1.1)
Click **Change Log** in the top bar to open an in-app history modal without opening Excel. Per map it shows:

1. **Current session** — live view of everything currently typed across all note fields; updates in real time while the modal is open
2. **Saved note history** — all Save HTML stamps across all fields, with timestamp and role
3. **Export rounds** — all Save Excel rounds with element status and notes

### Custom sections (per map tab)
- **Sections** button opens a full section editor modal
- Add extra elements to any built-in section (e.g. add "Coordinate system" to Base Layer)
- Create entirely new custom sections with custom elements, tags, descriptions, and specs
- Customizations are **per map tab** — each tab can have a different checklist structure
- All customizations persist through Save HTML and export correctly to Excel

### Audit history (per export round)
- **Per-round history** under each element — expands to show every Save Excel round with round number, timestamp, direction chip, person name, note, and status; all on one row
- **General comment** per map with its own previous-notes history
- History is read-only — past entries are never modified

### Multi-map support
- Unlimited map tabs per project
- Sections are drag-to-reorder per tab
- Attach a reference PDF or image per map — renders in a floating panel alongside the checklist
- Progress bar per map (checked items / total non-N/A items)

### Excel export detail
- **Project Overview** — one row per map with Mapper, Reviewer, date, version, and progress percentage
- **One sheet per map** — columns: ✓ | Section | Element | Type | Status | Specs Reviewed | Current Note | audit history columns (grow automatically with each export)
- **Audit column headers** include direction and person name: `1st Mapper Submission · CY` / `1st Review Comments · JS`
- **N/A rows** rendered in grey across all columns
- **Change Log sheet** — every Save Excel appends a timestamped block per map showing which elements changed, the new status, and the note; colour-coded by mapper (orange) vs reviewer (blue)

---

## How to use

### First time
1. **[Download the latest release](https://github.com/chhyang17/carto-review/releases/latest)** and open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari) — or try the **[live demo](https://chhyang17.github.io/carto-review)** first
2. Enter your project code in the top bar
3. Set the mode to **Mapper** or **Reviewer**
4. Add a map tab, fill in the meta fields (mapper name, reviewer name, date, version)
5. Work through the checklist sections

### Passing the file back and forth
1. **Mapper** fills in notes and statuses, clicks **Save HTML**
2. Sends the `.html` file to the reviewer
3. **Reviewer** opens it, switches mode to **Reviewer**, adds comments per element
4. Reviewer clicks **Save Excel** to generate the audit record, then **Save HTML** to send back
5. Mapper opens the returned file — all previous rounds are visible in each element's history, and all notes carry their full Save HTML history

### Reading note history
Each note field shows a **Note history** toggle below it once content is entered. Expand it to see:
- The current live note (amber, "Last edited") — updates as you type
- All previously saved versions with timestamp and who wrote them (Mapper / Reviewer)

### Reading export round history
Click the clock icon row below any element to expand its export history. Each round shows:
- Round number, timestamp, direction ("Sent for review" / "Reviewer comments"), and person name — all on one line
- The note recorded at time of export
- Status at that point

### Using the Change Log
Click **Change Log** in the top bar at any time to see the full history for all maps in one view — current unsaved session, Save HTML stamps, and Save Excel rounds.

### Adding custom sections or fields
1. Click the **Sections** button in the top bar
2. Select a built-in section to add extra elements to it, or click **+ Add custom section** for a new one
3. For each element, set the name, tag, description, and specs list
4. Click **Done** — the checklist updates immediately

> Custom sections and extra fields apply to the currently active map tab only. Different maps in the same project can have different checklist structures.

---

## Built-in sections and elements

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

- **Single file, zero runtime dependencies** — the XLSX export library loads from a CDN (`cdn.jsdelivr.net`); everything else is vanilla HTML / CSS / JS
- **No data leaves the browser** — all state lives in memory and is serialised into the saved HTML file; nothing is sent to any server
- **State persistence** — Save HTML serialises the full application state (maps, rows, note histories, export rounds, mode, custom sections, attached files) into a `<script>` block in the saved file; opening the file restores everything automatically
- **Note history** is stored separately from export rounds — Save HTML stamps build a continuous record independent of Save Excel
- **Attached files** are base64-encoded into the saved HTML — large PDFs will increase file size noticeably
- Tested in Chrome 120+, Edge 120+, Firefox 121+

---

## Background

Built by a GIS practitioner to solve a real workflow problem — multiple maps per project, multiple revision rounds, two or three people involved, no shared project management system.

The tool is intentionally file-based rather than cloud-based: it works offline, it travels with the project folder, and it doesn't require anyone to have an account.

---

## License

MIT — use it, adapt it, share it.

If you find it useful, a ⭐ on GitHub is appreciated.

---

## Possible future additions

- Template system — save a custom section configuration and load it into new projects
- Batch PDF export — print all map tabs in one action with a single click
- Section-level general notes field
- Dark mode
