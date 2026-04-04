# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Planning COT — analizador de planning mensual para el servicio de traumatologia (COT). Sube un Excel con el planning y visualiza calendarios, guardias, rankings, graficos D3 y retribucion estimada. Incluye vistas pixel art del hospital con sprites animados.

## Development

```bash
# Serve locally (port 8080)
npx serve --no-clipboard -l 8080

# Or use the provided script
.claude/serve.sh
```

No build step. No tests. No linting. All files are served statically via GitHub Pages.

## Architecture

**Single-file HTML apps** — each `.html` file is a self-contained app (CSS in `<style>`, JS in `<script>`, no frameworks):

- **index.html** (~6200 lines) — Main app. Excel upload, calendar, D3 charts (radar, slope, bar, stacked), PDF/ICS export, retribucion calculator. Auth check redirects to hub on production.
- **hospital.html** (~1200 lines) — Pixel art hospital view with animated surgeon sprites from sprite sheets.
- **hospital-topdown.html** (~2000 lines) — Top-down tile-based hospital map using canvas and sprite assets.
- **test-quirofano.html** — Test page for operating room tile rendering.

## Key conventions

- **Design system B "Clinico"**: fonts Lora + Inter, header gradient `#0f2240 → #1a3a5c → #234e77`, dark mode via `[data-theme="dark"]`. See parent repo `CLAUDE.md` for full rules.
- **CDN fallback chains**: SheetJS and D3 use multi-CDN fallback (`try-catch` with sequential `<script>` injection) because corporate proxies block CDNs.
- **D3 SVG sizing**: always set explicit `.attr('width', W).attr('height', H)` plus `viewBox` — Windows Chromium renders 0x0 otherwise.
- **`svgUrl()` helper**: use instead of `` `url(#${id})` `` for SVG gradients/clip-paths (fixes `file://` on Windows).
- **Dark mode toggle**: CSS-only sky toggle, stored in localStorage. Inputs use `--surface2`.
- **Language**: always `lang="es"`, all UI text in Spanish.

## Assets

- **assets/hospital/** — Hospital-specific sprite sheets (beds, doors, tiles, furniture) from the "Interior" tileset
- **assets/characters/** — Surgeon character sprite sheets (body, hair, outfits) for animated pixel art
- **assets/interior/** — Additional interior tiles (Hospital_01-07, Modern Interiors 32x32, home furniture sheets)
- **assets/zones/** — Pre-rendered zone images (quirofanos, consultas, urgencias, planta) as PNG and animated GIF
- **pixelart/** — Raw sprite packs (untracked/large): Modern Interiors, MetroCity, Character Generator

Sprites are 16x16 or 32x32 pixel tiles arranged in sprite sheets. The HTML files extract frames via canvas `drawImage()` with source rectangle coordinates.
