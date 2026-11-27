# Set up your own Supper Board

## What you need

- **A Claude account** with artifacts and scheduled tasks. Features vary by plan, so check [support.claude.com](https://support.claude.com).
- **A tablet for the kitchen.** Optional. See [kitchen-tablet.md](kitchen-tablet.md).

## 1. Publish the board

Attach [`board/supper-board.html`](../board/supper-board.html) to a Claude chat and ask:

> Publish this file as an artifact exactly as it is, and declare the `db` and `user` capabilities so it has a shared database. Don't change the design.

Claude gives you a private link. That link is your board. The page only saves data when it runs as a Claude artifact.

## 2. Load your first week

Ask Claude:

> Load a first week into my Supper Board. Use the data model in guides/data-model.md and the rules in automation/weekly-plan-task.md. Save my food guidelines in plan/current and add my staples.

## 3. Turn on the weekly task

Ask Claude to create one scheduled task with the prompt in [`automation/weekly-plan-task.md`](../automation/weekly-plan-task.md). Fill in the `[brackets]` first. Make sure the task can run without approval, because nobody is there to approve it on Friday evening.

## 4. Shop

On Saturday morning, open the board, tap **Copy list**, and shop at Coles or Aldi. When you are back, tap **Done shopping**.

## Change it

- **Rhythm:** 3 cook nights a week (Saturday, Monday, Wednesday), each making 2 portions, plus a flexible Friday. Change the rhythm in the task prompt and in your guidelines.
- **Food rules:** edit `plan/current.guidelines` (ask Claude), or add requests on the Feedback tab.
- **Colours:** ask Claude to change the variables at the top of the page's `<style>`.
