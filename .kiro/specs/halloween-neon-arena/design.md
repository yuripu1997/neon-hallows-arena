# Neon Hallows Arena design

All runtime code lives in the sole public game entry point. The file opens directly or through a static server and uses browser APIs for rendering, audio, and storage. [index.html](../../../index.html)

## Runtime structure

| Component | Responsibility |
| --- | --- |
| HTML and CSS | Lay out the Canvas playfield, title, HUD, and upgrade, pause, and results dialogs. |
| `Arena` | Own the simulation and current run. Its constructor takes a random function and an event callback. The browser supplies `Math.random`, and local tests can supply a predictable sequence. |
| `ArenaArt` | Draw the player, enemies, bosses, and costume icons from Canvas paths and shapes. |
| Browser integration | Map input, run the frame loop, draw the playfield and HUD, manage focus and dialogs, synthesize audio, and store the high score. |

The Canvas uses a 960 × 600 logical field, with pointer coordinates mapped through its current bounding rectangle. The backing resolution follows `devicePixelRatio`. Separate canvases cache the arena and title backgrounds. A small atlas caches common enemy poses and XP gems, while bosses and flashes use the original path painter. The HUD refreshes at up to 30 Hz during play and refreshes immediately on a costume swap or state change. Frozen overlays keep the last render until the state or display changes.

## Clock and input

`requestAnimationFrame` accumulates at most 0.05 seconds per frame and updates the simulation in fixed 1/60-second steps. Only `playing` advances the world. The title has its own presentation clock, and modal overlays display the frozen arena.

The title starts in `menu`. Play can enter `levelup`, `paused`, or `gameover`. Selecting a card returns to play when all earned choices are resolved, and `P` or the Resume button exits manual pause. A restart resets the run and starts wave 1. The results screen also offers a return to the title.

State changes clear held input and the frame accumulator. Losing window focus clears input, and hiding the tab also pauses an active run and resets the frame clock. Movement and fire use held input. Dash, pause, mute, and card shortcuts react once per press.

## Combat and waves

The simulation stores enemies, player bullets, hostile bones, drops, and visual effects as objects in arrays. A per-run pool reuses player bullets. Swept circle tests find projectile hits and block a normal dash on contact. Each piercing bullet tracks the enemies it has already hit, and each enemy is marked defeated before its points, effects, and drops are applied. Game over takes precedence when a simulation step also crosses an XP threshold.

The player starts with 100 HP and moves at 230 px/s. The starting weapon fires four shots per second. Each projectile deals 12 base damage, travels at 560 px/s, and has a range of 520 px. Baseline critical hits have a 5% chance and deal 1.5× damage. The baseline dash travels at 700 px/s for up to 0.15 seconds, with 0.25 seconds of immunity and a 2.5-second cooldown. Damage from contact and hostile bones shares a 0.5-second recovery window.

Regular enemies enter from the four edges. A shuffled roster introduces every unlocked species before weighted selection fills the rest of each wave. Spider groups take three slots. The spawn interval drops from 1.2 seconds in wave 1 to 0.45 in wave 10, with a floor of 0.4. Regular HP scales by `1 + 0.10 × (wave − 1)`. From wave 3, each regular spawn can roll elite at 8%, with triple HP, 1.4× size, and 1.5× XP and score.

The wave director moves through spawning, warning and boss combat on fifth waves, then rest. In boss waves, one of the `8 + 4 × wave` slots is reserved for the boss. The HUD counts that slot until the boss spawns. Regular groups and pending summons wait for room under the 120-enemy cap. A wave ends after the quota and any remaining summoned enemies are cleared. The three-second rest leaves movement and pickups active.

| First wave | Boss | First HP | First defeat points | Attacks |
| --- | --- | --- | --- | --- |
| 5 | Pumpkin King | 900 | 500 | Charge every 6 s with a 0.8 s cue. Summon four bats every 10 s. |
| 10 | Ghost Lord | 2,200 | 1,200 | Fire a 12-way volley every 5 s, summon three ghosts every 9 s, and phase for 1 s every 7 s. While phased, it takes no damage. |
| 15 | Skeleton Monarch | 4,000 | 2,500 | Fire eight spiral shots every 6 s, summon two archers every 12 s, and telegraph a charge every 9 s. |

Each complete rotation multiplies boss HP by 1.5. Repeat boss rewards start at 3,000 points and rise by 500 each encounter.

## Progression and equipment

XP is cumulative. Levels 2–8 require 8, 20, 36, 56, 80, 108, and 140 XP. Each successive level adds 40 XP to the threshold. Cards are drawn without replacement from eligible entries. If only the two uncapped cards remain, a disabled `MAX` card fills the third slot.

| Upgrade | Effect per stack | Limit |
| --- | --- | --- |
| Heavy rounds | +25% base damage | Uncapped |
| Quick trigger | +20% base fire rate | 5 |
| Light feet | +12% base move speed | 4 |
| Split shot | +1 projectile with 12° spacing | 3 |
| Piercing rounds | +1 target penetrated | 3 |
| XP magnet | +60% base XP pickup radius | 3 |
| Extra heart | +25 max HP and heal 25 HP | Uncapped |
| Quick step | Multiply dash cooldown by 0.75 | 3 |

Stats are recalculated from baseline values, card stacks, and one costume slot on every selection or pickup. Max HP clamps current HP. Each dash keeps the duration, protection, and cooldown assigned when it starts, and each bullet keeps its firing stats. Vampire heals according to the costume worn when the kill occurs. The Ghost costume multiplies the card-adjusted dash cooldown by 0.70. XP pickup starts at 48 px, while costume pickup always uses 26 px. Drops of the same XP type in the same 16 px cell combine at the first gem's position and keep the full total. Elite bonus gems retain their own color and slot. The closest costume within 90 px shows its name and effect.

## Presentation and storage

The world renders on Canvas while the HUD and dialogs use HTML. Visual feedback includes enemy bursts, damage flashes, level-up rings, dash trails, and boss warnings. Browser audio starts from a user gesture and uses Web Audio oscillators and generated noise. One master gain controls sound.

The results handler compares the run score with the record and stores a new best in `localStorage` under `neon-hallows-best`. The record stays in memory during the page session if storage is unavailable.
