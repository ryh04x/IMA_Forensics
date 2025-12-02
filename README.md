# Image Metadata Analyzer

> **v2.7.0 — Pro Stable Release**

**A client-side web-based digital forensic tool to extract, analyze, and interpret hidden metadata from digital images.**

---

## ⚙️ Project Overview

The Image Metadata Analyzer is a privacy-first, browser-based forensic utility that extracts EXIF, TIFF, GPS and other embedded metadata from images and helps analysts verify authenticity, detect tampering, reconstruct timelines, and preserve evidence integrity.

**Key purposes:**
- Verify image authenticity
- Surface editing software traces and anomalies
- Recover embedded thumbnails and hashes for chain-of-custody
- Visualize GPS coordinates on a map and link to Google Maps
- Produce professional forensic reports (printable PDFs)

---

## 📌 Table of Contents

1. [Key Features](#-key-features)
2. [Technology Stack](#-technology-stack)
3. [Getting Started](#-getting-started)
   - [Requirements](#requirements)
   - [Install](#install)
   - [Run Locally](#run-locally)
4. [Usage Guide](#-usage-guide)
   - [Input Options](#input-options)
   - [Analysis Workflow](#analysis-workflow)
   - [Session & Export](#session--export)
5. [Anomaly Detection & Risk Scoring](#-anomaly-detection--risk-scoring)
6. [Geolocation & Mapping](#-geolocation--mapping)
7. [Forensic Reporting](#-forensic-reporting)
8. [Security & Privacy](#-security--privacy)
9. [Developer Notes & Architecture](#-developer-notes--architecture)
10. [Roadmap / Future Scope](#-roadmap--future-scope)
11. [Contributing](#-contributing)
12. [Authors & Acknowledgements](#-authors--acknowledgements)
13. [License](#-license)
14. [Changelog (v2.7.0)](#-changelog-v270)

---

## 🔍 Key Features

- **Advanced Metadata Extraction**
  - Universal support: JPEG, PNG, WEBP, TIFF, HEIC.
  - Deep EXIF/TIFF tag parsing (Camera Model, Shutter, Aperture, Lens, Software, Dates).
  - Real-time search/filter across metadata tags.
- **Digital Forensics & Security**
  - Anomaly Detection Engine flags suspicious files (editing traces, missing timestamps, GPS inconsistencies).
  - SHA-256 integrity hashing for chain-of-custody.
  - Embedded thumbnail recovery.
- **Geolocation Intelligence**
  - Dark-mode Leaflet map to plot coordinates.
  - Direct link to open coordinates in Google Maps (Street View / Satellite).
- **Session Management & Inputs**
  - Drag-and-drop, file picker, clipboard paste (Ctrl+V), and URL fetching with CORS proxy toggle.
  - Session history with risk statuses.
- **Professional Reporting & Export**
  - Printable forensic reports (UI hidden & tables expanded automatically).
  - Export raw metadata to `.json` and copy to clipboard.

---

## 🛠️ Technology Stack

| Component | Technology |
|---|---|
| Frontend | HTML5, CSS3, ES6+, Tailwind / Custom CSS (responsive) |
| Parsing | `exifr` (EXIF/TIFF parsing library) |
| Mapping | `Leaflet.js` |
| Icons | `lucide` |
| Hashing | `SubtleCrypto` (Web Crypto API) for SHA-256 |
| Build | Vite / Rollup (recommended) |

> Note: The app is 100% client-side — no image data is uploaded.

---

## 🚀 Getting Started

### Requirements

- Modern browser that supports Web Crypto API and `File` / `Clipboard` APIs (Chrome, Firefox, Edge, Safari latest versions)
- Node.js (for local dev / building)

### Install (development)

```bash
# clone
git clone https://example.com/your-repo.git
cd your-repo

# install
npm install

# start dev server
npm run dev
```

### Build (production)

```bash
npm run build
# serve the `dist` folder with any static server
npx serve dist
```

---

## 🧭 Usage Guide

### Input Options

- **Drag & Drop:** Drop one or multiple image files into the dashed drop zone.
- **File Picker:** Click the drop zone to open a file browser.
- **Clipboard Paste:** Copy an image (or screenshot) and press `Ctrl+V` anywhere on the page.
- **URL Fetch:** Paste an image URL and click _Fetch Image_. If the site has CORS restrictions, toggle `CORS Proxy`.

### Analysis Workflow

1. The image preview, file size, MIME type and computed SHA-256 hash are shown.
2. Metadata table populates with parsed tags (grouped by EXIF, TIFF, GPS, IPTC if present).
3. The Anomaly Detector evaluates:
   - Presence of editing software traces (e.g. `Adobe Photoshop`, `GIMP`, `Lightroom`)
   - Missing or inconsistent creation/modification timestamps
   - GPS inconsistencies (impossible coordinates, switched lat/long, coordinate precision suspiciousness)
4. A **Risk Score** (Green / Yellow / Red) is computed and displayed with a short rationale.

### Session & Export

- **Session History:** Each analyzed file is logged with thumbnail, filename, time, and risk status.
- **Export JSON:** Click `Download JSON` to export the raw metadata structure.
- **Report (PDF):** Click `🖨️ Report` to generate a printable PDF — the UI will hide controls and expand data tables for a clean report.

---

## 🧩 Anomaly Detection & Risk Scoring

The engine uses heuristic checks:
- **Software fingerprinting:** Looks for `Software`, `ProcessingSoftware`, `ImageHistory` tags.
- **Timestamp validation:** Compares `DateTimeOriginal`, `DateTimeDigitized`, and `DateTime` for inconsistencies.
- **GPS validation:** Checks coordinate ranges, altitude anomalies and whether coordinates snap to known landmarks (optional reverse-geocode integration).
- **Thumbnail mismatch:** If an embedded thumbnail hash/content differs from the main image hash, flag as suspicious.

**Scoring:** Each issue adds weighted points to the risk score; thresholds determine the final status.

> Implementation note: This is a heuristics-first approach. For legally admissible conclusions, pair with additional analysis.

---

## 🗺️ Geolocation & Mapping

- Parsed GPS coordinates (if any) are displayed with precision and timestamp (if available).
- Coordinates plotted on a Leaflet map in dark mode.
- A direct link opens the coordinates in Google Maps (useful for Street View/satellite verification).

**Privacy note:** Reverse geocoding (if present) is optional and must be explicitly enabled — it may use remote APIs.

---

## 📑 Forensic Reporting

Report generation prepares a clean single-page (or multi-page) PDF containing:
- Case header (Project name, version `v2.7.0 Pro Stable`, analyst name, case ID placeholder)
- Image preview(s) and embedded thumbnails
- Key metadata highlights
- Full metadata table
- Risk summary and explanation
- SHA-256 hash and chain-of-custody notes

**Auto-behaviour:** UI chrome/buttons are hidden and all data sections are expanded before printing to ensure a consistent report.

---

## 🔐 Security & Privacy

- **Client-side only:** All processing happens in the browser. No uploads unless the user explicitly uses a server-based CORS proxy.
- **SHA-256 hashing** is performed with the Web Crypto API to avoid shipping data to third-parties.
- **CORS Proxy:** Optional to fetch images from strict origins — warn users that enabling a third-party proxy will route image bytes through that proxy.

---

## 🏗️ Developer Notes & Architecture

- **Modules:**
  - `ui/` — components (dropzone, table, map, session)
  - `parsers/` — wrapper around `exifr` and custom tag normalizers
  - `crypto/` — SHA-256 helpers (Web Crypto wrapper)
  - `report/` — print stylesheet and report scaffolding
  - `map/` — leaflet integration
  - `anomaly/` — heuristic rules and scoring engine

- **State management:** Lightweight in-memory state (e.g., simple store or use Zustand / Redux for larger scale)
- **Testing:** Unit tests for parsers and anomaly logic + end-to-end tests for UI flows (e.g., Playwright)

---

## 🔭 Roadmap / Future Scope

- AI-based deepfake detection (image content analysis)
- Video & audio metadata extraction
- Cloud-based collaborative case work (opt-in)
- Automated reverse-geocode caching & landmark snapping

---

## 🤝 Contributing

Contributions are welcome. Please follow these steps:

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit and push: `git commit -m "feat: your feature"`
4. Create a PR describing your changes and the reason

Please open issues for bugs or feature requests. Include sample images (if permissible) and reproduction steps.

---

## 👥 Authors & Project Team

- **Rhythm** — Developer — Roll No. 590018178
- **Harshit** — Developer — Roll No. 590016614
- **Tushar Arora** — Developer — Roll No. 590017995

**Under the Expert Guidance of:**
- Mr. Kunwar Pankaj Siddhant — School of Computer Science, UPES, Dehradun

---

## 📜 License

Submitted in partial fulfillment of the requirements for the award of the degree of Master of Computer Applications.

*(Add the project license here if you want an open-source license like MIT, Apache-2.0, etc.)*

---

## 📝 Changelog (v2.7.0 — Pro Stable Release)

- `v2.7.0` — Pro Stable
  - Improved anomaly detection engine
  - Thumbnail recovery improvements
  - Dark-mode Leaflet map + Google Maps links
  - Enhanced PDF/report generation and export options

---

## ❓ FAQ

**Q:** Are images uploaded to a server?  
**A:** No — all parsing & hashing happens locally in the browser by design.

**Q:** Can this detect manipulated images reliably?  
**A:** The tool flags heuristics and editing traces (eg. software, timestamp inconsistencies). It is not a substitution for dedicated deepfake / image-content forensic analysis.

---

## 🖼️ Example Usage Snippets (JS)

### Compute SHA-256 (Web Crypto)
```js
async function sha256Hex(fileBuffer) {
  const hashBuffer = await crypto.subtle.digest('SHA-256', fileBuffer);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}
```

### Parse EXIF with exifr
```js
import * as exifr from 'exifr';

const res = await exifr.parse(file, {iptc: true, tiff: true});
console.log(res);
```

---

If you'd like, I can also:
- Produce a `README.md` with badges, screenshot placeholders and ready-to-fill CI badges.
- Generate a `manifest` and `index.html` starter template.
- Create a `report-styles.css` print stylesheet and a minimal `app.js` skeleton for the core flows.

---

*Prepared for submission — Image Metadata Analyzer v2.7.0*

