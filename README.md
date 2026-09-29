# PDF Studio Community & Official Templates

Official repository hosting static JSON templates and WebP thumbnails for [PDF Studio](https://github.com/solomadestudios/PDFStudio).

## Repository Structure
- `/templates/manifest.json`: Template catalog listing all available online templates.
- `/templates/*.json`: Pre-built template definitions ready for download.
- `/thumbnails/*.webp`: Pre-rendered high performance vector snapshots for instant grid scrolling.

## Usage in PDF Studio
The app syncs templates via `RemoteTemplateManager` querying:
`https://raw.githubusercontent.com/solomadestudios/pdfstudio-templates/main/templates/manifest.json`