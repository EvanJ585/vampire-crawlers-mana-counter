# Mana Curve Counter

A static, browser-only mana curve counter for Vampire Crawlers-style deck drafting.

## What it does

- Starts with mana costs `0` through `5`.
- Lets you add the next exact cost bucket from the side button.
- Tracks card counts, total cards, average cost, max occupied cost, and target counts.
- Autosaves to browser `localStorage`.
- Supports undo and reset.
- Uses a combo-ladder target model that heavily favors low-cost cards.

## Target model

For visible costs `0..maxCost`, each cost uses:

```js
weight(cost) = (maxCost + 1 - cost) ** 2
```

The app normalizes those weights into percentages, then rounds target card counts with largest-remainder rounding so targets always add up exactly to the current deck total.

## GitHub Pages

This project is a plain static site. Publish from the repository root on the `main` branch.
