# Slayer 2 — Damage Optimiser

A build calculator for the Roblox game **Slayers 2**. Enter your character's stats and it
brute-forces **every valid combination of equipment and titles** to find the loadout that
maximizes your **M1 (basic attack) hit damage**, then shows the winning build and a full
damage breakdown.

**▶ Live tool:** https://j4ck7232.github.io/slayers2-m1-damage-optimizer/

It's a single self-contained HTML page — no account, no install, no data leaves your browser.

---

## What it does

- **Exhaustive search, not a guess.** Because only flat damage (`d`) and the damage
  multiplier (`dm`) matter for M1, and both are additive, the optimum always lies on the
  Pareto front of achievable `(Σd, Σdm)`. The tool computes that front over all legal
  equipment loadouts and title combinations and returns the true maximum.
- **Correct damage model.** `Final M1 = (total additional damage + hidden mastery bonus) × total additional damage factor`.
  The hidden mastery bonus is added **before** the multiplier, and multipliers stack
  **additive-to-1** (a 1.05× and a 1.10× give 1.15×, not 1.155×) — both verified in game.
- **Respects the real rules.** 5 equipment slots total, max 1 Haori, and the Outfits rule
  (a Uniform alone, a lone Top, a lone Bottom, or a Top + Bottom pair).
- **Ties are shown, not hidden.** When several items or layouts produce the same peak, each
  slot lists every interchangeable option so you can use whatever you own.
- **"What if I don't have…"** — remove any equipment you can't get and the search instantly
  rebuilds your best loadout from what's left.

## How to use it

1. Open the [live tool](https://j4ck7232.github.io/slayers2-m1-damage-optimizer/).
2. Fill in your own stats (all fields start blank/neutral):
   - **Skill-tree damage** (3.1 is the max).
   - **Mastery level** (0–400) — used to estimate the hidden bonus, or enter a measured value.
   - **Katana** and **Clan** — *Additional Damage* and *Additional Damage Factor* exactly as
     shown on your character sheet (this already includes any Refinement/Tier).
   - **Titles owned** — tick the Combat titles you actually have.
3. Read off your optimal loadout, the peak damage, and the breakdown. Use **What if I
   don't have…** to exclude gear you can't obtain.

## About the data (please read)

All item stats, title stats, and the damage formulas in this tool were **recorded and
verified by hand through in-game testing** — they are **not** official developer data.
A few mechanics are deliberately left as estimates or manual inputs because they could not
be pinned down:

- The **hidden mastery bonus** uses a linear fit (`≈ 13.80 − 0.0271 × (400 − level)`). Only
  the slope and the level-400 anchor are confirmed; the low-level offset is unverified, so
  there's a "measured" override.
- The **Refinement/Tier** system (Nightfall/Firstlight items) has no solved scaling formula,
  which is why Katana and Clan stats are entered directly from your own sheet rather than
  computed from a catalog.

So: treat the numbers as a strong, tested best-effort, not gospel. If something looks off in
game, trust your own character sheet.

## Contributing / reporting wrong stats

Corrections are very welcome — accuracy is the whole point.

- **Report an incorrect stat or bug:** open an [Issue](../../issues) with the item/title
  name, the value the tool shows, the value you see in game, and (ideally) a screenshot.
- **Fix it yourself:** the catalog lives in plain JavaScript arrays near the top of
  [`index.html`](./index.html) (`FREE`, `HAORI`, `UNIFORMS`, `BOTTOMS`, `SHIRTS`, `TITLES`).
  Edit the relevant `{ d, dm, names }` entry and open a Pull Request.

## Development

There is no build step or framework. The entire app — HTML, CSS, and vanilla JavaScript —
is inlined in a single file, [`index.html`](./index.html), which is exactly what is served
live. To work on it, open that file in a browser (or run any static server, e.g.
`python -m http.server`) and edit.

## Disclaimer

This is an unofficial, fan-made tool. It is not affiliated with, endorsed by, or connected
to the developers of Slayers 2. All game names are property of their respective owners.

## License

[MIT](./LICENSE) © 2026 J4ck7232 — questions welcome on Discord: **ej4ck7232**
