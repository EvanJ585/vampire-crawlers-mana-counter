# Vampire Crawlers Card Counter

A static, browser-only card counter for Vampire Crawlers-style deck drafting.

## What it does

- Starts with mana costs `0` through `5`.
- Lets you add the next exact cost bucket from the side button.
- Tracks card counts, total cards, target counts, and target percentages.
- Tracks wild cards separately with no mana number and keeps them out of target ratios.
- Autosaves to browser `localStorage`.
- Supports undo and reset.
- Uses a combo-ladder target model that favors low-cost cards and reacts to high-cost cards already in the deck.

## Target model

For visible costs `0..maxCost`, each cost uses:

```js
weight(cost) = (maxCost + 1 - cost) ** 2
```

The app uses those weights for the main curve, then adds a slow-growing high-cost floor so 5-cost cards begin showing up around the mid-20s and gain another target copy around 40 numbered cards. After that, a support-ladder pass raises lower-cost targets when the deck already has higher-cost cards. For example, 4 copies of a `2`-cost card push the `1`-cost target to at least 4. Wild cards count toward the deck total, but stay separate from numbered mana targets.

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
