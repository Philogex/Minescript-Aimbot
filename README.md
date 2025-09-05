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
- `VELOCITY_SMOOTHING`: one of `latest`, `ema`, `avg` (windowed)
- `VELOCITY_EMA_ALPHA`: EMA weight (when `ema`)
- `VELOCITY_INSTANT_WEIGHT`: blend of instantaneous vs smoothed velocity
- `N_AVG_SAMPLES`: window size for `avg` mode
- `ARROW_GRAVITY`, `ARROW_DRAG`, `ARROW_SPEED_SCALE`: arrow physics
- `FULL_DRAW_THRESHOLD`, `DRAW_EPS`: release at full draw
- `AIM_CONE_DEGREES`, `MAX_TARGET_DISTANCE`: acquisition cone/range
- `TARGET_Y_BIAS`: aim a bit below eyes (center‑mass)

Notes:
- Lead time also adds your network latency (ms/50) in multiplayer.
- Set `REPEAT_SHOTS_WHEN_ACTIVE = True` for continuous firing while locked.

### CLI Overrides (optional)

You can override a few settings when launching the script; if omitted, the in‑file defaults are used.

Examples:

```
# Prefer latest velocity only
... \Minescript-Aimbot\bow_aimbot --vel-mode=latest --vel-instant=1.0

# EMA smoothing (alpha=0.6), blend 50/50 with instantaneous
... \Minescript-Aimbot\bow_aimbot --vel-mode=ema --vel-alpha=0.6 --vel-instant=0.5

# Windowed average with small window (4), blend 30% inst / 70% avg
... \Minescript-Aimbot\bow_aimbot --vel-mode=avg --n-avg=4 --vel-instant=0.3
```

Supported flags:

- `--vel-mode=latest|ema|avg`
- `--vel-alpha=<float>` (EMA alpha)
- `--n-avg=<int>` (window size)
- `--vel-instant=<float>` (instantaneous weight 0..1)

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
