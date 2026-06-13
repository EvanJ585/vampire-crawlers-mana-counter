# Mana Curve Counter

A static, browser-only mana curve counter for Vampire Crawlers-style deck drafting.

## What it does

- Starts with mana costs `0` through `5`.
- Lets you add the next exact cost bucket from the side button.
- Tracks card counts, total cards, target counts, and target percentages.
- Tracks wild cards separately as flexible combo fillers with no mana number.
- Autosaves to browser `localStorage`.
- Supports undo and reset.
- Uses a combo-ladder target model that heavily favors low-cost cards.

## Target model

For visible costs `0..maxCost`, each cost uses:

```js
weight(cost) = (maxCost + 1 - cost) ** 2
```

The app normalizes those weights into percentages, then rounds target card counts with largest-remainder rounding so numbered-card targets always add up exactly to the current numbered-card total. Wild cards count toward the deck total, but stay separate from numbered mana targets.

## GitHub Pages

This project is a plain static site. Publish from the repository root on the `main` branch.

If using GitHub CLI:

```powershell
gh repo create vampire-crawlers-mana-counter --public --source . --remote origin --push
gh api repos/EvanJ585/vampire-crawlers-mana-counter/pages -X POST -f source.branch=main -f source.path=/
```

If creating the repo manually on GitHub:

```powershell
git remote add origin https://github.com/EvanJ585/vampire-crawlers-mana-counter.git
git push -u origin main
```

Then open the repository settings, go to Pages, and publish from the `main` branch root.
