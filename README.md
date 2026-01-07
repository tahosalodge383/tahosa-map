# Tahosa Map

An interactive, web-based map of chapters in **Tahosa Lodge**. The map is built as a static site and is intended to be embedded or linked from the lodge website, while remaining easy to host and maintain via GitHub Pages.

**Live map:** https://tahosalodge383.github.io/tahosa-map/

![Screenshot of map](images/Screenshot%202025-04-09%20102610.png)

---

## What this project is (and why it exists)

This project was created to provide an accurate, usable district/chapter reference map for the Tahosa Lodge website.

At the time of creation, the district map available on the council’s website:

- was no longer aligned with the official **Council Service Territory Maps** published by Scouting America,
- lacked important reference context (cities, counties, roads, state boundaries),
- was just seven colored polygons outlining the districts on a white background,
- and therefore made it difficult for someone to interpret where boundaries actually were.

This version focuses on *orientation and clarity*: district/chapter boundaries are overlaid on OpenStreetMap and presented as an interactive map with hover/click behavior, labels, and familiar geographic context.

**Reference:** [Council Service Territory Maps](https://www.scouting.org/outdoor-programs/properties/territory-maps/)

---

## How the map was made (documentary overview)

This repository is the “web export” version of the map—what a browser needs to render the interactive layers.

The overall workflow looked like this:

1. **Boundary tracing and GIS work in QGIS**
    - Council boundary was manually traced using the official service territory map as the reference.
    - The tracing process was not purely mechanical: some segments follow county boundaries cleanly, while others include irregular cuts and exclusions that required careful interpretation.

2. **Working inward to define districts/chapters**
    - District/chapter boundaries were created largely by following county and school district boundaries where appropriate.
    - The prior council map was used for guidance where needed.
    - District websites (and other public references) were used to confirm which school districts were served and to resolve edge cases.

3. **Supporting GIS datasets**
    - Publicly available GIS layers (county boundaries, school districts, municipalities, etc.) were used to “carve out” the final shapes with better precision than hand-drawing alone.

4. **Export to a web map using qgis2web**
    - The QGIS project was exported using the **qgis2web** plugin into a **Leaflet** web map.
    - After export, a small amount of manual HTML/asset tweaking was performed to get the final hosted version polished and consistent.

5. **Hosting on GitHub Pages**
    - The site is hosted via GitHub Pages and then embedded into (or linked from) the Tahosa Lodge website.

Tooling used:
- **[QGIS](https://qgis.org/)**
- **[qgis2web](https://github.com/qgis2web/qgis2web)**
- **[Leaflet](https://leafletjs.com/)**

---

## Repository layout

This is a static site. The important pieces are:

- `index.html`  
  The main entry point for the map (open this to view the project).

- `data/GreaterColoradoCouncil_1.js`  
  GeoJSON file containing the boundary and attribute data used by the map (district/chapter names, polygon features, etc.).

- `js/`, `css/`  
  JavaScript and stylesheets produced by export tooling and/or adjusted for the final presentation.

- `images/`  
  Documentation images such as the README screenshot.

- `qgis_data/Greater Colorado Council Map.zip`  
  Original QGIS files that were used to create the map prior to the qgis2web export.

Other folders (such as `webfonts/`) contain assets required for the exported map UI.

---

## Viewing the map locally

You can usually preview the map on your local machine:

### Open the file directly
1. Download or clone this repository.
2. Open `index.html` in your browser.

Note: some browsers apply stricter security rules when opening local files (especially around loading local data files). If you run into missing layers or console warnings, use Option B.

---

## Updating the map (recommended maintenance workflow)

This repo represents the “web-ready output.” The authoritative editing typically happens in QGIS, then gets exported again.

Because every GIS-to-web workflow accumulates a few “tribal knowledge” steps, here is a suggested repeatable process for updates:

### 1) Update GIS shapes and attributes in QGIS
- Adjust boundaries.
- Update district/chapter names and any popup/label fields used by the web map.
- Validate topology where appropriate (e.g., avoid gaps/overlaps if the map expects clean polygons).

### 2) Re-export using qgis2web
- Export to **Leaflet** format.
- Keep export settings consistent with prior versions where possible (layer names, field usage, styling, popup templates), to reduce downstream edits.

### 3) Replace exported site assets in this repository
Typically, that means updating some combination of:
- `index.html`
- files in `data/`
- files in `js/` and `css/`

### 4) Re-apply any manual tweaks (if applicable)
After export, a small amount of manual HTML/asset tweaking may be needed to get the final hosted version polished and consistent.

### 5) Validate before publishing
- Confirm boundaries visually at multiple zoom levels.
- Click/hover several areas to confirm labels/popups still look correct.
- Compare against the Council Service Territory Maps for alignment.

### 6) Publish
Commit changes and push to the default branch used by GitHub Pages. Once Pages rebuilds, verify the live URL.

---

## Data sources, attribution, and accuracy notes

- The basemap is OpenStreetMap-based via the Leaflet ecosystem (and includes attribution within the map UI).
- Administrative and school district boundary datasets were obtained from publicly available GIS sources and used as references to improve accuracy and consistency.

**Accuracy note:** This map is intended as a practical, visual reference for district/chapter orientation and website use. When official boundary interpretation matters for a decision or publication, verify against the official Council Service Territory Maps and current council guidance.

---

## Contributing / Corrections

If you spot a boundary that looks incorrect:
- include the district/chapter name,
- describe the location (nearest city/county/road),
- and, if possible, link the reference source used for the correction.

[Opening an issue](../../issues) with that information is the fastest way to get it fixed.

---

## Author

This map was originally created by Brendan Curley, 2025 Associate Lodge Adviser of Marketing.

