# Neon Hallows Arena tasks

These specifications were written in the project workspace. The local build and verification results below were recorded on November 24, 2026.

## Milestones

The build plan dates are for 2026 in Beijing time (UTC+8).

| Milestone | Planned target | Deliverable |
| --- | --- | --- |
| M1 | November 25 | Start a run, move, shoot, dash, and clear the early waves. |
| M2 | November 26 | Add the full regular roster, XP, upgrade cards, the first boss, and a restartable run with a record score. |
| M3 | November 28 | Finish the six costumes, elite encounters, and audiovisual feedback. |
| M4 | November 30 | Verify all bosses and the wave 20 rotation, measure performance, and freeze features. |
| M5 | December 2 | Publish the game and prepare the demo, screenshots, and Devpost draft. |
| M6 | December 3 at 20:00 | Check and submit the entry. Reserve December 4 for recovery. |

The development brief lists December 5 at 06:00 as the submission deadline. Confirm the official deadline and entry requirements before submission.

## Implementation

- [x] **M1** Build the single-file Canvas arena, title screen, desktop controls, combat, spawning, and wave-clear scoring.
- [x] **M2** Add five regular enemy types, XP gems, eight upgrade types, the Pumpkin King, game-over stats, restart, and a browser-local high score.
- [x] **M3** Add elites, costume drops and single-slot swaps, all six abilities, and synthesized sound and visual effects.
- [x] **M4** Add the Ghost Lord, Skeleton Monarch, rotating boss scaling, bullet recycling, and the active-enemy cap.
- [x] **M5** Write the English README and workspace specifications.

## Local verification

Environment for browser checks was macOS 15.7.3 with Chromium 149.0.7827.55 and Chrome 158.0.8127.36. System WebKit 20621.3.11.11.3 was exercised in an isolated `WKWebView` with simulated events. A manual Safari browser window and trusted audio gesture remain separate checks. The final local build has SHA-256 `56e667b04cda20cd7e26bb8b93d24cbb4985ab7e9c83872022750d6bc1dcfea7` and opens at the normal title screen. [index.html](../../../index.html)

| Milestone | Check | Observed result |
| --- | --- | --- |
| M1, M5 | Open from a local file and a static server. Check offline play, resize, input, high DPI and audio. | Chrome passed `file://` with networking disabled and a 1920 × 1200 backing canvas at DPR 2. Chromium passed loopback HTTP and file launch, keyboard movement, pointer aim after resize, dash, pause, audio start and mute. Both physical launch paths recorded zero console errors and zero subresource requests. System WebKit ran the title, start, movement, pause, game over and `R` from both entry points, with zero script or resource errors. |
| M2 | Reach level 5, defeat the Pumpkin King and enter wave 6 in one title-screen run. | Chromium scripted-input run reached wave 6 at level 8 and scored 2,755. The two-second warning, health bar, charge lane and bat summons were visible. A deterministic engine check verified exactly one boss costume and one clear reward. |
| M2, M3 | First upgrade, pause, queued levels, `MAX` slot and hidden-tab handling. | Verified three distinct cards at 8 XP, mouse and digit selection, stationary world clock while the cards were open, and pause on a simulated visibility change. A 20 XP jump required two choices. The disabled card ignored its shortcut. The XP meter shows current-level progress and matched 8 of 16 XP at 50% fill. |
| M2 | Restart and preserve the best after reload and a lower score. | Chromium ended and restarted a run at wave 1 with zero score. Its 2,755 record persisted after reload. Chrome preserved 421 when a later run scored 31. With storage blocked, returning to the title retained 42 in the same page. |
| M3 | Elite and costume odds, expiry and pickup radius. | Engine assertions covered the 8%, 2% and 25% boundaries, 10 bonus XP, 12-second expiry, preserved totals for merged XP, and 27 px versus 26 px with a full XP magnet. |
| M3 | Equip and swap out all six costumes. | Engine assertions passed impact splash, 0.6 s Ghost protection and faster dash, 2 and 8 HP kill healing, Witch spread stacking, Skeleton critical damage, and Zombie max HP and regen. Chrome reflected all six names through the actual pickup route. Repeated pickup preserved one outfit and restart reset the slot. |
| M4 | Boss attacks, invulnerability and cycling. | Engine checks covered two-second warning, charge and summons, Ghost Lord's 12-projectile volley and one-second phase, and Monarch's eight shots, two archers and charge cue. Three fixed-seed runs from wave 1 reached wave 16. Verified wave 20 Pumpkin King at 1,350 HP and 3,000 points, then wave 25 at 3,300 HP and wave 30 at 6,000 HP. |
| M4, M5 | Sustain 100 enemies, enforce the 120 cap and reset transient entities. | Chrome with hardware Canvas averaged 60.00, 59.60 and 59.90 FPS. P95 frame intervals were 16.8, 16.7 and 16.8 ms. The engine deferred spawns at 120, admitted a spawn after a slot opened, and reset active effects, bullets and enemies on restart. |

The three 30-second performance samples followed a three-second warmup on an Intel Core i5-8279U with Intel Iris Plus Graphics 655, 16 GB RAM, a 1280 × 820 Chrome viewport and DPR 1. The fixture held 100 enemies, steered the player while firing a rapid four-round Pumpkin spread, and replenished defeats. The hardware-accelerated run met the planned mean and P95 thresholds. A software-only headless browser ran below 60 FPS under the same stress. The subsequent interface fixes changed the XP label and title layout at narrow widths.

| Fixed seed | First upgrade | First costume | Wave 6 | Wave 11 | Wave 16 |
| --- | --- | --- | --- | --- | --- |
| 2 | 5.7 s | Vampire at 2.9 s | 95.2 s | 210.1 s | 325.8 s |
| 11 | 5.5 s | Zombie at 91.6 s | 94.2 s | 203.5 s | 317.0 s |
| 2026 | 5.7 s | Skeleton at 50.8 s | 89.6 s | 209.1 s | 332.0 s |

The balance timings are simulation time from scripted movement, aim and card picks. Independent play by a new player remains a useful release check.

## Release and submission

- [x] Complete the local browser and engine checks, record three balance runs, and freeze the local candidate.
- [x] Prepare the 72-second captioned reel and three screenshots from repeatable gameplay. [Local media and contest copy](../../../DEVPOST.md)
- [ ] Have a new player try the game. Verify Safari browser input and audio from a real start gesture.
- [ ] Publish the arena on GitHub Pages. Verify the public entry point in a signed-out browser and add the verified link to the README.
- [ ] Confirm current Kiroween rules. Add public links and any actual Kiro session evidence to Devpost draft 1316747.
- [ ] Verify the public game, repository, and video links from the draft, submit the entry, and retain the confirmation.
