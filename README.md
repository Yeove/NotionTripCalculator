# Trip Calculator

Work out who pays who after a group trip, in the fewest possible transfers.

**Live at [calculator.yeove.com](https://calculator.yeove.com)**

## How it works

Balances are matched largest debtor to largest creditor, repeatedly, until everyone is at zero. That gives at most `creditors + debtors − 1` transfers, and the page tells you when the result is the minimum.

## Getting your balances

If you track shared purchases in a Notion database with a "Who Paid" and a "Who Split" column, add one formula column per person:

```
if(contains(prop("Who Paid"), "NAME"), prop("Price"), 0)
  - if(contains(prop("Who Split"), "NAME"), prop("Price Split"), 0)
```

Sum each column in the table footer. Those sums are the net balances to paste in here.

## License

MIT
