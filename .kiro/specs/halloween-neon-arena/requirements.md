# Neon Hallows Arena requirements

Neon Hallows Arena is an original desktop survival game for the Kiroween Costume Contest. Players upgrade their abilities with XP and change tactics by picking up costumes, one at a time. These requirements were written in the project workspace from the development brief, build plan, and game source.

## R1. Launch and controls

- Open the English title screen by double-clicking the file or serving it over static HTTP. Both paths use the single public game entry point. [index.html](../../../index.html)
- Play offline with embedded artwork, styles, scripts, and synthesized audio. Both launch paths must reach gameplay with zero console errors and zero external asset requests.
- Start with `Enter` or the start button. Move with `WASD` or the arrow keys, aim with the mouse, and hold the left mouse button to fire. Diagonal movement matches cardinal speed, and aim follows the pointer after a viewport resize.
- Use `Space` to dash, `P` to pause or resume, and `M` to mute or unmute. A hidden tab pauses an active run. Resuming returns control with the game clock at the point where it paused.

## R2. Waves and scoring

- Start at wave 1 and level 1 with 100 HP, zero score, and an empty costume slot. Bats and spiders appear in wave 1. Zombies join in wave 2, ghosts and elite variants in wave 3, and Skeleton Archers in wave 4.
- Spawn `8 + 4 × wave` enemies, including one reserved boss slot every fifth wave. Spiders spawn in groups of three. At most 120 enemies can be active, including summons.
- On each wave clear, grant `50 × wave` points and heal up to 8 HP. Show the clear message and allow three seconds to move and collect drops before the next wave. Kill and clear rewards each count once.
- While playing, show HP, wave, remaining foes, score, best score, level, XP progress, dash recharge, and the equipped costume.

## R3. XP and upgrade cards

- Collect 8 XP to reach the first upgrade. Pause enemies, projectiles, survival time, dash recharge, and drop timers while the cards are open.
- Show three distinct cards with names, effects, and stack counts. Accept a click or `1`, `2`, or `3` on an eligible card. If two cards are eligible, display a third card marked `MAX` and keep it disabled.
- Apply one upgrade per level and keep selected stacks for the run. When a pickup crosses multiple thresholds, require each choice before resuming play.

## R4. Costume pickups

- Each defeat grants a costume drop chance by enemy type. It is 2% for a regular foe, 25% for an elite, and 100% for a boss. An elite that rolls no costume drops a 10 XP gem in addition to its regular XP.
- Show the nearby costume name and effect before pickup. The drop lasts 12 seconds of active play and equips automatically at 26 px. The XP magnet affects only gems.
- Verify that each pickup changes the player's look, the HUD, and the corresponding ability. Walk around a drop to keep the current costume. On a swap, the new power replaces the old one and XP upgrades carry over.

| Costume | Expected ability |
| --- | --- |
| Pumpkin | Hits splash for 50% of projectile damage within 70 px of impact. The direct target takes its direct hit once. |
| Ghost | Dash through foes with 0.6 s of damage immunity and a 30% shorter dash cooldown. |
| Vampire | Recover 2 HP for a regular kill or 8 HP for an elite or boss kill. |
| Witch | Fire one extra projectile per shot, in addition to any Split shot upgrades. |
| Skeleton | Crit with a 25% chance for double damage. |
| Zombie | Gain 50 max HP and recover 1.5 HP per second. Clamp current HP to the resulting maximum on swap. |

## R5. Boss waves

- After the player clears the regular enemies on every fifth wave, show a two-second warning and then the boss and its health bar. Charge attacks show a red direction marker before movement begins.
- Fight the Pumpkin King at wave 5, Ghost Lord at wave 10, and Skeleton Monarch at wave 15. Each boss has a distinct attack pattern, awards points, and drops one costume on defeat. Clear the boss and its remaining minions to advance.
- Play naturally through the first boss to wave 6. Exercise the later patterns through a reproducible test setup. At wave 20, the Pumpkin King returns with 1,350 HP. Every return multiplies that boss's previous HP by 1.5.

## R6. Results, persistence, and performance

- At zero HP, show the run score, best score, wave reached, kills, and time survived. Show `NEW BEST` when the run sets a record. `R` or the restart button begins a fresh run at wave 1.
- In the same browser and storage context, retain the best score after refresh and after a lower-scoring run. A browser that blocks storage must still support play and retain the session record until the page closes or reloads.
- Target 60 FPS on a 60 Hz desktop with 100 active enemies. Record the browser, hardware, viewport and device pixel ratio, and check that effects and projectiles expire and that spawns respect the cap. The measurement procedure is listed with browser verification. [Tasks](tasks.md)
