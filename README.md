# Himalayan Drive — Nepal Mountain Highway

A 3D mountain-highway driving simulator that runs entirely in the browser.
Drive a 4.2 km winding loop through green Himalayan hills, overtake buses
and trucks, and chase your best lap.

**Live:** enable GitHub Pages (Settings → Pages → Deploy from branch → `main` → `/ (root)`),
then open `https://<your-username>.github.io/Nepal-Drive/`

## What is in v1

- Real 3D world (Three.js / WebGL): sun + soft shadows, sky gradient, drifting clouds, fog, procedural terrain with grass, rock and snow peaks
- Winding mountain road with centre dashes, edge lines, guardrails on bends, and signs for Mugling, Kathmandu and Pokhara
- Detailed player car: metallic paint, glass cabin, spoiler, headlights, turning front wheels, body roll
- Live traffic: buses, trucks and cars driving both ways
- Arcade physics: acceleration, braking, reverse, handbrake, off-road slowdown with dust, crash damage (press `R` to repair)
- HUD: speedometer, lap / distance / time, best lap (saved on your device), live minimap
- Cameras: chase, hood, high (`C`)
- Engine sound (Web Audio, starts after you press play)
- Phone controls: on-screen steering, gas and brake
- Quality toggle: High / Medium graphics on the start screen

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
