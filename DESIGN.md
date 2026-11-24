---
name: Neon Hallows Arena
description: An original Halloween survival arcade game with Canvas artwork and compact keyboard-first chrome.
colors:
  orange: "#ff7a18"
  orange-hover: "#ffa35d"
  action-ink: "#211024"
  cyan: "#00f0ff"
  violet: "#a855f7"
  green: "#39ff88"
  gold: "#ffcf83"
  red: "#ff7e87"
  costume-ghost: "#b98bfa"
  costume-vampire: "#fb6f96"
  costume-witch: "#79ffad"
  costume-skeleton: "#f2e4c2"
  costume-zombie: "#c7e96c"
  ground: "#10091d"
  arena: "#0a0018"
  arena-floor: "#130722"
  arena-grid: "#251434"
  panel: "#171024"
  raised: "#241631"
  edge: "#4b355c"
  muted: "#bba9cb"
  light: "#fff4e6"
  readout: "#100920ed"
  readout-edge: "#4b355cb8"
  meter-track: "#352543"
  veil: "#0a0018c9"
  card: "#22132d"
  card-hover: "#352144"
  card-edge: "#826234"
typography:
  display:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "4.5rem"
    fontWeight: 700
    lineHeight: 1
    letterSpacing: "-0.04em"
  display-accent:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "2.25rem"
    fontWeight: 700
    lineHeight: "2.5rem"
    letterSpacing: "0.18em"
  headline:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "3rem"
    fontWeight: 600
    lineHeight: 1
    letterSpacing: "-0.04em"
  title:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "1rem"
    fontWeight: 600
    lineHeight: "1.5rem"
  title-small:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "0.875rem"
    fontWeight: 600
    lineHeight: "1.25rem"
  card-title:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "1rem"
    fontWeight: 600
    lineHeight: "1.25rem"
  body:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "1rem"
    fontWeight: 400
    lineHeight: "1.5rem"
  body-small:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "0.875rem"
    fontWeight: 400
    lineHeight: "1.25rem"
  label:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "0.75rem"
    fontWeight: 600
    lineHeight: "1rem"
  score:
    fontFamily: '"Avenir Next", system-ui, sans-serif'
    fontSize: "2.25rem"
    fontWeight: 600
    lineHeight: "2.5rem"
rounded:
  square: "0px"
spacing:
  2xs: "2px"
  xs: "4px"
  sm: "8px"
  md: "12px"
  lg: "16px"
  xl: "24px"
  2xl: "32px"
components:
  button-primary:
    backgroundColor: "{colors.orange}"
    textColor: "{colors.action-ink}"
    typography: "{typography.title}"
    rounded: "{rounded.square}"
    padding: "8px 12px"
  button-primary-hover:
    backgroundColor: "{colors.orange-hover}"
  button-quiet:
    backgroundColor: "{colors.panel}"
    textColor: "{colors.light}"
    typography: "{typography.title-small}"
    rounded: "{rounded.square}"
    padding: "8px 12px"
  button-quiet-hover:
    backgroundColor: "{colors.raised}"
  keycap:
    textColor: "{colors.light}"
    typography: "{typography.label}"
    rounded: "{rounded.square}"
    padding: "2px 4px"
  readout:
    backgroundColor: "{colors.readout}"
    textColor: "{colors.light}"
    typography: "{typography.label}"
    rounded: "{rounded.square}"
    padding: "{spacing.sm}"
  upgrade-overlay:
    backgroundColor: "{colors.veil}"
    textColor: "{colors.light}"
    typography: "{typography.headline}"
    padding: "{spacing.xl}"
  upgrade-card:
    backgroundColor: "{colors.card}"
    textColor: "{colors.light}"
    typography: "{typography.card-title}"
    rounded: "{rounded.square}"
    padding: "{spacing.md}"
  upgrade-card-hover:
    backgroundColor: "{colors.card-hover}"
  results-strip:
    textColor: "{colors.light}"
    typography: "{typography.title}"
    padding: "8px 4px"
---

# Design System: Neon Hallows Arena

## Overview

**Creative North Star: "A carved pumpkin in a dark arcade arena"**

A dim violet grid gives the angular Canvas silhouettes and lit jack-o'-lantern room to stand out. Bone-white type and fine rules frame the arena and keep its center open during combat.

Costumes read through silhouette, color, and an ability label. Cards and meters use the same compact type and square edges as the rest of the interface.

**Key Characteristics:**

- Deep violet ground and a faint 32-unit grid
- Faceted Canvas artwork with bright gameplay cues
- Compact square controls and tabular readouts

## Colors

- **Primary.** Pumpkin orange marks “Hallows,” primary actions, HP, and Pumpkin effects. The button pairs orange with dark plum text and lightens on hover.
- **Secondary.** Electric cyan identifies the player and the default reticle and shots. It also marks dash progress and keyboard focus.
- **Tertiary.** Violet marks bats and arena effects. Green marks “Arena” and zombie accents. Gold identifies XP, upgrade details, and results. Coral marks boss warnings. Each costume supplies its own drop, gear label, and reticle tint.
- **Neutral.** Violet-black surrounds the field. Dark plum separates the floor, borders, HUD, cards, and veil. Bone white carries readable text and muted lilac carries labels and supporting copy.

## Typography

Use `"Avenir Next", system-ui, sans-serif` throughout. The desktop title uses a tight 700-weight display (4.5rem) with a smaller, tracked “Arena” line (2.25rem). Dialog headlines use 600 weight (3rem). Actions and card titles use 600 weight (0.875–1rem). Supporting copy uses 400 weight (0.875–1rem), with the title introduction capped at 32ch. HUD labels and controls use 600 weight (0.75rem). Tabular numerals stabilize scores, counters, timers, and keycaps.

## Layout

The centered shell caps at 1088px and normally leaves 24px gutters. The 960 × 600 logical Canvas scales to an 8:5 arena and draws at device pixel ratio. On desktop the title sits to the left of the carving and the controls wrap below the frame.

| Query | Implemented change |
| --- | --- |
| Arena width ≤ 880px | The display drops to 3.75rem. |
| Arena width ≤ 735px | The display drops to 3rem and “Arena” to 1.5rem. Title padding and wardrobe spacing tighten. |
| Viewport width ≤ 640px | Gutters drop to 12px. The title and artwork stack in flow. HUD insets drop from 12px to 4px. Dialog states reserve at least 310px and retain three upgrade columns with 4px gaps. |
| Viewport height ≤ 660px and width ≥ 641px | The shell uses a height-based width, 8px vertical padding, and a 32px top rail. |

Play uses a keyboard and mouse at every width.

## Elevation & Depth

Layer the HUD over the field and the translucent violet veil over the HUD when a dialog opens. Thin borders and darker fills define depth. Only the title and its introduction cast shadows in the DOM. Their dark halos keep the text readable over Canvas artwork.

## Shapes

Use square corners and 1px rules for controls, panels, and the arena frame. Gold corner marks pick out the top-left and bottom-right of the frame. Faceted silhouettes, circular pickup rings, and diamond XP drops give Canvas objects distinct outlines.

## Components

- **Actions and keys.** Orange buttons enter, resume, or restart the run. Quiet plum buttons handle sound and returning to the title. Both use a 2px cyan focus outline with a 3px offset and move down 1px while pressed. The standard transitions are 240ms for background and border and 280ms for the press, using `cubic-bezier(.22, 1, .36, 1)`.
- **HUD.** HP and wave sit top-left, with score and best top-right. Costume, level and XP, and dash sit along the bottom. The flat meters are 4px high. The centered boss meter is 8px high and follows the boss tint. A status banner reads “BOSS APPROACHES” or “WAVE N CLEAR.”
- **Wardrobe.** The title pairs 24px Canvas icons with “Witch +1 shot” and “Pumpkin Splash damage.” A costume pickup updates the HUD icon and label, draws a 550ms ring, and shows the equipped name and ability detail for 2.6s.
- **Upgrade.** “Level N upgrade” centers three square cards over the dimmed fight. Each shows a gold-outlined glyph, a numbered keycap, a title, an effect, and a stack count. Hover and focus brighten the plum fill and gold border. Capped cards show “MAX · N stacks” with reduced opacity. The first enabled card receives focus and the dialog cycles Tab focus among enabled buttons.
- **Pause and results.** “Paused” offers “Resume.” “Game over” pairs a gold points total with Best, Wave, Kills, and Survived. “NEW BEST” appears when the run sets a record. “Play again” restarts and “Title screen” returns to the cover.
- **Controls.** `Enter` starts from the title. `WASD` or the arrow keys move, the mouse aims, and holding left click fires. `Space` dashes, `P` pauses or resumes, and `M` toggles sound. `1`–`3` select an upgrade and `R` restarts from results. Dialog actions also support standard keyboard button activation.
- **Reduced motion.** The preference disables CSS transitions, freezes title ambience and standard enemy poses, removes the drop-ring pulse, lowers effect opacity, and fixes the opacity of the boss warning wash. Combat and threat cues stay visible.

## Do's and Don'ts

- Do keep visible UI copy in English and use text alongside color for key state changes.
- Do keep the interface at the field edges during combat and reserve the centered veil for modal states.
- Don't load external fonts, artwork, or sound. Use the local font stack, original Canvas art, and synthesized audio.
