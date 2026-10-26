# Max's Cookbook

A single-page recipe site. Everything lives in `index.html`: the styles, the app code, and the recipe
data itself as `SEED_RECIPES` and `SEED_PLANS` near the top of the script.

No build step, no dependencies. Open `index.html` in a browser and it works.

## What the site does

- Recipes scale with the serving stepper; amounts are re-rendered as fractions
- Ingredients check off into a basket bar that fills as you shop
- Step numbers tap to mark done
- Steps with a time get a countdown timer; the tray at the bottom right tracks running timers
- "Feed me something" opens a random recipe
- Keeps the screen awake while cooking, where the browser allows it

## Adding a recipe

Add an object to `SEED_RECIPES`. The shape:

```js
{
  id: "spinach-tomato-pepper-quiche",   // unique, used as the URL hash
  title: "Spinach, Tomato and Red Pepper Quiche",
  category: "Mains",                     // becomes a filter chip
  description: "One line for the card.",
  time: "About 1 hr 20 min",
  baseServings: 4,                       // amounts scale from this
  ingredients: [
    { amount: 8, name: "large eggs" },
    { amount: 1, unit: "cup", name: "whole milk" },
    { amount: 2, unit: "tbsp", group: "Oil and seasoning", name: "extra virgin olive oil" }
  ],
  steps: [
    { title: "Heat the oven", text: "Heat the oven to 375°F." },
    { title: "Bake", minutes: 45, text: "Bake until the center barely jiggles." }
  ],
  notes: "Free text. Line breaks are kept."
}
```

Notes on the fields:

- `unit` must be one of the units in the `UNITS` map, or leave it off and fold the counting noun
  into `name` ("3 garlic cloves" is `{ amount: 3, name: "garlic cloves" }`)
- `group` starts a labeled section in the ingredient list and carries down until it changes
- `minutes` on a step is what creates the timer button
- the card emoji is picked automatically from the title by the `EMOJI` table

## Deploying

Vercel serves the repo root as a static site. No framework preset, no build command, no output
directory. Pushing to the default branch is the deploy.
