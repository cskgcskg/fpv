# 🚁 FPV Drone Simulator

A realistic, lightweight **FPV (first-person-view) drone freestyle simulator** that runs entirely in the browser — no build step, no installs, no external assets. Built with vanilla JavaScript and [Three.js](https://threejs.org/).

![Status](https://img.shields.io/badge/status-active-brightgreen) ![Engine](https://img.shields.io/badge/three.js-r128-orange) ![Build](https://img.shields.io/badge/build-single--file%20%2B%20modular-blue) ![License](https://img.shields.io/badge/license-MIT-green)

The focus is **flight feel first**: a physically-grounded acro flight model with real momentum and inertia, tuned to sit close to sims like *Liftoff* / *The Zone*, wrapped in a stylised low-poly world.

---

## 🎮 Try it

Every build is a static file or static site — nothing to install.

| Build | What it is | How to run |
|-------|-----------|-----------|
| **Trippy Plains v4** | Latest freestyle map. Big open field, 1× / 2× / 3× equipment, dive-through towers, curving tunnels, in-flight tuning. | Open `Drone sim/Trippy Plains/trippy-plains-v4.html` |
| **Single-file sim** | The full-featured original — every world, all quads, scoring, easter eggs, in one HTML file. | Open `Drone sim/index-32.html` |
| **Multi-file sim** | Same engine split into ES modules, ready to host on GitHub Pages. | Serve the `Drone sim/Multi file FPV sim/` folder (see below) |

> ⚠️ **Open the files directly in a desktop browser** (Chrome recommended). Don't run them inside an embedded preview/iframe — browsers block the Gamepad API in frames, so a controller won't be detected there.

---

## ✨ Features

- **Realistic acro flight model** — accel-limited rate controller with true rotational *and* linear inertia. The quad carries momentum and has weight, and it's stable by design.
- **Deep physics** — battery voltage sag (punch fades under load), wind + gusts + turbulence, propwash oscillation, vortex-ring-state on hard descents, ground effect, asymmetric motor spool.
- **Solid-object collisions** — crash, bounce, or rest depending on impact severity, plus a panic-recover key to level out after a tumble.
- **Multiple quads** — 5″ freestyle, 3.5″ cinewhoop, 5″ racer, 2.5″ sub-250, and a dedicated **THE ZONE** 5″ profile tuned from real-sim Betaflight "Actual" rates — each with distinct mass, power, rates and handling.
- **Flight modes** — Acro (rate) and Angle (self-levelling), toggle in flight.
- **In-flight tuning panel (TAB)** — snappiness (rate + snap), rate **PID (P/I/D)**, camera angle, and floor/background brightness, with the keyboard control reference built into the same panel.
- **Several worlds to fly** — a freestyle park and bando, golden-hour scenery, and the **Trippy Plains** open freestyle field inspired by *The Zone*.
- **DJI / gamepad support** — auto-detect, guided stick calibration remembered between sessions, plus full keyboard controls.

---

## 🕹️ Controls

| Key | Action |
|-----|--------|
| `W` / `S` | Throttle up / down |
| `A` / `D` | Yaw left / right |
| `↑` / `↓` | Pitch forward / back |
| `←` / `→` | Roll left / right |
| `SPACE` | Arm / disarm |
| `R` | Reset to spawn |
| `X` | Level / recover |
| `M` | Acro ↔ Angle mode |
| `1` – `5` | Swap quad |
| `[` / `]` | Camera angle down / up |
| `TAB` | Controls & tuning panel |

A gamepad (e.g. DJI RC) is auto-detected on the setup screen — move a stick to wake it.

---

## 🗺️ Trippy Plains map versions

The Trippy Plains freestyle field has been iterated as standalone single files:

- **v1** — first open field inspired by *The Zone* screenshots.
- **v2** — open dive-through scaffold towers, curving square **tunnels** to fly through horizontally, darker floor, and the in-flight tuning panel.
- **v3** — every piece of equipment in **three size tiers** (original 1× inner ring, 2× mid ring, 3× outer ring) plus camera-angle controls.
- **v4** — `TAB` opens a single panel showing the **keyboard controls and the tuning sliders together**, matching the multi-file project's style.

---

## 🚀 Deploy the multi-file build to GitHub Pages

The modular version under `Drone sim/Multi file FPV sim/` uses native ES modules with an import map (no bundler), so it can be hosted as-is.

1. Put the contents of `Multi file FPV sim/` at the root of a repo (or a `/docs` folder).
2. The included `.nojekyll` file keeps GitHub Pages from stripping the `src/` and `assets/` folders.
3. In your repo: **Settings → Pages → Build and deployment → Deploy from a branch**, pick the branch and folder.
4. Open the published URL and fly.

To run it locally (modules need a server, not `file://`):

```bash
cd "Drone sim/Multi file FPV sim"
python3 -m http.server 8000
# then open http://localhost:8000
```

### Project structure

```
Multi file FPV sim/
├── index.html        # markup, CSS, import map, loading screen
├── src/
│   ├── main.js       # Sim loop, setup, scoring, UI wiring
│   ├── config.js     # G, quad profiles (mass, TWR, rates, PID)
│   ├── physics.js    # flight model, battery, wind, collisions
│   ├── input.js      # keyboard + gamepad
│   ├── world.js      # scene build, maps, post-processing
│   ├── state.js      # shared env + colliders
│   └── assets.js     # optional HDRI / glTF loaders
├── assets/
└── .nojekyll
```

---

## 🛠️ Tech

- **Three.js r128** — UMD global for single files, ESM `three@0.128.0` via import map for the modular build.
- **Flight model** — `thrust = TWR · mass · g · throttle^k`, anisotropic quadratic drag, quaternion attitude, fixed-timestep accumulator, Betaflight "Actual" rate curves.
- **Collisions** — AABB colliders built from meshes flagged `userData.solid`, resolved by impact severity.
- **No dependencies to install** — Three.js is loaded from a CDN.

---

## 📋 Requirements

- A modern desktop browser (Chrome recommended; Safari works but its Gamepad API is less reliable).
- Optional: a USB/Bluetooth gamepad or DJI controller for proper stick feel.

---

## 📄 License

MIT — free to use, modify, and share.
