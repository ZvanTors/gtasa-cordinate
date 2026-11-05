# UNCLES · GTA-SA Location Finder

**Tactical coordinate plotter for Grand Theft Auto: San Andreas**

A lightweight, self-contained web tool for visualizing, managing, and exporting in-game coordinates on the San Andreas map. Built for roleplay servers, mission designers, and anyone who needs precise location tracking.

---

## Features

- **Interactive Map**
  - Full San Andreas map with smooth pan & zoom (mouse, trackpad, and touch)
  - Pinch-to-zoom and drag support on mobile
  - Fullscreen mode

- **Coordinate Input**
  - Paste multiple positions at once (one per line)
  - Flexible format: `x, y` or `x, y, z` + optional label
  - Real-time validation with clear error feedback

- **Point Management**
  - Color-coded markers with hover tooltips
  - Adjustable marker size
  - Optional labels on the map
  - Out-of-bounds points are clamped to the edge and clearly marked with distance
  - Quick “Locate” and “Delete” actions per point

- **Productivity Tools**
  - Click-to-add mode (pick positions directly on the map)
  - Live coordinate HUD under the cursor
  - One-click copy of all coordinates
  - Coordinate grid overlay (every 500 units)

- **UX**
  - Fully responsive (desktop + mobile drawer)
  - Dark tactical theme
  - Persian UI with proper RTL support
  - Zero dependencies — single HTML file

---

## Quick Start

1. Download or clone the repository.
2. Open `index.html` in any modern browser.
3. That’s it. No build step, no server required.

The map image is embedded as a base64 WebP, so the file is completely self-contained.

---

## Usage

### Input Format

```
1200, -400
1500.5, 800, 12
-2100, 950, 0, Grove Street
2500, -1800, 5, Airport Runway
```

- At least **X** and **Y** are required.
- **Z** is optional (defaults to `0`).
- Anything after the numbers is treated as a label.

### Controls

| Action                    | How                                      |
|---------------------------|------------------------------------------|
| Pan                       | Click + drag / touch drag                |
| Zoom                      | Mouse wheel / pinch / zoom buttons       |
| Reset view                | Center button                            |
| Add point by clicking     | Enable “افزودن با کلیک روی نقشه”         |
| Toggle labels / grid      | Switches in the side panel               |
| Copy all points           | Button next to the points list           |
| Copy current HUD coords   | Button in the bottom coordinate bar      |

---

## Coordinate System

The map covers the classic San Andreas world bounds:

```
X, Y  ∈  [-3000 … 3000]
```

Points outside this range are still accepted. They are drawn on the nearest edge and display how far outside the map they lie.

---

## Tech Stack

- Pure HTML / CSS / Vanilla JavaScript
- No frameworks, no build tools
- Modern CSS (custom properties, flex/grid, backdrop-filter)
- Pointer Events + Wheel API for interaction
- Embedded WebP map image

---

## Browser Support

Works in all evergreen browsers:

- Chrome / Edge / Brave
- Firefox
- Safari (desktop & iOS)

---

## License

MIT License — feel free to use, modify, and distribute.

---

**UNCLES · GTA-SA**  
Tactical location finder for San Andreas
