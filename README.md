# 🌀 Trippy Plains — FPV Freestyle Sim

A standalone, single-file FPV drone freestyle sim. Three linked worlds, ten craft (including a collective-pitch helicopter), real-physics flight model, and full DJI/gamepad support. Everything lives in one `.html` file — no build, no installs, no external assets (Three.js loads from a CDN), so it runs straight from disk or GitHub Pages.

> **Latest:** `trippy-plains-v25.html` — double-click to open in a desktop browser (Chrome recommended) and fly.

---

## 🚀 Quick start

1. Double-click `trippy-plains-v25.html` (or serve it from any static host).
2. On the setup screen choose **Keyboard**, **Controller** (power it on first — move a stick to wake it) or **Touch** on phones/tablets.
3. With a controller, run **CALIBRATE STICKS** the first time (see below). It's remembered afterwards.
4. Hit FLY. The TAB tuning panel opens automatically — press **TAB** to hide it.

> ⚠️ Open the file directly — don't run it inside an embedded preview/iframe, or the browser blocks the Gamepad API.
>
> 🍏 **Safari:** Safari only exposes a controller after a **button press** on it — moving the sticks alone won't wake it. Press any button (C1/C2/record on a DJI RC), serve the page over **https** (GitHub Pages is fine), and keep the tab focused. The setup screen shows a live count of devices WebKit reports; if it stays at 0 after button presses over https, Safari is not exposing the controller — there is no web API that can fix this, use Chrome/Edge on that machine. (Likewise iPhone web pages cannot drive real haptics — Android only; iOS 17.4+ gets a best-effort light tick.)

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
| `1` – `0` | Swap craft (or click the CRAFT row in TAB) |
| `N` | Next map |
| `Q` | Fast render ↔ full quality |
| `G` | Gate run — timed 5-gate slalom (Zone Field) |
| `V` | Wind on / off |
| `[` / `]` | Camera angle down / up |
| `TAB` | Controls & tuning panel (open by default) |
| `ESC` | Back to the start screen |

The bottom-right legend shows numbered mini-icons for all ten craft — the active one is lit green. The same row appears in TAB as clickable buttons.

**📱 Mobile / touch:** on a touch device the setup screen offers **FLY · TOUCH** — two thumb-stick zones appear at the bottom corners (Mode 2: left = throttle/yaw with sticky throttle that holds where you leave it, right = pitch/roll, spring-centred). A button column on the right edge gives ARM / RST / LVL / MAP / TAB / ESC, and the panel has a pinned ✕ to close it. **Building on mobile:** open TAB in the Sandbox, tap a chip (including 🧹 erase), close the panel with ✕, then tap the upper part of the screen to place or erase — the lower screen stays reserved for your thumbs. Landscape recommended; the HUD compacts and the tile row lifts above your thumbs.

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
| 9 | TINY 65 | 65 mm 1S whoop — parachute drag, heavy sag, ~40 km/h indoor dancer |
| 0 | LIFTER X8 | 8" cinelifter — 1.9 kg camera mule, slow to spool, plan ahead, ~117 km/h |

---

## 🗺️ Four worlds, linked by portals

Every map has three glowing **portal gates** near spawn (pulsing ring, halo, 150 m sky beam; colour = destination). Fly through the hoop and you emerge at the matching gate in the next world — speed, attitude, arm state, battery and timer all carry over. Approach corridors are kept clear of equipment. `N` or TAB → MAP also switches directly. The sim always boots into Trippy Plains.

**🌀 Trippy Plains** — open-field freestyle: scaffolds, helixes, tables, gates and pennants in three size tiers, curving square tunnels, bent holey pipes, torus rings, floating sky equipment, surfable dirt mounds, and two floor portals down to a mirrored underground "Inception" level.

**⛰ Zone Field** — grass-and-dirt practice field: dirt-jump cluster (surfable), scaffold towers, slalom gates, octagonal hoops, containers, grind rails, power lines, trees — plus a 6-arch race loop, ladder gates, limbo hurdles, two dive towers, a 7-pole slalom, a wall-ride corridor and a power-loop tower.

**🏭 Ruhrwerk** — massive abandoned West-German industrial complex: a dozen brick chimneys (three square ones with diveable hollow cores), seven empty warehouses with door/roof gaps, conveyor truss bridges, three cranes, tank farms, silo batteries, rail spur with hopper wagons, transmission pylons, pipe racks, blast furnace, flare stack, coke-oven battery, settling ponds, scrap yard, cooling-water channel, an open pit with two turning bucket-wheel excavators and surfable slag heaps — plus **THE BLOCK**: a 10-storey empty shell with window bands and holed floors, stamped three times, and three 3×-scale **MEGA BLOCKS** with a full-height drop shaft and a horizontal gap straight through the middle.

**▦ Sandbox** — an empty grid world that *you* build while flying: open TAB and drag chips (box, wall, gate, hoop, arch, tower, surfable mound, pole) onto the world — or click a chip, then click the ground. Objects face you, snap to axis alignment, and collide for real. Right-click an object to remove it, CLEAR SANDBOX wipes it, and the layout auto-saves to the browser.

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

**Craft** — clickable picker for all ten machines. **Snappiness** — Rate (up to 2000 °/s), Snap (up to 320k), **Pitch rate** and **Yaw rate** per-axis overrides. **Flight · Physics** — Power (TWR), mass/inertia, throttle response, gravity, expo, **drag %, propwash %, angle-mode lean**. **Rate PID** — P, I, D. **Camera** — angle + FoV. **Feel · Wind** — cam-shake amount (0 = off), wind speed (0 = off), props-in-view and **haptics** toggles, all remembered. **Sound** — motor volume. **Scene** — floor/background brightness, contrast and colour saturation, **time of day (DAWN / NOON / DUSK — remembered)**. **Build** — sandbox object palette (drag-drop or click-place, right-click remove, CLEAR). **Map** — Plains / Zone Field / Factory / Sandbox buttons. **Controller** — stick deadzone (remembered) + calibrate sticks.

---

## ⚙️ Physics (real-quad benchmark)

500 Hz integration; Betaflight "Actual" rates; motor-mixer saturation with air-mode floor (idle spool, collective bump during hard rotation); prop inflow loss and translational lift; vortex-ring state with propwash buffet; rotor inflow damping; gyroscopic ω×Iω coupling; asymmetric motor spool; 6S battery sag; ground effect; optional wind (`V`); AABB + surfable-ellipsoid terrain collisions. The Zone-spec quad hovers at 40 %, pulls 8 g, and tops out near real-world speeds. The heli is a genuinely different model: governor headspeed with cyclic authority ∝ headspeed², and signed collective for sustained inverted flight.

---

## ⚡ Performance

Single file + one CDN fetch. On every map load all static opaque meshes are **baked into one merged mesh per material**, collapsing thousands of draw calls to a few dozen; vegetation is instanced (one call per map); towers share cached geometries; switching maps disposes the old map's GPU buffers. If FPS sits under 45 for 3 s the sim auto-drops to fast render (flash + `Q` restores), and `Q` toggles it manually any time.

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
| `trippy-plains-v13.html` | **Pro pack — Feel: camera micro-shake from propwash/motors/airspeed, crash thud, speed-scaled wind whoosh, low-battery beeper. Turtle mode (full stick flips an upside-down quad). `G` gate run: timed 5-gate slalom in Zone Field with glowing next-gate marker + best time saved. Tune presets (SAVE/LOAD/DEFAULT per craft, auto-loaded on swap). OSD: voltage colour-coded by cell health + mAh-used tile.** |
| `trippy-plains-v14.html` | **Feel controls: cam-shake and wind sliders in TAB (0 = off, persisted; `V` toggle wired up). Scene contrast + colour-saturation sliders (persisted). Zone Field race/freestyle expansion: 6-arch race loop, ladder gates, limbo hurdles, dive towers, pole slalom, wall-ride corridor, power-loop tower.** |
| `trippy-plains-v16.html` | **SANDBOX — 4th map: empty grid world, buildable in flight from a TAB palette (drag-drop / click-place, right-click remove, auto-saved layout, real colliders incl. surfable mounds). Portals now 3 per map. Feel polish: arm/disarm + gate + portal + build tones, subtle speed-FOV kick.** |
| `trippy-plains-v17.html` | **Pro tuning: panel widened (no horizontal scroll), clickable CRAFT picker in TAB, new sliders — yaw rate, drag %, propwash %, angle-mode lean, FoV, stick deadzone (persisted) — all covered by tune presets. Two new craft: TINY 65 (1S whoop) and LIFTER X8 (8" cinelifter), drag-validated to real top speeds.** |
| `trippy-plains-v18.html` | **Realism graphics pass — bump-mapped grounds with max-anisotropy filtering (sharp at FPV grazing angles), richer procedural surfaces (tire tracks & scuffs on the plains, mow stripes & dirt patches on the zone grass, oil stains & faded lane lines on the factory concrete), painted-sun sky domes with horizon haze and high streak clouds, soft billboard clouds replacing the old blobs, ~11k instanced grass/scrub/weed tufts per map (one draw call), per-tree foliage colour variation, tighter shadow frustum + normal-bias for crisper contact shadows.** |
| `trippy-plains-v19.html` | **Light & surface pass — time-of-day system (DAWN / NOON / DUSK buttons: low warm sun with long shadows, repainted sky, matched fog & hemisphere light, persisted). Procedural wall materials: brick with soot streaks on chimneys & coke ovens, corrugated cladding with rust runs & bolt rows on warehouses, panel-lined stained concrete on towers, neutral grime maps tinting containers/gates/cranes. Prop dust kicks up when hovering low at throttle.** |
| `trippy-plains-v20.html` | **Pilot pack — props-in-view overlay (subtle spinning blur discs at top of frame, throttle/tilt-driven, toggleable & remembered), crash video glitch (frame jitter + scanline static + colour washout for half a second), live rates-curve graph in TAB (roll/pitch/yaw, Betaflight-configurator style, redraws with every slider), compass heading + degrees in the HUD, amps-draw OSD tile, FPS counter.** |
| `trippy-plains-v21.html` | **World & atmosphere — distant horizon scenery on every map (fog-softened hill rings on Plains/Zone, an industrial skyline of silhouette blocks and far chimneys around the Ruhrwerk), screen-space sun lens flare that blooms when you look into the sun, wind-driven fluttering flags and pennants, a drifting smoke plume off the tallest factory stack, lazy bird flocks circling the open maps, and a 900-star night sky with a moon over the Sandbox.** |
| `trippy-plains-v22.html` | **Baked & fast — per-material static-geometry baking on map load (draw calls collapse from ~1500+ to a few dozen in the Ruhrwerk; animated pieces excluded automatically), auto fast-render fallback below 45 fps, per-map hemisphere bounce light (green off grass, tan off dirt, grey off concrete), denser low-sun fog at dawn/dusk for deeper atmospheric layering.** |
| `trippy-plains-v23.html` | **Mobile & touch — FLY · TOUCH mode with dual thumb-sticks at the bottom of the screen (multi-touch, radius-clamped, sticky throttle, spring-centred right stick), touch button column (ARM/RST/LVL/MAP/TAB/ESC), pinch-zoom/scroll locked, compact HUD layout under 760 px, TAB panel touch-scrollable. Follow-up fixes: pinned ✕ close button in the panel, touch buttons layered above the panel, tap-to-place/erase sandbox building with a 🧹 erase chip.** |
| `trippy-plains-v24.html` | **Haptics — vibration on crashes, arm/disarm, gates, portals, build taps, touch buttons and the duck (Vibration API on Android/Chrome; gamepad dual-rumble bonus where supported; iOS Safari has no vibration API — on iOS 17.4+ the sim falls back to the native switch-control Taptic tick: a single light tap per event, big events double-tap; older iOS gets nothing). Toggle in FEEL, remembered. Graphics: the quad now casts a soft contact-shadow blob that grows/fades with altitude and slides away from the sun (the landing depth cue), a cool rim/backlight opposite the sun (time-of-day matched) so silhouettes separate from the background, and per-instance hue/lightness variation across all vegetation.** |
| `trippy-plains-v25.html` | **Grounded light — contact-AO layer: every grounded structure on every map gets a soft baked shadow skirt, built as a single merged mesh (one draw call) from the physics colliders, visually anchoring towers, gates, crates and chimneys to the ground. Per-time-of-day cinematic colour grade composited with your contrast/colour settings (warm sepia dawn, amber dusk). Factory water now lives — scrolling micro-ripples shimmer the settling ponds and cooling channel. Safari controller diagnostics + iOS gesture-context haptic ticks.** |

---

## 🛠️ Tech

Three.js r128 (UMD global). Procedural canvas textures, alpha-mapped holey pipes/toruses, `ShapeGeometry` ground holes, mirrored (`scale.y = −1`) underground, seeded-RNG fixed maps. Web Audio synthesised motors. No dependencies to install.

## 📄 License

MIT — free to use, modify, and share.
