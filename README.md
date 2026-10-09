# Floor Planner

An English-only, purely front-end interior/floor-plan design tool: place furniture on a 2D SVG plan, demolish or modify walls, take measurements, then switch to a Three.js 3D scene for bird's-eye views or first-person walkthrough. The whole app is a single `index.html`, no build step.

Based on [wy51ai/floorplan-3d](https://github.com/wy51ai/floorplan-3d) (MIT), converted to English-only UI.

## Features

**2D plan**
- Original floor plan displayed at 1:60 / 1:100 scale, dimensions in mm
- Drag in 60+ furniture/appliance items from the library (bedroom, living, dining/kitchen, bathroom, appliances, study/leisure)
- Move, rotate (Shift for free angle), resize, auto-snap to walls
- Measure tool (snaps to nearby walls, Shift locks horizontal/vertical)
- Demolish/modify non-load-bearing walls; load-bearing walls marked separately
- Layer toggles: dimensions, room names, furniture, grid, load-bearing walls

**3D scene**
- Bird's-eye, oblique, and top-down views; click a room in the list to fly to it
- Walkthrough mode: WASD + mouse on desktop, virtual joystick on touch; click doors to open/close
- Full-height / cutaway wall toggle, sun-time slider, night lighting
- Detailed furniture models: cabinet door seams and handles, upholstered headboards, metallic and ceramic materials with environment reflections
- Select and drag furniture in 3D too, synced live with the 2D plan

**Plans and stats**
- Automatic per-room area and total usable-area stats
- Change flooring materials per room (wood, tile, marble, terrazzo, carpet, etc.) with +5% waste cost estimation
- Undo / redo, plan auto-saved in browser localStorage
- Export PNG, export / import plan JSON

## Quick start

```
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open `index.html` in a browser. Three.js loads from jsDelivr CDN, so the 3D scene needs a network connection on first load.

## Shortcuts

| Key | Action |
| --- | --- |
| `T` | Toggle 2D / 3D |
| `V` / `M` / `X` | Select / Measure / Demolish-wall tools |
| `R` / `Shift+R` | Rotate selection 90° CW / CCW |
| `Delete` / `Backspace` | Delete selection |
| `Ctrl/⌘ + D` | Duplicate selection |
| `Ctrl/⌘ + Z`, `Ctrl/⌘ + Shift + Z` | Undo, redo |
| `F` | Fit to window |
| `+` / `-` | Zoom in / out |
| `[` / `]` | Toggle left library / right panel |
| `Shift + F` | Fullscreen |
| `Esc` | Cancel current action |
| Walkthrough: `WASD` / arrows, `Shift`, `E` | Move, walk fast, toggle doors |

## Tech stack

- Vanilla HTML / CSS / JavaScript, no framework, no build step
- 2D plan drawn with SVG
- 3D scene with [Three.js](https://threejs.org/) r160 (OrbitControls, PointerLockControls, RoundedBoxGeometry, RoomEnvironment, CSS2DRenderer)
- Data saved in `localStorage`

## Custom floor plan

Plan data lives inside `index.html`:

- `ROOMS`: room polygons, names, default flooring
- `WALLS` / `WINS`: walls and window openings
- `MATS`: flooring material names and unit prices
- `LIB`: furniture library (type, name, default sizes, colors)
- `buildFurniture()`: 3D models for each furniture type

Note: built-in names in the source data are stored in Chinese and shown through an English name map (namesake `NAMES_EN` map + `data-en` attributes) so the UI stays fully English; anything you rename yourself displays as typed.

## License

[MIT](LICENSE)
