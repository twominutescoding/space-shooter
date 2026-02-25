# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Game

No build process or dependencies required. Open `space-shooter.html` directly in any modern web browser.

## Project Structure

This is a **single-file HTML5 game** (`space-shooter.html`) — all HTML, CSS, and JavaScript live in one file. There are no external dependencies, no package manager, and no build tools.

External resources loaded at runtime:
- Google Fonts: Orbitron (title), Share Tech Mono (UI text)

## Architecture

**VOID STRIKER** is a Space Invaders-style arcade game rendered on an HTML5 Canvas (480×560px).

### Game States
- `menu` → `playing` → `dead` (or `win`)

### Key Global Objects
- `player` — ship position, velocity, lives, invincibility timer
- `enemies[]` — 40-enemy grid (10×4), each with `type` (0–2), `alive`, and color/points
- `bullets[]` / `enemyBullets[]` — projectile arrays
- `particles[]` — explosion/damage visual effects

### Enemy Types (by row, bottom to top)
| Type | Shape | Points |
|------|-------|--------|
| 0 | Crab | 50 |
| 1 | Bug | 100 |
| 2 | Diamond (top) | 150 |

### Game Loop
`requestAnimationFrame` → delta-time-based updates → draw. All movement uses `dt` (seconds) for frame-rate independence.

### Difficulty Scaling
Each wave: enemy movement speed increases by `0.08`, enemy fire rate interval decreases (floors at ~15 frames).

### Controls
- **Desktop**: Arrow keys / WASD to move, Space / Z to shoot
- **Mobile**: Touch-drag to move, touch triggers auto-shoot

### Rendering
All drawing is done with Canvas 2D API using `shadowBlur`/`shadowColor` for neon glow effects. Scanline overlay and animated starfield (120 stars) provide the retro CRT aesthetic.
