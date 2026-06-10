# 🌀 Trippy Plains — FPV Freestyle Sim

A standalone, single-file FPV drone freestyle sim. Three linked worlds, eight craft (including a collective-pitch helicopter), real-physics flight model, and full DJI/gamepad support. Everything lives in one `.html` file — no build, no installs, no external assets (Three.js loads from a CDN), so it runs straight from disk or GitHub Pages.

> **Latest:** `trippy-plains-v12.html` — double-click to open in a desktop browser (Chrome recommended) and fly.

---

## 🚀 Quick start

1. Double-click `trippy-plains-v12.html` (or serve it from any static host).
2. On the setup screen choose **Keyboard** or **Controller** (power on your gamepad first — move a stick to wake it).
3. With a controller, run **CALIBRATE STICKS** the first time (see below). It's remembered afterwards.
4. Hit FLY. The TAB tuning panel opens automatically — press **TAB** to hide it.

> ⚠️ Open the file directly — don't run it inside an embedded preview/iframe, or the browser blocks the Gamepad API.

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
| `1` – `8` | Swap craft (see icons in the legend) |
| `N` | Next map |
| `Q` | Fast render ↔ full quality |
| `[` / `]` | Camera angle down / up |
| `TAB` | Controls & tuning panel (open by default) |
| `ESC` | Back to the start screen |

The bottom-right legend shows numbered mini-icons for all eight craft — the active one is lit green.

**Input is self-healing:** in keyboard mode the controller takes over the moment you move a stick (🎮 flash + HUD icon); if the pad naps or its index drifts mid-flight, it re-acquires automatically or falls back to keyboard.

---

## 🚁 The hangar

| Key | Craft | Character |
|-----|-------|-----------|
| 1 | MARIO 5 | 5" freestyle, raw power, razor-sharp rates |
| 2 | THE ZONE *(default)* | 680 g / TWR 8 / Actual 210·700·0.57 / FoV 125° |
| 3 | BEE 35 | 3.5" cinewhoop — ducted, planted, forgiving |
| 4 | RACE X | 5" racer — instant response, huge momentum |
| 5 | WASP | 2.5" sub-250 — feather-light, hyper-twitchy |
| 6 | LONGRANGE 7 | 7" — floaty, carries speed forever |
| 7 | HELI CP | Collective-pitch heli: governor headspeed, signed collective, hovers ~62 % stick, flies inverted |
| 8 | MASTER 3.5 | 3.5" freestyle, Master-3X class: 365 g on 4S, nimble & punchy |

---

## 🗺️ Three worlds, linked by portals

Every map has two glowing **portal gates** near spawn (pulsing ring, halo, 150 m sky beam; colour = destination). Fly through the hoop and you emerge at the matching gate in the next world — speed, attitude, arm state, battery and timer all carry over. Approach corridors are kept clear of equipment. `N` or TAB → MAP also switches directly. The sim always boots into Trippy Plains.

**🌀 Trippy Plains** — open-field freestyle: scaffolds, helixes, tables, gates and pennants in three size tiers, curving square tunnels, bent holey pipes, torus rings, floating sky equipment, surfable dirt mounds, and two floor portals down to a mirrored underground "Inception" level.

**⛰ Zone Field** — grass-and-dirt practice field: dirt-jump cluster (surfable), scaffold towers, slalom gates, octagonal hoops, containers, grind rails, power lines, trees.

**🏭 Ruhrwerk** — massive abandoned West-German industrial complex: a dozen brick chimneys (three square ones with diveable hollow cores), seven empty warehouses with door/roof gaps, conveyor truss bridges, three cranes, tank farms, silo batteries, rail spur with hopper wagons, transmission pylons, pipe racks, blast furnace, flare stack, coke-oven battery, settling ponds, scrap yard, cooling-water channel, an open pit with two turning bucket-wheel excavators and surfable slag heaps — plus **THE BLOCK**: a 10-storey empty shell with window bands and holed floors, stamped three times, and three 3×-scale **MEGA BLOCKS** with a full-height drop shaft and a horizontal gap straight through the middle.

> 🥚 *A golden duck nests somewhere industrial. Touch it.*

---

## 🎮 Calibration (DJI / any gamepad)

Available from the setup screen and TAB → CONTROLLER:

1. **Guided detection** — four steps by physical stick ("Push the LEFT stick fully UP"…), with progress dots and live feedback; each detected axis locks so it can't be picked twice, and the wizard waits for release between steps.
2. **Live channel table** — centre-growing bars per channel (post-inversion, so a wrong direction is obvious), with manual axis dropdowns and inversion checkboxes to fix anything by hand.
3. **ARM / RESET assignment** — press or flip any control; plain buttons and DJI-style switch-axes both work.

Everything (axes, inversions, button bindings) is saved to the browser and reloaded next session — the setup screen will say *"Calibration remembered — just hit FLY."*

---

## 🎛️ TAB tuning panel

Open by default in flight; TAB toggles it. Live tuning synced to the active craft:

**Snappiness** — Rate (°/s, up to 2000), Snap (accel limit, up to 320k), **Pitch rate** (180–2000 °/s — pitch-axis override for very fast flips; pitch snap auto-scales). **Flight · Physics** — Power (TWR), mass/inertia, throttle response, gravity, expo. **Rate PID** — P, I, D. **Camera** — angle. **Sound** — motor volume. **Scene** — floor/background brightness. **Map** — Plains / Zone Field / Factory buttons. **Controller** — calibrate sticks.

---

## ⚙️ Physics (real-quad benchmark)

500 Hz integration; Betaflight "Actual" rates; motor-mixer saturation with air-mode floor (idle spool, collective bump during hard rotation); prop inflow loss and translational lift; vortex-ring state with propwash buffet; rotor inflow damping; gyroscopic ω×Iω coupling; asymmetric motor spool; 6S battery sag; ground effect; optional wind (`V`); AABB + surfable-ellipsoid terrain collisions. The Zone-spec quad hovers at 40 %, pulls 8 g, and tops out near real-world speeds. The heli is a genuinely different model: governor headspeed with cyclic authority ∝ headspeed², and signed collective for sustained inverted flight.

---

## ⚡ Performance

Single file + one CDN fetch. Repeated towers share cached geometries; switching maps disposes the old map's GPU buffers; `Q` toggles a fast-render mode (lower pixel ratio, shadows off) if the dense factory dips your frame rate.

---

## 📦 Version history

| File | Highlights |
|------|-----------|
| `trippy-plains.html` | v1 — first open field inspired by *The Zone*. |
| `trippy-plains-v2.html` | Dive-through towers, curving tunnels, tuning panel. |
| `trippy-plains-v3.html` | Equipment in three size tiers + camera-angle controls. |
| `trippy-plains-v4.html` | TAB shows controls + tuning together. |
| `trippy-plains-v5.html` | Synthesised motor sound + volume control. |
| `trippy-plains-v6.html` | Doubled equipment, floor hole, mirrored underground, bent pipes. |
| `trippy-plains-v7.html` | Holey torus rings + full flight tuning. |
| `trippy-plains-v8.html` | Second floor portal + stick calibration. |
| `trippy-plains-v9.html` | Zone-grade physics: mixer saturation/air mode, prop inflow, rotor drag, gyro coupling, per-quad FoV. |
| `zone-sim.html` | From-scratch Zone-style sim — fixed seeded map, surfable mounds, timer + voltage OSD. |
| `trippy-plains-v10.html` | Best of Zone merged in; calibration v2; 7" + heli; in-flight multimap. |
| `trippy-plains-v11.html` | Beacon portals with clean corridors; Ruhrwerk built & densified (3 waves); THE BLOCK + MEGA BLOCKS; golden duck; ESC menu; craft icons; Q toggle; self-healing input. |
| `trippy-plains-v12.html` | **Pitch-rate slider (180–2000 °/s) + extended Rate/Snap ranges; gradient sky domes, per-map sun colour, vignette; 8th craft (3.5" Master-3X class).** |

---

## 🛠️ Tech

Three.js r128 (UMD global). Procedural canvas textures, alpha-mapped holey pipes/toruses, `ShapeGeometry` ground holes, mirrored (`scale.y = −1`) underground, seeded-RNG fixed maps. Web Audio synthesised motors. No dependencies to install.

## 📄 License

MIT — free to use, modify, and share.
