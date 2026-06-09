# 🌀 Trippy Plains — FPV Freestyle Map

A standalone, single-file FPV drone freestyle space inspired by *The Zone*. Open-field, low-poly, physics-driven, and built to fly. Everything lives in one `.html` file — no build, no installs, no external assets (Three.js loads from a CDN).

> **Latest:** `trippy-plains-v9.html` — just double-click to open in a desktop browser (Chrome recommended) and fly.

---

## 🚀 Quick start

1. Double-click `trippy-plains-v9.html` to open it directly in a desktop browser.
2. On the setup screen choose **Keyboard** or **Controller** (plug in / power on your gamepad first — move a stick to wake it).
3. If a controller is detected you can **calibrate the sticks** before flying (see below).
4. Fly. Press **TAB** any time for the controls + tuning panel.

> ⚠️ Open the file directly — don't run it inside an embedded preview/iframe, or the browser will block the Gamepad API and your controller won't be detected.

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

A gamepad (e.g. DJI RC) is auto-detected on the setup screen.

---

## 🎮 DJI / gamepad calibration

The setup screen and the TAB panel both have a **CALIBRATE STICKS** button.

- **First time:** the controller shows as *not calibrated* — calibration is recommended. The wizard walks you through four moves: full **throttle up**, full **yaw right**, full **pitch forward**, full **roll right**. It detects which axis and direction each maps to.
- **Already calibrated:** a saved calibration is detected, and you get the choice to **fly with it** or **re-calibrate**.
- Calibration is saved to your browser (`localStorage`) and reused next time.
- You can re-calibrate any time in flight from **TAB → CONTROLLER → CALIBRATE STICKS**.

---

## 🗺️ What's in the map

- **Zone-inspired freestyle field** — scaffolds, helixes, tables, box stands, square gates and pennants scattered across a big open field in **three size tiers** (1× inner, 2× mid, 3× outer).
- **Curving square tunnels** you fly through horizontally.
- **Long bent cylindrical pipes with holes** — fly straight down the inside through the bends.
- **Big holey torus rings** — fly the donut hole or loop the tube.
- **Floating / suspended equipment** higher in the air, including scaffolds turned on their side like sky-walkways.
- **Two floor portals** opening to an **underground "Inception" level** — a full mirror copy of everything above the floor, flipped below it. Dive through a portal, roam the underside, and fly back up through a portal. One portal sits near the action; the second is further out over open ground.

---

## 🎛️ TAB tuning panel

Press **TAB** in flight for one panel with the keyboard reference plus live tuning:

- **Snappiness** — Rate (°/s), Snap
- **Flight · Physics** — Power (TWR), Mass / inertia (g), Throttle response (ms), Gravity (m/s²), Expo
- **Rate PID** — P, I, D
- **Camera** — camera angle
- **Sound** — motor volume (0 = mute)
- **Scene** — floor / background brightness
- **Controller** — calibrate sticks

Values sync to the active quad and refresh when you swap drones.

---

## 🔊 Sound

A fully synthesised motor sound (Web Audio, no audio files): pitch, brightness and volume rise with throttle, idling low when armed and silent when disarmed. Audio starts on the first FLY click (browsers require a user gesture). Control the level with **TAB → Sound → Motor volume**.

---

## 📦 Version history

| File | Highlights |
|------|-----------|
| `trippy-plains.html` | v1 — first open field inspired by *The Zone*. |
| `trippy-plains-v2.html` | Open dive-through towers, curving tunnels, darker floor, tuning panel. |
| `trippy-plains-v3.html` | Equipment in three size tiers (1× / 2× / 3×) + camera-angle controls. |
| `trippy-plains-v4.html` | TAB shows controls + tuning together (multi-file style). |
| `trippy-plains-v5.html` | Synthesised throttle / motor sound + volume control. |
| `trippy-plains-v6.html` | Doubled equipment, floor hole, mirrored "Inception" underground, bent pipes. |
| `trippy-plains-v7.html` | Holey torus rings + full flight tuning (power, mass, throttle resp, gravity, expo). |
| `trippy-plains-v8.html` | Second floor portal + DJI/gamepad stick calibration (setup & TAB). |
| `trippy-plains-v9.html` | **Zone-grade physics: motor-mixer saturation + air mode, prop inflow & translational lift, rotor inflow damping, gyroscopic coupling, idle spool, per-quad FoV (125° Zone).** |

---

## 🛠️ Tech

Three.js r128 (UMD global). Accel-limited acro rate model with Betaflight "Actual" rates, motor-mixer saturation (air mode), prop inflow & translational lift, rotor inflow damping, gyroscopic ω×Iω coupling, battery sag, wind, propwash/VRS, ground effect, and AABB collisions. Procedural canvas textures; alpha-mapped holey pipes and toruses; ground built with `ShapeGeometry` holes; the underground is a mirrored (`scale.y = −1`) clone of the field. No dependencies to install.

---

## 📄 License

MIT — free to use, modify, and share.
