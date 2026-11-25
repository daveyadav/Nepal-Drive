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
