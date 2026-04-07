# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Planning COT — analizador de planning mensual para el servicio de traumatología (COT). Sube un Excel con el planning y visualiza calendarios, guardias, rankings, gráficos D3 y retribución estimada.

## Development

```bash
# Serve locally (port 8080)
npx serve --no-clipboard -l 8080

# Or use the provided script
.claude/serve.sh
```

No build step. No tests. No linting. All files are served statically via GitHub Pages.

## Architecture

**Single-file HTML app** — `index.html` (~5700 lines) is a self-contained app (CSS in `<style>`, JS in `<script>`, no frameworks). Excel upload, calendar, D3 charts (radar, slope, bar, stacked), PDF/ICS export, retribución calculator. Auth check redirects to hub on production.

### Data flow

```
Data source (one of):
  A) Excel upload → processFile() → FileReader → XLSX.read()
  B) Google Sheets → fetchFromGoogleSheets() → Apps Script proxy → base64 → XLSX.read()

  → parseWorksheetPure(ws)
  → parsedData{surgeonId: [{day, month, year, dayOfWeek, activity, companions?}]}
  → allDates[], availableMonths[]
  → renderResults(sid):
      ├─ renderCalendar()      → month grid with activity tags
      ├─ renderSummary()       → activity counts (month/total modes)
      ├─ renderTurns()         → weekly turn breakdown
      ├─ renderRetribution()   → guard/localizado pay (contaje/bruto/neto)
      └─ renderCharts()        → 13+ D3 charts (lazy, only when dashboard expanded)
```

### Key globals

- `SURGEONS` — ID→name registry; `SURGEON_FEMALE` — female ID set; `SURGEON_UNITS` — ID→unit list
- `ACTIVITIES` — activity definitions with label, tag, icon, color, period (morning/afternoon/allday)
- `parsedData` — parsed planning data `{ surgeonId: [entries] }`
- `currentMonth`, `currentYear`, `availableMonths` — month navigation state
- `summaryMode` ('month'|'total'), `retribMode` ('contaje'|'bruto'|'neto'), `currentJornada` (100|80|60)
- `RETRIB_RATES` — hardcoded guard/localizado pay rates (GPF + LOC)
- `HOLIDAYS_2026` — official Andalucía + Seville holidays; `inferredHolidays` — auto-detected from data
- `chartsExpanded`, `icompMode`, `icompViz` — dashboard/chart UI state
- `gsLoadedFromCloud` — whether current data came from Google Sheets (controls source display)

### Google Sheets connection

Uses a Google Apps Script proxy that exports the spreadsheet as XLSX binary (base64). This preserves cell colors needed for parsing. Key localStorage keys:
- `planning-gs-url` — Apps Script endpoint URL (configured by user via settings gear)
- `planning-gs-hash` — MD5 hash for cache validation (avoids re-downloading unchanged data)
- `planning-gs-ts` — timestamp of last successful fetch
- `planning-gs-xlsxB64` — cached XLSX blob for offline fallback

Auto-loads on page open if URL configured. Checks for updates every 30 min (shows non-intrusive banner). Manual upload always works as fallback.

### Excel parsing details

- `parseWorksheetPure(ws)` — finds URG rows (surgery headers), day columns, and maps surgeon IDs to activities by row offset
- `getCellFgRGB()` detects cell colors: **orange** = gestion, **green** = rucot/diferida_t
- `groupSurgeonsAsPairs()` — quirófano pairing logic with `companions[]` arrays

### Auth

Line 4: checks `localStorage.getItem('cot_auth')` with 24h expiry. Redirects to hub (`jmacot.github.io`) on production; bypassed on localhost.

## Key conventions

- **Design system B "Radiología Glass"**: fonts Source Serif 4 + Source Sans 3 + Source Code Pro, header Slate Steel `#1e293b → #334155 → #475569`, glassmorphism cards/inputs, dark mode via `[data-theme="dark"]`. See parent repo `CLAUDE.md` and `@STYLE-GUIDE.md` for full rules.
- **CDN fallback chains**: SheetJS and D3 use multi-CDN fallback (`try-catch` with sequential `<script>` injection) because corporate proxies (ImprivataCE) block CDNs.
- **D3 SVG sizing**: always set explicit `.attr('width', W).attr('height', H)` plus `viewBox` — Windows Chromium renders 0×0 otherwise.
- **`svgUrl()` helper**: use instead of `` `url(#${id})` `` for SVG gradients/clip-paths (fixes `file://` on Windows).
- **D3 chart theming**: `getChartTheme()` returns colors for current light/dark mode; gradients via `addGradient()` in `<defs>`; `showD3Tooltip()` handles viewport-aware positioning.
- **Dark mode toggle**: CSS-only sky toggle, stored in localStorage. Inputs use `--surface2`.
- **Lazy chart rendering**: charts only render when dashboard is expanded, via `requestAnimationFrame()`.
- **Language**: always `lang="es"`, all UI text in Spanish.
- **Event pattern**: button groups (summary-toggle, retrib-toggle, jornada-toggle, etc.) use uniform toggle pattern — remove active from all, add to clicked, update state, re-render.

## Assets

- **assets/img/portada.png** — Welcome hero image

## Project structure

```
planning-cot/
├── index.html      # App completa (single file, ~5700 líneas)
├── icon.svg        # App icon
├── assets/img/     # Imágenes de la app
├── .gitignore
├── LICENSE          # MIT
├── README.md
└── CLAUDE.md
```
