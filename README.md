# 🗺️ UNCLES · GTA-SA Location Finder

**Tactical coordinate plotter for Grand Theft Auto: San Andreas**

A clean, fast, and fully self-contained web tool for plotting, managing, and exporting in-game coordinates on the San Andreas map.  
Perfect for roleplay servers, mission creators, and anyone who needs precise location tracking.

---

## ✨ Features

### 🗺️ Interactive Map
- Smooth pan & zoom (mouse, trackpad, and touch)
- Pinch-to-zoom support on mobile
- Fullscreen mode
- Live coordinate HUD under the cursor

### 📍 Point Management
- Paste multiple coordinates at once
- Flexible format: `x, y` or `x, y, z` + optional label
- Color-coded markers with hover tooltips
- Adjustable marker size
- Optional labels on the map
- Out-of-bounds points are clamped and clearly marked

### ⚡ Productivity Tools
- Click-to-add mode (pick positions directly on the map)
- One-click copy of all coordinates
- Coordinate grid overlay (every 500 units)
- Quick Locate & Delete actions per point

### 📱 User Experience
- Fully responsive design
- Mobile-friendly side drawer
- Dark tactical theme
- Persian UI with proper RTL support
- Zero dependencies — single HTML file

---

## 🚀 Quick Start

1. Download or clone the repository
2. Open `index.html` in any modern browser
3. Done.

No build step. No server. No installation.

The map is embedded as a base64 WebP, so the file is completely self-contained.

---

## 📌 How to Use

### Input Format

```txt
1200, -400
1500.5, 800, 12
-2100, 950, 0, Grove Street
2500, -1800, 5, Airport Runway
```

- **X** and **Y** are required  
- **Z** is optional (defaults to `0`)  
- Anything after the numbers becomes a label

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

## 🧭 Coordinate System

The map covers the classic San Andreas world bounds:

```txt
X, Y  ∈  [-3000 … 3000]
```

Points outside this range are still accepted.  
They are drawn on the nearest edge and show how far outside the map they lie.

---

## 🛠️ Tech Stack

- Pure HTML / CSS / Vanilla JavaScript
- No frameworks, no build tools
- Modern CSS (custom properties, flex/grid, backdrop-filter)
- Pointer Events + Wheel API
- Embedded WebP map image

---

## 🌐 Browser Support

Works in all modern browsers:

- ✅ Chrome / Edge / Brave  
- ✅ Firefox  
- ✅ Safari (desktop & iOS)

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

**UNCLES · GTA-SA**  
Tactical location finder for San Andreas 🔥
