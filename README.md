# [Mapbots](https://mapbots.github.io): Auto-updating, programmable map of NapBots' daily performances.


### Overview

The [Mapbots](https://mapbots.github.io) app gives you a customizable overview
of the latest performance data of all [NapBots](https://napbots.com)
crypto-trading [bots](https://platform.napbots.com/strategies).
It is a powerful tool to explore allocation performances
and to find a composition that works.

Every hour, my agent in the cloud runs
'mapbots/[get-strat-data](https://github.com/mapbots/get-strat-data)',
which merges and massages the latest data from NapBots, and uploads this at
mapbots/data/[strats.json](https://raw.githubusercontent.com/mapbots/data/main/strats.json).
The Mapbots app builds on that data.

Load and study the example configurations at [mapbots.github.io](https://mapbots.github.io).
They are self-explanatory and should be easy to modify.


### Basic info

- Bots are named by maximum-four-letter abbreviations.
  This makes them consistent to use as variable names in the `calcs`.
  For example: `'cat'`, `'lion'`, `'hors'` (not horsE), etc.
  - NapBots gave these **animal names** to their bots in 2021.
    But now they've given different names to their bots again, and they
    may do so again; so here we just keep the cute names.
    Mapbots shows the bots' permanent ‘strategy-code’ identifiers too.
- Daily-performance values are shown in **tooltips**
  that appear when you mouse over the colored cells.
  Most other cells have explanatory tooltips too.
- Day-performance column headers show **date tags** like `'210801'`,
  which is shorthand for `'2021-08-01'`.
- Performance-summary columns (right part of map) show **performance factors**
  ([‘fold changes’](https://en.wikipedia.org/wiki/Fold_change)) rather than
  percentages. This is more intuitive for summarizing large,
  crypto-size wins and losses.

- Other features: creating **permalinks**, downloading as **image**,
  copying **TSV data** (click on column headers), hotkeys, etc.
  You will find it all on the map.
  For more info, check comments in the [source code](index.html).


### Customized calculations: `calcs`

Among the many customization options (incl. sizes, colors, ordering),  
`calcs` are the most powerful ones:
- Calcs can calculate the performance of any bot-allocation, based on a simple
  specification text-string. E.g. `'lion40 hors60 lev1.2'`
  generates a time-series of daily performances for an allocation of
  40% Golden Lion bot and 60% Jade Horse, at leverage 1.2.  
  > Note: allocations are calculated by simply combining individual bots'
  > performances on each day. E.g. the above example corresponds to
  > a JS function: `lev(1.2, 0.40*lion + 0.60*hors)` (where bot names represent
  > bots' performances for a given day).  
  > So these calculations make only a rough approximation of an allocation's
  > performance. Ideally, strats.json's `data.trades` could be used
  > (not implemented here); also NapBots' regular, small rebalancing trades
  > could be taken into account.  
  > Still, the approximations seem to work pretty well, and you can still verify
  > the most interesting ones in NapBots' Allocation Performance Tool.

- Calcs can auto-generate a whole range of allocations you may want to explore,
  based on a specification text-string.
  E.g. `lion0,100,5 cat0,100,5` generates calcs with the Golden Lion and
  Tanzanite Cat bots, each from 0 to 100% in steps of 5%,
  and with the condition that the total allocation is 100%.  
  You can also include additional conditions, as in:
  `hors50 peli50 spread 50 step 5 lev 1.5 cond "hors != peli"`.  
  (Watch out: a specification that generates too many combinations at once
  may freeze your browser!)
- Calcs can be specified as JavaScript functions that do anything you program
  them to do. They can show exponential-moving-averages, cumulative performances,
  differences, etc.  
  They have access to bot-related functions, e.g. `cat_prev(2)`, which returns
  the performance of the Cat bot from two days before the particular day
  for which a calculation is being done.  
  Note: the grid of cell values is calculated column-by-column, then row-by-row.


### About

Mapbots was created for personal use by a NapBots user,
who is *not* affiliated with NapBots.

I am sharing this overview- and exploration-app
so _you_ can benefit from it too. 😍

► Please share your Mapbots explorations and as Permalinks
  with the NapBots community!
  High-performance, low-drawdown bot allocations is what we're all looking for.

► If Mapbots guides you to big profits you otherwise wouldn't have known how
to get: kindly reciprocate the generosity and tip me at the address
found on the [map](https://mapbots.github.io).
🥰


### License

[AGPL-3.0](LICENSE.md).
This means you can use and modify the code, but you must share those
modifications and the code you build around it back with the community.
