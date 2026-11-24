# Neon Hallows Arena

## Entry details

- Devpost draft 1316747
- Category · Costume Contest
- Tagline · Survive the neon Halloween arena — grab costumes, gain powers, slay the bosses.

## Project description

### Inspiration

The idea was to make a costume change the next decision a player makes in a fight. In this Halloween arena, getting dressed up can be the difference between splitting your shots and clearing space with an explosion.

### What it does

Neon Hallows Arena is an arcade survival game of escalating monster waves. Walk over a costume to swap powers on the spot. A Witch adds a projectile, Pumpkin shots splash on impact, and a Ghost dashes through the horde. Three more costumes change how you heal or deal critical damage. You can wear one at a time, so a drop can be worth stepping around.

XP unlocks a choice of three permanent upgrades. Every fifth wave brings a boss, beginning with the Pumpkin King and his telegraphed charge. Defeating a boss earns points and guarantees a fresh costume. The arena saves your best score in your browser.

### How it was built

The game is a single HTML file. Canvas draws the arena, characters and effects from code, and Web Audio generates the sound effects. The fixed-step simulation stops while the upgrade cards are open. Costume stats are recomputed from the current outfit and the cards earned during the run, so taking off a costume also removes its power.

### Controls

Use WASD or the arrow keys to move. Aim with the mouse and hold left click to shoot. Space dashes, P pauses, and M toggles sound. Click a card or press 1, 2, or 3 to select it. On the results screen, press R to play again.

## Local media

- [Costume decision](screenshots/01-costume-choice.png)
- [Pumpkin King charge warning](screenshots/02-pumpkin-king.png)
- [Upgrade selection](screenshots/03-upgrade-cards.png)
- [Gameplay reel](demo/neon-hallows-arena-demo.mp4)

## Before submission

- [ ] Confirm this year's official cutoff, repository, video hosting and Kiro usage requirements in Devpost.
- [ ] Verify and add the public game, source and video URLs to the draft.
- [ ] Add a description of Kiro's actual contribution from a recorded Kiro session. The workspace contains `.kiro` specifications for the project.
- [ ] Select Costume Contest, preview the media and controls, then submit when ready and retain confirmation.
