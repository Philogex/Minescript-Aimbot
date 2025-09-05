# Bow Aimbot (Minescript / Pyjinn)

Single‑file bow aimbot for Minecraft using Minescript (Pyjinn). Computes a ballistic intercept with configurable gravity/drag, smooth velocity averaging, ping‑aware release timing, and center‑mass bias.

---

## Installation

Requirements:

* [`minescript`](https://github.com/maxuser0/minescript.git) 5.05b+

Clone:

```bash
git clone https://github.com/Philogex/Minescript-Aimbot.git
mv Minescript-Aimbot <minescript-directory>
```

---

## Usage

- Run the script (Pyjinn) in Minescript.
- Controls:
  - Mouse1: toggle lock‑on (starts drawing and aims when ready)
  - `O`: cancel/stop (releases right‑click if held)

Behavior:
- On lock, it selects the entity under the crosshair or the best in a small view‑cone.
- It draws the bow, waits until full draw, then computes the intercept and snaps aim just before releasing.
- It holds orientation for a couple ticks to cover arrow spawn delay.

---

## Configuration

All options are at the top of `bow_aimbot.pyj`:

- `RELEASE_DELAY_TICKS`: base ticks to lead for local release latency
- `LEAD_EXTRA_TICKS`: extra lead for fast movers
- `POST_RELEASE_HOLD_TICKS`: hold aim after release (spawn tick)
- `N_AVG_SAMPLES`: velocity smoothing window
- `ARROW_GRAVITY`, `ARROW_DRAG`, `ARROW_SPEED_SCALE`: arrow physics
- `FULL_DRAW_THRESHOLD`, `DRAW_EPS`: release at full draw
- `AIM_CONE_DEGREES`, `MAX_TARGET_DISTANCE`: acquisition cone/range
- `TARGET_Y_BIAS`: aim a bit below eyes (center‑mass)

Notes:
- Lead time also adds your network latency (ms/50) in multiplayer.
- Set `REPEAT_SHOTS_WHEN_ACTIVE = True` for continuous firing while locked.

---

## Project Structure

```
bow_aimbot/
├── bow_aimbot.pyj   # aimbot script (single file)
├── README.md
└── LICENSE
```

---

## License

This project is licensed under the [MIT License](LICENSE).

---
