# Data model

The board keeps everything in its artifact database: JSON documents grouped into collections. The page, the scheduled tasks, and you (through Claude) all read and write the same documents. Dates are local `YYYY-MM-DD` strings.

## Collections

### `meals`: the live week plan
One document per night.

| Field | Type | Notes |
|---|---|---|
| `date` | string | `2026-10-05` |
| `kind` | `"cook"` \| `"leftovers"` \| `"flex"` | Drives the colored chip and the "cook night 2 of 3" count |
| `title` | string | "Chicken fajitas" |
| `details` | string | One line under the title |
| `recipe` | object | `{serves, time, oven?, ingredients: [], steps: [], tip}` |
| `from` | string | Leftover nights only: the id of the cook meal, which links to its recipe |
| `thaw` | string | Optional. What to move from freezer to fridge **the night before**, e.g. "the chicken thighs (about 400 g)" |
| `thawDone` | bool | Set when someone taps "Done, it's in the fridge" |
| `rating` | 0–5 | Set from the stars |

### `draft`
Not used. The Friday task writes the new week straight into `meals`.

### `history`
Past meals, kept so ratings add up across plans.

### `notes`
`{meal: <meal id>, text, at}`, for example "try with angel hair next time."

### `ideas`
`{text, at}`: requests for the next plan, like "more fish" or "busy week of the 20th."

### `grocery`
`{text, at}`: extras for the next shopping list.

### `staples`
`{name, group, status, order}`. `status` is `"have"`, `"low"`, or `"unknown"`. "Low" adds the item to the next shopping list.

### `freezer`
`{name, forMeal, at}`: what's in the freezer and what it's for.

### `plan` (two documents)

**`plan/current`**

| Field | Notes |
|---|---|
| `start`, `end` | Range of the live plan |
| `guidelines` | Household food rules, which the planner reads every time |
| `status` | `active` → `list_ready` → `shopped` |
| `pickup` | Shopping day, e.g. "Sat 28 Nov, morning" |
| `statusNote` | One-line note shown in the banner, e.g. "24 items on the list." |

**`plan/draft`**: this week's shopping list

| Field | Notes |
|---|---|
| `start`, `end`, `pickup` | The week's range and shopping day |
| `summary` | What's new and what's returning |
| `prep` | "Freeze on arrival: …" |
| `groceries` | `[{section, items: []}]` |
| `orderText` | The paste-ready list behind **Copy list** |
| `included` | `{grocery: [ids], staples: [ids]}`, cleared when you tap "Done shopping" |

## Status flow

```mermaid
stateDiagram-v2
  [*] --> active
  active --> list_ready: Friday task writes the week and the list
  list_ready --> shopped: you tap "Done shopping"
  shopped --> list_ready: next Friday
```
