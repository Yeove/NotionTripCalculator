# Trip Calculator

Work out who pays who after a group trip, in the fewest possible transfers.

Enter each person's net balance — positive if the group owes them, negative if they owe the group — and it returns the shortest list of payments that squares everyone up. Debts flowing both ways between two people cancel out automatically.

**Live at [calculator.yeove.com](https://calculator.yeove.com)**

## How it works

Balances are matched largest debtor to largest creditor, repeatedly, until everyone is at zero. That gives at most `creditors + debtors − 1` transfers, and the page tells you when the result is provably the minimum. Everything runs in integer cents, so rounding never leaves a stray penny.

If your balances don't sum to zero, the header says how far off they are — usually a purchase missing a payer or a splitter.

## Notes

Single file, no build step, no dependencies beyond Poppins and [Maple Mono](https://github.com/subframe7536/maple-font). Nothing is stored or sent anywhere; close the tab and it's gone.

To host it yourself, drop `index.html` in a repo and turn on GitHub Pages.

## Getting your balances

If you track shared purchases in a Notion database with a "Who Paid" and a "Who Split" column, add one formula column per person:

```
if(contains(prop("Who Paid"), "NAME"), prop("Price"), 0)
  - if(contains(prop("Who Split"), "NAME"), prop("Price Split"), 0)
```

Sum each column in the table footer. Those sums are the net balances to paste in here.

## License

MIT
