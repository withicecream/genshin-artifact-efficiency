# Genshin Artifact Efficiency — Safe Cleaner

A single, dependency-free `index.html` that takes a **GOOD** export of your
Genshin Impact artifacts and visualizes them as **Keep / Maybe / Discard** so
you can clean your inventory without throwing away a real keeper.

Everything runs **client-side in your browser**. Your artifact data is never
uploaded anywhere.

## Use it

1. Export a GOOD file from [Genshin Optimizer](https://frzyc.github.io/genshin-optimizer/)
   (Database → Export) or any scanner (Adepti / Amenoma / Artiscan).
2. Open the tool (see below), click the file picker, choose your GOOD file.
3. Review the color-coded table. Tune the thresholds if you want a stricter or
   looser cut, then **Recalculate**.

## Viewing online without external hosting

- **GitHub Pages** — repo *Settings → Pages → Deploy from branch*, pick the
  branch and `/ (root)`. Served at
  `https://<you>.github.io/genshin-artifact-efficiency/`.
- **htmlpreview** (zero setup) —
  `https://htmlpreview.github.io/?https://github.com/<you>/genshin-artifact-efficiency/blob/<branch>/index.html`
- **Local** — just open `index.html` in any browser.

## Safety model (Maximum-safety mode)

Genshin damage depends on each character's exact formula, so this tool does
**not** guess formulas. Instead it asks a strictly safer question:

> Is there *any* stat archetype — crit, ATK, HP, DEF, EM/transformative-
> reaction, ER/support, or healing — for which this artifact could be good?

For each artifact it scores every archetype as
`Σ (substat roll value × archetype weight × main-stat fit)` and keeps the best.
An artifact is only ever marked **Discard** when its **optimistic** score —
assuming *every remaining upgrade roll lands perfectly* into its best
substat — still can't reach the "useful" bar for any archetype. That makes
false discards structurally impossible: the tool over-keeps rather than risk
cutting a piece some character's formula would value (HP/DEF/EM/non-crit
characters included — the EM archetype carries **no crit weight**, so
transformative-reaction pieces are judged correctly).

Locked and equipped artifacts are always kept. 3★/low-rarity pieces are
flagged Discard by default (toggleable).

## Safe cleanup workflow (no deletion here)

1. Click **Export GOOD (keepers locked)** — produces a GOOD file with every
   Keep/Maybe artifact `lock: true` and discardables unlocked.
2. Re-import that file into Genshin Optimizer.
3. In-game, lock the pieces GO shows as locked, then trash the unlocked ones.

You never delete anything from this tool — it only recommends and marks.
