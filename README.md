# 🚁 FPV Drone Simulator

A realistic, lightweight **FPV (first-person-view) drone freestyle simulator** that runs entirely in the browser from a **single HTML file** — no build step, no installs, no external assets. Built with vanilla JavaScript and [Three.js](https://threejs.org/).

![Status](https://img.shields.io/badge/status-active-brightgreen) ![Build](https://img.shields.io/badge/build-single--file-blue) ![Engine](https://img.shields.io/badge/three.js-r128-orange) ![License](https://img.shields.io/badge/license-MIT-green)

The focus is **flight feel first**: a physically-grounded acro flight model with real momentum and inertia, tuned to sit close to sims like *Liftoff* / *The Zone*, wrapped in a stylised low-poly world with a hand-written post-processing pipeline.

> **Latest build:** `index-32.html` — just open it in a desktop browser and fly.

---

## ✨ Features

- **Realistic acro flight model** — accel-limited rate controller with true rotational *and* linear inertia (the quad carries momentum and has weight). Stable by design.
- **Deep physics** — battery voltage sag (punch fades under load), wind + gusts + turbulence, propwash oscillation, vortex-ring-state on hard descents, ground effect, asymmetric motor spool.
- **Solid-object collisions** — crash, bounce, or rest depending on impact severity, plus a panic-recover key to level out after a tumble.
- **4 quads** — Mario 5 (5″ freestyle), Bee 35 (3.5″ cinewhoop), Race X (5″ racer), Wasp (2.5″ sub-250) — each with distinct mass, power, rates and handling.
- **Flight modes** — Acro (rate) and Angle (self-levelling), toggle in flight.
- **Full tuning panel** — power, rates, snap, mass/inertia, drag, throttle response, gravity, **rate PID (P/I/D)**, expo, roll sensitivity, camera tilt, shake, and post-FX — with **save/load presets per quad** and an in-app explainer.
- **Graphics (Road A)** — custom post-processing: **bloom, motion blur, colour grade, vignette**, plus **image-based lighting** and **procedural normal-map surface detail**. Soft shadows, day / golden-hour / night cycle, gradient sky, drifting clouds, mountains, water, weather sway.
- **A world to fly** — freestyle park (ramps, rails, funboxes, weave pillars, quarter-pipe), an abandoned **bando** shell with fly-through gaps, a **halfpipe**, spin pylons with X-tops, square gates, glowing torus gates, a dragon longship on an S-river, a homestead with people/dog/llamas/cats/cheetahs/koalas, golden towers, hot-air balloons, a rainbow, and a giant 3D sign.
- **Freestyle trick scoring** — flips, rolls, spins and airtime build a score with on-screen popups.
- **DJI controller support** — gamepad auto-detect, guided stick calibration that's **remembered between sessions**, plus full keyboard controls.
- **Easter eggs** — a few hidden surprises. Try the classic Konami code, and keep an eye on the sky. 👀

---

## 🚀 Quick start

1. Download the repo (or just the latest `index-NN.html`).
2. **Double-click the file to open it directly in a desktop browser** (Chrome recommended).
3. Pick a quad, choose **Keyboard** or **Controller**, and fly.

> ⚠️ **Open the file directly** — do not run it inside an embedded preview/iframe. Browsers block the Gamepad API in frames, so a controller won't be detected there.

No server required — it's a static file.

---

## 🎮 Controls

### Keyboard (Mode 2 layout)

| Key | Action |
|-----|--------|
| `W` / `S` | Throttle up / down (hold & release to hold) |
| `A` / `D` | Yaw left / right |
| `↑` / `↓` | Pitch forward / back |
| `←` / `→` | Roll left / right |
| `SPACE` | Arm / disarm |
| `R` | Reset position |
| `X` | Level / recover (panic) |
| `M` | Acro ⇄ Angle mode |
| `V` | Wind on / off |
| `N` | Day / Golden / Night |
| `[` / `]` | Camera tilt down / up |
| `1`–`4` | Swap quad |
| `TAB` | Tuning panel |
| `G` | Hide / show the controls legend |
| `H` | Back to setup |

### DJI / generic controller

Power on the controller, plug in (USB-C → USB-A), open the file in Chrome, then **move a stick** so the browser wakes it. Hit **Calibrate Sticks** once and it's **saved for next time** — after that just press **Fly · Controller**. Manual axis remap/invert is also available.

---

## 🔧 Tuning

Press **`TAB`** in flight to open the tuning panel. Everything is live, defaults are sensible, and you can **Save / Load / Default** per quad.

| Parameter | What it does |
|-----------|--------------|
| **TWR** | Power & punch (thrust-to-weight). |
| **Rate** | Top rotation speed (°/s). |
| **Snap** | How fast it reaches that rate (twitch vs. rotational weight). |
| **Mass / inertia** | Heavier = carries momentum, glides, harder to stop. |
| **Drag** | Air resistance — lower = faster & floatier, higher = planted. |
| **Throttle resp** | Motor spool lag — lower = punchier vertical. |
| **Gravity** | Fall strength (9.81 = real). Raise if it feels floaty. |
| **P / I / D** | Rate PID — stiffness / steady-state trim / damping. |
| **Roll sensitivity** | Roll rate relative to pitch. |
| **Expo** | Softens stick centre for fine control. |
| **Bloom / Motion blur / Vignette** | Post-FX intensities. |

**Recipes:** more inertia → Mass ↑ + Drag ↓ · snappier → Rate ↑ & Snap ↑ · smoother → D ↑ and Expo ↑.

---

## 🧠 How the flight model works

Rather than simulating a full PID loop against a blade-element thrust model (fragile and easy to make unstable), this sim uses the approach proven in good acro sims:

- **Rotation:** stick → target body **rate**; an *accel-limited* controller drives the actual rate toward it. The acceleration limit gives genuine rotational inertia (flips have weight; you must stop them) while staying unconditionally stable.
- **Thrust:** collective thrust along the body-up axis, `thrust = TWR · m · g · throttle²`, so hover sits at a realistic ~33–46% stick.
- **Translation:** gravity + anisotropic quadratic aerodynamic drag, integrated with quaternion attitude at a fixed timestep.
- On top: battery sag scales thrust, wind acts via relative airspeed, VRS/propwash add disturbance, and collisions resolve against axis-aligned obstacle boxes.

The result is a quad that hovers around 40% throttle, punches hard, carries momentum through lines, drops when you chop throttle, and recovers cleanly.

---

## 🖼️ Graphics

All rendering is hand-rolled in Three.js with **no external assets**:

- **Post-processing pipeline** (custom, single-file): bright-pass → separable Gaussian **bloom**, temporal **motion blur**, **colour grade** + **vignette**, with correct linear→sRGB output. MSAA preserved via a multisample render target on WebGL2.
- **Image-based lighting** from a procedural sky for believable PBR reflections.
- **Procedural normal maps** generated at load for surface micro-relief.
- Soft shadow mapping, ACES tone mapping, gradient sky + sun/moon, day/night, fog, animated water, wind-driven foliage.

---

## 🗺️ Roadmap

- **Road A (done):** push browser Three.js as far as it goes — post-FX, IBL, procedural PBR detail. Roughly the ceiling without an art pipeline.
- **Road B (future):** to truly rival a commercial sim, the presentation would move to a native engine (Unreal 5 / Unity) with **authored assets** (textured models, real environments). The flight-physics math here ports directly — it's the genuinely hard, reusable part.

---

## 📦 Version history (highlights)

Every iteration is kept (`index-6.html` → `index-32.html`) so you can compare or roll back.

| Version | Highlights |
|---------|-----------|
| v6–v7 | Stable rebuild of the flight model; deep physics (battery, wind, VRS, propwash, angle mode) |
| v8–v13 | Graphics passes: shadows, scenery, wildlife, golden hour, day/night |
| v14–v16 | Dragon river/boat, more birds, S-river, blue water |
| v17–v21 | Ducks, sky/rainbow, flora, snappier feel, inertia, physics sliders, more quads |
| v22–v26 | Solid collisions & crashes, 3D sign, freestyle park, bando + halfpipe, gravity & PID sliders, tuning presets |
| v27–v30 | Fixed z-fighting flicker, spin pylons & square gates, roll sensitivity, trick scoring, saved calibration, easter eggs |
| v31–v32 | Post-processing (bloom / motion blur / grade), IBL, procedural PBR normal detail, post-FX sliders |

---

## 🛠️ Tech

- **Three.js** (r128, single CDN script)
- Vanilla JavaScript / HTML / CSS — one self-contained file per version
- Fixed-timestep physics integrator, quaternion attitude, custom WebGL post-processing

No frameworks, no bundler, no `node_modules`.

---

## ⚠️ Notes & limitations

- Designed for **desktop browsers** (Chrome/Edge/Firefox). Best with a gamepad.
- It's a **stylised** world, not photoreal — see the Roadmap for why.
- The post-FX build (v31+) is heavier than earlier versions; if a low-end machine struggles, use an earlier version or turn Bloom/Motion blur down in `TAB`.

---

## 📄 License

MIT — see `LICENSE`.

---

*Built iteratively, feel-first. Fly safe. 🚁*
