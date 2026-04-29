# Improved Initiative Custom Dark CSS Theme

## Project Overview
A custom CSS theme for the [Improved Initiative](https://www.improved-initiative.com/) D&D combat tracker Player View. Designed for high-readability display on TVs and laptops during tabletop gaming sessions.

## Project Structure
```
/
├── Additional Player View.css   # The main CSS theme file (paste into Improved Initiative Settings → Custom CSS)
├── index.html                   # Preview page demonstrating the theme with sample combat data
├── README.md                    # Short project description
└── replit.md                    # This file
```

## Tech Stack
- **Pure CSS** (no build system, no dependencies)
- **HTML** preview page for Replit display
- **Python 3** built-in HTTP server for serving static files (port 5000)

## Running the App
The workflow `Start application` runs:
```
python3 -m http.server 5000 --bind 0.0.0.0
```
This serves the static preview at port 5000.

## Usage
To use the CSS theme in Improved Initiative:
1. Open [improved-initiative.com](https://www.improved-initiative.com/)
2. Go to Settings → Custom CSS
3. Paste the contents of `Additional Player View.css`

## Design Tokens (CSS Variables)
All visual settings are configurable via CSS variables at the top of `Additional Player View.css`:
- Colors: `--text-main`, `--hp-green`, `--danger-red`, `--gold`, `--gold-light`
- Layout: `--panel-width`, `--row-height`, `--header-height`, etc.
- Grid columns: `--col-init`, `--col-portrait`, `--col-name`, `--col-hp`, `--col-tags`, `--col-reaction`
