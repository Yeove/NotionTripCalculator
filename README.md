# Trip Calculator

Work out who pays who after a group trip, in the fewest possible transfers.

**Live at [calculator.yeove.com](https://calculator.yeove.com)**

## How it works

Balances are matched largest debtor to largest creditor, repeatedly, until everyone is at zero. That gives at most `creditors + debtors − 1` transfers, and the page tells you when the result is the minimum.

## Notion Setup

This tool is meant to be used alongside tracked shared purchases in a Notion database. You'll need four columns to start:

| Column | Property type | What it holds |
|---|---|---|
| `Price` | Number | What the purchase cost |
| `Who Paid` | Multi-select | Whoever fronted the money |
| `Who Split` | Multi-select | Everyone sharing the cost |
| `Price Split` | Formula | `prop("Price") / prop("Who Split").length()` |

Then add one more formula column per person:

| Column | Property type | What it holds |
|---|---|---|
| `Net Cost - Alex` | Formula | `if(prop("Who Paid").includes("Alex"), prop("Price"), 0) - if(prop("Who Split").includes("Alex"), prop("Price Split"), 0)` |
| `Net Cost - Sam` | Formula | `if(prop("Who Paid").includes("Sam"), prop("Price"), 0) - if(prop("Who Split").includes("Sam"), prop("Price Split"), 0)` |
| `Net Cost - Robin` | Formula | `if(prop("Who Paid").includes("Robin"), prop("Price"), 0) - if(prop("Who Split").includes("Robin"), prop("Price Split"), 0)` |
| `Net Cost - Theo` | Formula | `if(prop("Who Paid").includes("Theo"), prop("Price"), 0) - if(prop("Who Split").includes("Theo"), prop("Price Split"), 0)` |

Worth pasting a note above each one, so whoever opens it later knows what it's for:

```
/* This is the total each person owes or is owed for the whole trip.
   Copy the sum of this column at the bottom of the table & paste everyone's
   name and totals into https://calculator.yeove.com/ and it'll tell you
   who needs to pay who. */
```

Each cell works out what that person fronted on that row, minus their share of it:

| Item | Price | Who Paid | Who Split | Price Split | Net Cost - Alex | Net Cost - Sam | Net Cost - Robin | Net Cost - Theo |
|---|---|---|---|---|---|---|---|---|
| Cabin booking | 144.64 | Alex | Alex, Sam, Robin, Theo | 36.16 | **108.48** | −36.16 | −36.16 | −36.16 |
| Groceries | 115.43 | Robin | Alex, Sam, Robin, Theo | 28.86 | −28.86 | −28.86 | **86.57** | −28.86 |
| Dinner out | 130.24 | Alex | Alex, Sam, Robin, Theo | 32.56 | **97.68** | −32.56 | −32.56 | −32.56 |
| Bag of ice | 2.99 | Sam | Alex, Sam, Robin | 1.00 | −1.00 | **1.99** | −1.00 | 0.00 |
| **Sum** | **393.30** | | | | **176.31** | **−95.58** | **16.86** | **−97.58** |

The ice splits three ways because Theo sat that one out, so his cell is 0.00 for that row.

Sum each `Net Cost` column in the table footer. Those sums are the net balances to paste in here. They always add up to zero; if they don't, some row is missing a payer or a splitter.

### A note on `includes` vs `contains`

You'll see `contains()` used for this a lot, and it mostly works, but it does a substring match on the whole multi-select flattened into text — so `contains(prop("Who Split"), "Sam")` is also true on a row whose splitters are Alex, **Sam**antha and Robin. Sam then gets charged for rows he wasn't on, and his total comes out low.

`includes()` matches whole list items instead, so it can't misfire that way. Use it and you never have to think about whether anyone's name is hiding inside someone else's.

## License

MIT
