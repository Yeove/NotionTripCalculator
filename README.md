# Trip Calculator

Work out who pays who after a group trip, in the fewest possible transfers.

**Live at [notioncalculator.yeove.com](https://notioncalculator.yeove.com)**


## Notion Setup

This tool is meant to be used alongside tracked shared purchases in a Notion database. You'll need four columns like so:

| Column | Property type | What it holds |
|---|---|---|
| `Price` | Number | What the purchase cost |
| `Who Paid` | Multi-select | Whoever fronted the money |
| `Who Split` | Multi-select | Everyone sharing the cost |
| `Price Split` | Formula | `prop("Price") / prop("Who Split").length()` |

Create additional views, filtered via "Who Paid", group via "Who Split"


Feed the sum totals of each person's "Price Split" into this calculator, and it'll cleanly summarize the net totals of who owes who.

## License

MIT
