# Supper Board

A kitchen board for one person. It shows tonight's dinner with its recipe, the week's plan, when to thaw things, and the shopping list. Every Friday evening Claude writes next week's meals and a shopping list for Coles or Aldi, so the shopping is done on Saturday morning.

## What it does

**On your phone or a kitchen tablet:**
- **Tonight:** what's for dinner. Tap it for the recipe, with ingredients you can tick off and a "keep screen on" button for cooking.
- **This week:** 3 cook nights (Saturday, Monday, Wednesday). Each recipe makes 2 portions, 1 for that night and 1 for the leftover night. Friday is a flexible night.
- **Thaw reminders:** the night before a meal that uses frozen meat, the board says "Before bed: move the chicken to the fridge", with a button to mark it done.
- **Push back a day:** slide tonight's meal and everything after it later by 1 or 2 days, with Undo.
- **Ratings and notes:** star each cook night and leave notes like "less chilli next time".
- **Shopping:** the week's shopping list with a **Copy list** button, extras you add yourself, pantry staples you mark Have or Low, and a freezer list.
- **Requests:** "more fish", "nothing heavy next week". The next plan uses them.

**On a schedule (Friday evening):** Claude moves past meals to history, reads every rating, note, request, freezer item and staple, writes next week's recipes, and saves the shopping list to the board.

## What's in this repo

```
board/supper-board.html          The board (publish this as a Claude artifact)
automation/weekly-plan-task.md   Friday scheduled-task prompt (fill in the [brackets])
guides/
  setup.md                       Build your own, step by step
  data-model.md                  Every collection and field the page uses
  kitchen-tablet.md              Tablet notes, kiosk mode, mounting
```

## Build your own

Start with **[guides/setup.md](guides/setup.md)**. In short:

1. Publish `board/supper-board.html` as a Claude artifact with the `db` and `user` capabilities.
2. Ask Claude to load a first week, using [the data model](guides/data-model.md).
3. Ask Claude to create the Friday scheduled task from [`automation/weekly-plan-task.md`](automation/weekly-plan-task.md).
4. On Saturday, tap **Copy list** and shop. Tap **Done shopping** when you are back.

## Limitations

- The board only runs as a Claude artifact. Hosted somewhere else, it has nowhere to save data.
- The board can't push notifications. The Friday task notifies the account owner when it finishes.
- Scheduled-task and artifact features depend on your Claude plan and may change.
- The meal plans and recipes are written by an AI. Check cooking temperatures and allergens yourself.
- Store notes such as "(Coles)" are a guess about stock, not a live check.

Based on the original Supper Board project. MIT licence.
