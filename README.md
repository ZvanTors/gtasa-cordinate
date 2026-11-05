<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>UNCLES GTA-SA — Tactical Location Finder</title>
<meta name="description" content="A sleek, tactical-style coordinate mapper for Grand Theft Auto: San Andreas">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='48' fill='%23100c08'/%3E%3Cpath d='M50 10 L58 42 L90 50 L58 58 L50 90 L42 58 L10 50 L42 42 Z' fill='%23ff6a1a'/%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#100c08;
    --bg-soft:#171009;
    --surface:#1c140c;
    --surface-2:#241a10;
    --surface-3:#2e2113;
    --border:#33230f;
    --border-strong:#4a3419;
    --accent:#ff6a1a;
    --accent-hover:#ff8038;
    --accent-soft:rgba(255,106,26,.14);
    --accent-soft-strong:rgba(255,106,26,.30);
    --gold:#ffb454;
    --text:#f5ead9;
    --text-dim:#c2ab90;
    --text-faint:#8a745c;
    --danger:#ff6b62;
    --success:#8fdcae;
    --radius-sm:6px;
    --radius-md:10px;
    --radius-lg:18px;
    --shadow-md:0 8px 24px rgba(0,0,0,.35);
    --shadow-lg:0 20px 50px rgba(0,0,0,.55);
    --font-ui:'Segoe UI',system-ui,-apple-system,sans-serif;
    --font-display:'Rajdhani','Segoe UI',sans-serif;
    --font-mono:'JetBrains Mono','Consolas',monospace;
  }

  *{ box-sizing:border-box; margin:0; padding:0; }
  html{ scroll-behavior:smooth; }

  body{
    font-family:var(--font-ui);
    color:var(--text);
    background:
      radial-gradient(circle at 82% 15%, rgba(255,106,26,.09), transparent 45%),
      radial-gradient(circle at 8% 92%, rgba(255,180,84,.06), transparent 40%),
      linear-gradient(160deg,var(--bg),var(--bg-soft));
    min-height:100vh;
    line-height:1.7;
    font-size:16px;
  }

  ::-webkit-scrollbar{ width:10px; height:10px; }
  ::-webkit-scrollbar-track{ background:var(--bg-soft); }
  ::-webkit-scrollbar-thumb{ background:var(--border-strong); border-radius:5px; }
  ::-webkit-scrollbar-thumb:hover{ background:var(--accent); }
  *{ scrollbar-width:thin; scrollbar-color:var(--border-strong) transparent; }

  :focus-visible{ outline:2px solid var(--accent); outline-offset:3px; border-radius:4px; }

  .container{
    max-width:920px;
    margin:0 auto;
    padding:56px 28px 96px;
  }

  /* ---------- Hero ---------- */
  .hero{
    text-align:center;
    padding:32px 16px 52px;
    border-bottom:1px solid var(--border);
    margin-bottom:56px;
    position:relative;
  }

  .hero-mark{
    width:64px;
    height:64px;
    margin:0 auto 20px;
    color:var(--accent);
    filter:drop-shadow(0 0 18px rgba(255,106,26,.55));
    animation:float 4s ease-in-out infinite;
  }

  .hero-mark svg{ width:100%; height:100%; display:block; }

  @keyframes float{
    0%, 100%{ transform:translateY(0); }
    50%{ transform:translateY(-6px); }
  }

  .hero h1{
    font-family:var(--font-display);
    font-size:clamp(30px, 5.5vw, 48px);
    font-weight:700;
    letter-spacing:.08em;
    margin-bottom:14px;
    background:linear-gradient(135deg, var(--accent) 20%, var(--gold) 100%);
    -webkit-background-clip:text;
    background-clip:text;
    -webkit-text-fill-color:transparent;
    line-height:1.15;
  }

  .hero .tagline{
    font-size:clamp(14px, 2.2vw, 17px);
    color:var(--text-dim);
    margin-bottom:28px;
    max-width:600px;
    margin-left:auto;
    margin-right:auto;
  }

  .hero .tagline strong{ color:var(--text); }

  .hero em{
    color:var(--text-faint);
    font-size:13px;
    font-style:normal;
    letter-spacing:.04em;
    font-family:var(--font-mono);
    display:block;
    margin-top:8px;
  }

  /* ---------- Badges ---------- */
  .badges{
    display:flex;
    flex-wrap:wrap;
    gap:8px;
    justify-content:center;
    margin-bottom:22px;
  }

  .badge{
    display:inline-flex;
    align-items:center;
    gap:6px;
    padding:6px 13px;
    border-radius:999px;
    font-size:11.5px;
    font-weight:700;
    font-family:var(--font-mono);
    letter-spacing:.04em;
    border:1px solid var(--border-strong);
    background:var(--surface-2);
    color:var(--text-dim);
    text-transform:uppercase;
  }

  .badge.accent{ color:var(--accent); border-color:var(--accent-soft-strong); background:var(--accent-soft); }
  .badge.gold{ color:var(--gold); border-color:rgba(255,180,84,.3); background:rgba(255,180,84,.1); }

  /* ---------- Sections ---------- */
  section{ margin-bottom:64px; }

  h2{
    font-family:var(--font-display);
    font-size:clamp(22px, 3.4vw, 30px);
    font-weight:700;
    letter-spacing:.03em;
    margin-bottom:22px;
    color:var(--text);
    display:flex;
    align-items:center;
    gap:14px;
    padding-bottom:14px;
    border-bottom:1px solid var(--border);
  }

  h2::before{
    content:'';
    display:inline-block;
    width:4px;
    height:26px;
    background:linear-gradient(180deg, var(--accent), var(--gold));
    border-radius:2px;
    flex-shrink:0;
  }

  h3{
    font-family:var(--font-display);
    font-size:clamp(16px, 2.2vw, 19px);
    font-weight:700;
    letter-spacing:.03em;
    color:var(--gold);
    margin:28px 0 14px;
    text-transform:uppercase;
  }

  p{
    color:var(--text-dim);
    margin-bottom:16px;
    font-size:15.5px;
  }

  strong{ color:var(--text); font-weight:700; }
  em{ color:var(--gold); font-style:italic; }

  a{
    color:var(--accent);
    text-decoration:none;
    border-bottom:1px dotted var(--accent);
    transition:color .15s ease, border-color .15s ease;
  }
  a:hover{ color:var(--accent-hover); border-color:var(--accent-hover); }

  code{
    font-family:var(--font-mono);
    font-size:13px;
    background:var(--surface-2);
    color:var(--gold);
    padding:2px 7px;
    border-radius:5px;
    border:1px solid var(--border);
    white-space:nowrap;
  }

  /* ---------- Lists ---------- */
  ul, ol{
    color:var(--text-dim);
    padding-left:0;
    list-style:none;
    margin-bottom:18px;
  }

  ul li, ol li{
    position:relative;
    padding-left:28px;
    margin-bottom:10px;
    font-size:15.5px;
  }

  ul li::before{
    content:'▸';
    position:absolute;
    left:4px;
    top:0;
    color:var(--accent);
    font-weight:700;
  }

  ol{ counter-reset:item; }
  ol li{ padding-left:36px; counter-increment:item; }
  ol li::before{
    content:counter(item);
    position:absolute;
    left:0;
    top:3px;
    width:24px;
    height:24px;
    display:flex;
    align-items:center;
    justify-content:center;
    background:var(--accent-soft);
    color:var(--accent);
    border:1px solid var(--accent-soft-strong);
    border-radius:50%;
    font-size:11px;
    font-weight:700;
    font-family:var(--font-mono);
  }

  /* ---------- Table ---------- */
  .table-wrap{
    overflow-x:auto;
    border-radius:var(--radius-md);
    border:1px solid var(--border-strong);
    margin-bottom:22px;
    box-shadow:var(--shadow-lg);
  }

  table{
    width:100%;
    border-collapse:collapse;
    font-size:14.5px;
    min-width:520px;
  }

  thead{
    background:linear-gradient(180deg, var(--surface-2), var(--surface));
  }

  thead th{
    padding:13px 18px;
    text-align:left;
    font-family:var(--font-mono);
    font-weight:700;
    font-size:12px;
    letter-spacing:.06em;
    color:var(--gold);
    border-bottom:1px solid var(--border-strong);
    text-transform:uppercase;
  }

  tbody td{
    padding:12px 18px;
    border-bottom:1px solid var(--border);
    color:var(--text-dim);
    vertical-align:top;
  }

  tbody tr:last-child td{ border-bottom:none; }
  tbody tr:hover td{ background:rgba(255,106,26,.05); color:var(--text); }
  tbody td strong{ color:var(--text); }

  /* ---------- Code blocks ---------- */
  pre{
    background:var(--surface);
    border:1px solid var(--border-strong);
    border-radius:var(--radius-md);
    padding:20px 22px;
    overflow-x:auto;
    margin-bottom:22px;
    font-family:var(--font-mono);
    font-size:13px;
    line-height:1.75;
    color:var(--text);
    box-shadow:var(--shadow-lg);
    position:relative;
  }

  pre code{
    background:none;
    border:none;
    padding:0;
    color:var(--text);
    font-size:inherit;
    white-space:pre;
  }

  pre[data-lang]::before{
    content:attr(data-lang);
    position:absolute;
    top:9px;
    right:16px;
    font-size:10px;
    color:var(--text-faint);
    letter-spacing:.1em;
    text-transform:uppercase;
    font-weight:700;
  }

  /* ---------- Callout ---------- */
  .callout{
    background:var(--accent-soft);
    border-left:3px solid var(--accent);
    border-radius:0 var(--radius-md) var(--radius-md) 0;
    padding:16px 20px;
    margin-bottom:22px;
    font-size:14.5px;
    color:var(--text);
    line-height:1.8;
  }

  .callout.gold{
    background:rgba(255,180,84,.08);
    border-left-color:var(--gold);
  }

  .callout strong{ color:var(--accent); }
  .callout.gold strong{ color:var(--gold); }

  /* ---------- Preview block ---------- */
  .preview{
    background:linear-gradient(180deg, var(--surface-2), var(--surface));
    border:1px solid var(--border-strong);
    border-radius:var(--radius-lg);
    padding:26px;
    margin-bottom:22px;
    overflow-x:auto;
    box-shadow:var(--shadow-lg);
  }

  .preview pre{
    background:none;
    border:none;
    padding:0;
    margin:0;
    box-shadow:none;
    color:var(--gold);
    font-size:12px;
  }

  .preview pre::before{ display:none; }

  /* ---------- Color swatches ---------- */
  .swatches{
    display:grid;
    grid-template-columns:repeat(auto-fill, minmax(190px, 1fr));
    gap:12px;
    margin-bottom:22px;
  }

  .swatch{
    display:flex;
    align-items:center;
    gap:12px;
    background:var(--surface-2);
    border:1px solid var(--border);
    border-radius:var(--radius-md);
    padding:11px 14px;
    transition:border-color .2s ease, transform .2s ease;
  }

  .swatch:hover{ border-color:var(--accent); transform:translateY(-2px); }

  .swatch-box{
    width:36px;
    height:36px;
    border-radius:8px;
    flex-shrink:0;
    border:1px solid var(--border-strong);
    box-shadow:0 0 12px rgba(0,0,0,.4);
  }

  .swatch-info{ display:flex; flex-direction:column; min-width:0; }
  .swatch-name{ font-size:12px; font-weight:700; color:var(--text); font-family:var(--font-mono); }
  .swatch-value{ font-size:11px; color:var(--text-faint); font-family:var(--font-mono); }

  /* ---------- Footer ---------- */
  footer{
    text-align:center;
    padding-top:48px;
    border-top:1px solid var(--border);
    margin-top:80px;
    color:var(--text-faint);
    font-size:14px;
  }

  footer .footer-brand{
    font-family:var(--font-display);
    font-size:20px;
    font-weight:700;
    letter-spacing:.08em;
    color:var(--accent);
    margin-bottom:10px;
  }

  footer p{ font-size:13.5px; margin-bottom:10px; }
  footer .heart{ color:var(--accent); display:inline-block; }

  /* ---------- Responsive ---------- */
  @media (max-width:640px){
    .container{ padding:28px 18px 64px; }
    .hero{ padding:16px 8px 40px; margin-bottom:40px; }
    section{ margin-bottom:44px; }
    h2{ font-size:22px; }
    p, ul li, ol li{ font-size:14.5px; }
    pre{ padding:16px 18px; font-size:12px; }
    .preview{ padding:16px; }
    .preview pre{ font-size:10px; }
  }

  @media (prefers-reduced-motion:reduce){
    *{ transition-duration:.001ms !important; animation-duration:.001ms !important; }
    html{ scroll-behavior:auto; }
  }
</style>
</head>
<body>

<div class="container">

  <!-- ================= HERO ================= -->
  <header class="hero">
    <div class="hero-mark">
      <svg viewBox="0 0 24 24" aria-hidden="true">
        <path d="M12 2L14 10L22 12L14 14L12 22L10 14L2 12L10 10Z" fill="currentColor"/>
      </svg>
    </div>

    <h1>UNCLES GTA-SA</h1>
    <p class="tagline">
      A sleek, tactical-style coordinate mapper for <strong>Grand Theft Auto: San Andreas</strong>
    </p>

    <div class="badges">
      <span class="badge accent">HTML5</span>
      <span class="badge accent">CSS3</span>
      <span class="badge accent">JavaScript</span>
      <span class="badge gold">MIT License</span>
      <span class="badge">Zero Dependencies</span>
      <span class="badge">Single File</span>
    </div>

    <em>Persian-first · RTL · No build step · Portable deployment</em>
  </header>

  <!-- ================= OVERVIEW ================= -->
  <section id="overview">
    <h2>✨ Overview</h2>
    <p>
      <strong>UNCLES GTA-SA</strong> is a lightweight, single-file web application that lets you plot,
      visualize, and manage coordinates on the San Andreas map with surgical precision. Built with a
      <strong>tactical HUD aesthetic</strong> — dark surfaces, glowing orange markers, and monospaced
      telemetry — it's designed for players, modders, and speedrunners who need to locate anything
      in the state of San Andreas in seconds.
    </p>
    <p>
      Whether you're hunting for a specific pickup, marking stunt jumps, or documenting a route, this
      tool turns raw <code>x, y, z</code> coordinates into an interactive, pannable, zoomable map.
    </p>
  </section>

  <!-- ================= FEATURES ================= -->
  <section id="features">
    <h2>🎯 Features</h2>
    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Feature</th><th>Description</th></tr>
        </thead>
        <tbody>
          <tr><td>📍 <strong>Batch Coordinate Parsing</strong></td><td>Paste dozens of <code>x, y, z</code> lines at once — each line becomes a point</td></tr>
          <tr><td>🎨 <strong>Custom Labels</strong></td><td>Attach human-readable names to any coordinate</td></tr>
          <tr><td>🖱️ <strong>Click-to-Add</strong></td><td>Toggle "pick mode" and click directly on the map to drop a point</td></tr>
          <tr><td>🔍 <strong>Pan &amp; Zoom</strong></td><td>Smooth drag-to-pan, cursor-centered zoom, and quick reset</td></tr>
          <tr><td>🧭 <strong>Live Coordinate HUD</strong></td><td>Real-time readout of the position under your cursor</td></tr>
          <tr><td>📐 <strong>Coordinate Grid</strong></td><td>Toggleable 500-unit reference grid with labels</td></tr>
          <tr><td>🏷️ <strong>Smart Labels</strong></td><td>Optional labels next to every point for at-a-glance reading</td></tr>
          <tr><td>🚨 <strong>Out-of-Bounds Detection</strong></td><td>Points outside the map bounds are flagged with a golden dashed ring</td></tr>
          <tr><td>📋 <strong>One-Click Copy</strong></td><td>Copy all plotted coordinates to clipboard in GTA-ready format</td></tr>
          <tr><td>🎛️ <strong>Adjustable Marker Size</strong></td><td>Slider to scale point radius from 4px to 34px</td></tr>
          <tr><td>🌐 <strong>Fullscreen Mode</strong></td><td>Immersive map-first experience</td></tr>
          <tr><td>📱 <strong>Fully Responsive</strong></td><td>Mobile drawer panel · desktop sidebar · touch-optimized</td></tr>
          <tr><td>🌙 <strong>Tactical Dark Theme</strong></td><td>Orange-on-charcoal HUD aesthetic with glassmorphic surfaces</td></tr>
        </tbody>
      </table>
    </div>
  </section>

  <!-- ================= PREVIEW ================= -->
  <section id="preview">
    <h2>📸 Preview</h2>
    <div class="preview">
<pre>
┌──────────────────────────────────────────────────────┐
│  ✦ UNCLES [GTA-SA]          📍 12 نقاط     ⛶        │
├──────────────────────────────────────────────────────┤
│  ┌───────────────┐  ┌──────────────────────────────┐ │
│  │ ورودی موقعیت‌ها │  │  ⌜                        ⌝  │ │
│  │               │  │      🗺️  SAN ANDREAS MAP       │ │
│  │ 1000, -400,0  │  │                              │ │
│  │ 2450, 1100,0  │  │   ●  ●        ●              │ │
│  │ 300, 800, 12  │  │        ⚡                     │ │
│  │               │  │                  ●  ●        │ │
│  │ [رسم] [پاک]   │  │                              │ │
│  │               │  │  ═══ 1000, -400, 0 ═══      │ │
│  └───────────────┘  │  ⌞                        ⌟  │ │
│                     └──────────────────────────────┘ │
└──────────────────────────────────────────────────────┘
</pre>
    </div>
  </section>

  <!-- ================= COORDINATE FORMAT ================= -->
  <section id="format">
    <h2>📝 Coordinate Format</h2>
    <p>
      Each line in the input field represents <strong>one point</strong>. The parser is tolerant of
      common formatting quirks.
    </p>

    <h3>Accepted formats</h3>
<pre data-lang="text"><code>x, y, z
x, y, z, label
position : x, y, z</code></pre>

    <h3>Examples</h3>
<pre data-lang="text"><code>1200, -400, 0
2450, 1100, 15.5
-1800, 700, 0, Grove Street
position : 1500, -600, 0, Ammunation</code></pre>

    <div class="callout">
      <strong>Notes</strong><br>
      • <code>z</code> is optional and defaults to <code>0</code><br>
      • Commas, whitespace, and the optional <code>position :</code> prefix are all handled<br>
      • Labels may contain spaces<br>
      • Points outside the map bounds are still plotted but visually flagged
    </div>
  </section>

  <!-- ================= GETTING STARTED ================= -->
  <section id="getting-started">
    <h2>🚀 Getting Started</h2>
    <p>No build step. No npm. No server required.</p>

<pre data-lang="bash"><code># Clone or download
git clone https://github.com/your-name/uncles-gta-sa.git

# Open in your browser
cd uncles-gta-sa
open index.html      # macOS
xdg-open index.html  # Linux
start index.html     # Windows</code></pre>

    <p>
      Or simply <strong>double-click <code>index.html</code></strong> — the entire app
      (including the map) ships as a single self-contained file.
    </p>
  </section>

  <!-- ================= HOW TO USE ================= -->
  <section id="how-to-use">
    <h2>🎮 How to Use</h2>
    <ol>
      <li><strong>Paste coordinates</strong> into the textarea (one point per line).</li>
      <li>Hit <strong>«رسم نقاط»</strong> (<em>Render Points</em>) to plot them on the map.</li>
      <li><strong>Drag</strong> to pan · <strong>scroll / +− buttons</strong> to zoom · <strong>reset button</strong> to recenter.</li>
      <li>Toggle <strong>«افزودن با کلیک روی نقشه»</strong> to enter pick mode and click anywhere to drop a new point.</li>
      <li>Enable <strong>labels</strong>, <strong>grid</strong>, and adjust <strong>marker size</strong> from the control panel.</li>
      <li>Use <strong>«کپی همه»</strong> to copy every plotted coordinate back to your clipboard.</li>
      <li>On mobile, tap the floating <strong>FAB</strong> to open the control drawer.</li>
    </ol>
  </section>

  <!-- ================= DESIGN SYSTEM ================= -->
  <section id="design">
    <h2>🎨 Design System</h2>

    <div class="swatches">
      <div class="swatch"><span class="swatch-box" style="background:#100c08;"></span><div class="swatch-info"><span class="swatch-name">--bg</span><span class="swatch-value">#100c08</span></div></div>
      <div class="swatch"><span class="swatch-box" style="background:#1c140c;"></span><div class="swatch-info"><span class="swatch-name">--surface</span><span class="swatch-value">#1c140c</span></div></div>
      <div class="swatch"><span class="swatch-box" style="background:#ff6a1a;"></span><div class="swatch-info"><span class="swatch-name">--accent</span><span class="swatch-value">#ff6a1a</span></div></div>
      <div class="swatch"><span class="swatch-box" style="background:#ffb454;"></span><div class="swatch-info"><span class="swatch-name">--gold</span><span class="swatch-value">#ffb454</span></div></div>
      <div class="swatch"><span class="swatch-box" style="background:#f5ead9;"></span><div class="swatch-info"><span class="swatch-name">--text</span><span class="swatch-value">#f5ead9</span></div></div>
      <div class="swatch"><span class="swatch-box" style="background:#ff6b62;"></span><div class="swatch-info"><span class="swatch-name">--danger</span><span class="swatch-value">#ff6b62</span></div></div>
      <div class="swatch"><span class="swatch-box" style="background:#8fdcae;"></span><div class="swatch-info"><span class="swatch-name">--success</span><span class="swatch-value">#8fdcae</span></div></div>
    </div>

    <h3>Typography</h3>
    <ul>
      <li><code>Vazirmatn</code> — Persian UI text</li>
      <li><code>Rajdhani</code> — Tactical display headings</li>
      <li><code>JetBrains Mono</code> — Coordinates &amp; telemetry</li>
    </ul>

    <p>
      The result is a <strong>HUD-forward, amber-lit aesthetic</strong> that feels at home inside a
      GTA loading screen.
    </p>
  </section>

  <!-- ================= TECHNICAL HIGHLIGHTS ================= -->
  <section id="technical">
    <h2>🧠 Technical Highlights</h2>
    <ul>
      <li><strong>Zero dependencies</strong> — no frameworks, no bundlers, no build pipeline</li>
      <li><strong>Embedded map</strong> — the San Andreas map is inlined as a Base64 WebP, keeping the app fully portable</li>
      <li><strong>CSS-variable theming</strong> — swap the palette by editing <code>:root</code></li>
      <li><strong>Transform-based pan/zoom</strong> — GPU-accelerated via <code>will-change: transform</code></li>
      <li><strong>Accessible inputs</strong> — <code>:focus-visible</code> rings, ARIA labels, and semantic markup</li>
      <li><strong>RTL-first</strong> — built for Persian by default, with <code>direction: ltr</code> scoped to numeric fields</li>
      <li><strong>Reduced-motion support</strong> — respects <code>prefers-reduced-motion</code></li>
    </ul>
  </section>

  <!-- ================= RESPONSIVE ================= -->
  <section id="responsive">
    <h2>📱 Responsive Behavior</h2>
    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Breakpoint</th><th>Layout</th></tr>
        </thead>
        <tbody>
          <tr><td><code>&lt; 880px</code></td><td>Slide-in drawer panel + floating action button</td></tr>
          <tr><td><code>≥ 880px</code></td><td>Persistent sidebar with map on the right</td></tr>
          <tr><td><code>&lt; 420px</code></td><td>Compact header, hidden stat labels, condensed HUD</td></tr>
        </tbody>
      </table>
    </div>
  </section>

  <!-- ================= PROJECT STRUCTURE ================= -->
  <section id="structure">
    <h2>🗂️ Project Structure</h2>
<pre data-lang="text"><code>uncles-gta-sa/
└── index.html      # The entire application</code></pre>
    <p>That's it. Everything — HTML, CSS, JavaScript, and the map image — lives in one file.</p>
  </section>

  <!-- ================= CONTRIBUTING ================= -->
  <section id="contributing">
    <h2>🤝 Contributing</h2>
    <p>Contributions, bug reports, and feature requests are welcome.</p>
    <ol>
      <li>Fork the repo</li>
      <li>Create a branch: <code>git checkout -b feature/my-idea</code></li>
      <li>Commit: <code>git commit -m "Add my idea"</code></li>
      <li>Push: <code>git push origin feature/my-idea</code></li>
      <li>Open a Pull Request</li>
    </ol>
  </section>

  <!-- ================= LICENSE ================= -->
  <section id="license">
    <h2>📄 License</h2>
    <p>Released under the <strong>MIT License</strong> — free to use, modify, and share.</p>
    <div class="callout gold">
      <strong>Disclaimer</strong><br>
      <em>Grand Theft Auto: San Andreas</em> and all related assets are property of
      <strong>Rockstar Games</strong>. This project is an unofficial fan tool and is not affiliated
      with or endorsed by Rockstar Games or Take-Two Interactive.
    </div>
  </section>

  <!-- ================= FOOTER ================= -->
  <footer>
    <div class="footer-brand">UNCLES GTA-SA</div>
    <p><strong>Built for the streets of Los Santos.</strong> 🟠</p>
    <p>If this tool helped you find your way, drop a <span class="heart">⭐</span> on the repo.</p>
  </footer>

</div>

</body>
</html>
