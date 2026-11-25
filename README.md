# Himalayan Drive — Nepal Mountain Highway

A 3D mountain-highway driving simulator that runs entirely in the browser.
Drive a 4.2 km winding loop through green Himalayan hills, overtake buses
and trucks, and chase your best lap.

**Live:** https://daveyadav.github.io/Nepal-Drive/ (Pages: Settings → Pages → Deploy from branch → `main` → `/ (root)`)

## What is in v2 (research-led rebuild, 2026-11-25)

- Realistic graphics: gradient sky dome + sun disc + haze fog, ACES tone mapping, procedural asphalt (cracks, patches, worn markings baked into the road texture), splat-blended olive terrain with terraced fields, alpha-card trees (not cones), Trishuli river beside the road
- Real Nepal detailing: W-beam guardrails, black-white delineator posts, milestones, chevron signs, bilingual green gantry signs with real distances (Mugling 2 km, Narayanghat 36 km, Kathmandu 108 km), chiya pasal (चिया पसल), landslide scars with drums + excavator, suspension bridge with prayer flags, utility poles with sagging wires, petrol pump at Mugling
- Detailed player jeep: clearcoat paint with environment reflections, glass cabin, roof rails, number plate, working headlights
- Live traffic: Sajha-green bus, Tata trucks, micro vans, motorbikes (weave and overtake), blind-bend bus warnings with horn
- Arcade bicycle-model physics: speed-sensitive steering, drift on handbrake, off-road slowdown with dust, crash damage, guardrail scrapes
- Missions: Checkpoint Run (Galchhi → Malekhu → Kurintar → Mugling → Narayanghat, beat the clock) or Free Drive (3 laps); overtake + near-miss scoring with combos; fuel + damage, refuel/repair at the Mugling pump
- Weather: Autumn Clear / Golden Hour / Monsoon rain (wet road, rain streaks)
- HUD: speedometer, score, time, next checkpoint, fuel + damage bars, live minimap
- Cameras: chase, hood, high (`C`); procedural engine/wind/horn/skid audio (Web Audio)
- Phone controls: drag left half to steer, GAS / BRAKE buttons on the right
- Quality tiers: High / Medium / Low, with automatic drop if the frame rate falls

## v3.1 (2026-11-25) — lag, reversed steering and twitchy handling fixed
Research-led fix pass for the three problems reported after playing v3 on a
Redmi 10. (1) Steering was reversed: drag-right / D gave +steer and the
bicycle model turns LEFT for positive steer — one sign was missing. Fixed
with a single negation (`P.steer = -input * maxSteer`, verified against the
car's nose axis: ExtrudeGeometry side profile, nose = local +Z, so
`rotation.y = heading` is correct). Drag steering is now relative/anchored
(touch-down point = anchor, 100 px = full lock, 10% dead zone, expo 1.35,
anchor slides at full lock, returns to centre on release), with per-role
pointer IDs so GAS/BRAKE fingers can't hijack steering, plus a "Reverse
steering" toggle on the menu as a safety net. (2) Lag: DPR 1.0 on phones
(1.5 desktop), no MSAA/stencil/alpha buffers, shadows off on phones (blob
shadow under the player car only), terrain + props downgraded to Lambert on
phones (clearcoat/PMREM kept only for the player car paint, PMREM skipped
on phones), terrain 128×128 segments, static scenery merged into one
vertex-colour mesh per group on phones (traffic bodies, houses, signs,
bridge planks, boulders, drums), traffic wheels merged tyre+hub, minimap
static layer cached offscreen and redrawn at ~8 Hz, physics samples a
precomputed height grid instead of noise, zero allocations in the frame
loop, adaptive ladder (demote after ~2.5 s over 21 ms/frame, promote after
~8 s under 17 ms, 10 s grace reset on every Start). (3) Handling calmed:
top speeds Bolero 80 / Swift 86 / Hilux 83 km/h, accel ~7 m/s² with taper,
braking 11 m/s², reverse 20 km/h, max steer as a speed curve (28° parked →
5° at top speed, full-lock yaw capped ~0.8 rad/s), steering smoothing
150 ms in / faster return, FOV 63° +7 at top speed. Also fixed: car now
spawns on the highway centreline at Mugling (was half on the shoulder),
grass/houses can no longer spawn on any road ribbon (junctions included),
and the "Graphics lowered" toast only fires on a real drop after the grace
period. Bonus fix: dirt roads never slowed the car before — the code read
`road.dirt`, a property that doesn't exist (roads have `surface`); dirt is
now 18 m/s with grip 7.

## v3 (2026-11-25) — free world
Open 1200×1200 m map, drive anywhere: Prithvi Highway across the map with
Mugling in the middle, a road south to Narayanghat over the Trishuli bridge,
a road through Mugling bazaar, a dirt track along the river to a rafting
point, and switchbacks up to a hilltop viewpoint with snow peaks behind.
Real cars built from extruded side profiles with wheel arches: pick a
Bolero-style SUV, a Swift-style hatchback or a Hilux-style pickup (each
drives differently). Free Ride mode: explore and discover 8 glowing places
(bazaar, bridge, rafting point, viewpoint, tea shops, landslide, pump,
Manakamana sign). Highway Run: timed Mugling → Narayanghat, 4 gates.
Different surfaces (asphalt / dirt / off-road / river) change grip and speed.

## v2.2 (2026-11-25) — smoother handling, more realistic cars
- Handling: steering now eases in (no snap), shrinks hard with speed, longer
  wheelbase, higher grip — the jeep turns calmly instead of twitching. Touch
  steering takes a longer drag for full lock.
- Speed: gentler acceleration that tapers near the top, softer braking,
  top speed ~108 km/h on road (~29 km/h off road) — easy to hold a steady
  speed on the bends.
- Cars: 5-spoke alloy wheels, wheel-arch trim, grille slats, fog lights,
  wipers, door lines, side steps, mirror indicators, antenna, front + rear
  plates and a soft contact shadow on the jeep; buses get window pillars,
  side stripe, SAJHA YATAYAT boards and mirrors; trucks get grille, exhaust
  stack, mud flaps and plates; micros and sedans get mirrors, handles, chrome
  trim and plates.

## Controls

| Key | Action |
|---|---|
| `W` / `↑` | Accelerate |
| `S` / `↓` | Brake / reverse |
| `A` `D` / `←` `→` | Steer |
| `Space` | Handbrake |
| `C` | Change camera |
| `R` | Repair / back to start |
| `P` / `Esc` | Pause |

Goal: finish 3 laps. Watch the checkpoints and don't hit the buses.

## Tech

Single self-contained `index.html` (Three.js r160 via CDN). No build step,
no server needed — any static host works.
