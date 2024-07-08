---
aliases:
  - d20 ± Xd6
date: 2024-02-01
dateModified: 2024-05-30
fileClass:
  - Note
image: 
share: true
stage: 🌱 Seedling
title: d20 ± Xd6 Checks
---

Dice checks in [[Protectors of Empai Tirkosu|PoET]] are `d20 ± [X]d6 > 10`, where X is the total difference between your modifier vs the target's modifier.

This is functionally a pretty standard check for a [[d20 System|d20 System]], with the difference being the total remaining modifier becomes that many d6's instead of a flat number.

> [!Example]+ Example Check
> I want to use my +3 athletics to bust down a difficulty 2 door. 
> Usually, this would be a "DC 12 Athletics Check" of `d20+3 ≥ 12`
> 
> PoET first simplifies out the modifiers. 
> `d20+3 ≥ 12` → `d20+3 ≥ 10+2` → `d20+1 ≥ 10`
> 
> Then, replaces whatever modifier remains with a d6. 
> `d20+1 ≥ 10` → `d20+1d6 ≥ 10`
> 
> _If I was going against a difficulty 4 door, my end result would be `d20-2d6 ≥ 10` instead._

#### Outcome

Differences in modifiers scale _fast_, basically three times faster. [^1]

> [!danger]+ Outcome Table
>
> | Chances of rolling above 10 <br>when you add N | d20+N | d20+Nd6 | _d20+(N\*3)_ |
> | ---- | ---- | ---- | ---- |
> | 0 | 50% | 50% | _50%_ |
> | 1 | 55% | 67.5% | _65%_ |
> | 2 | 60% | 84.4% | _80%_ |
> | 3 | 65% | 95% | _95%_ |
> | 4 | 70% | 99% | _100%_ |
>
> ![[./assets/images/chart (1).png|chart (1).png]]

This fits the theme [[Protectors of Empai Tirkosu|PoET]] is going for, where modifiers represent [[Protectors of Empai Tirkosu#Tiers|PoET Tiers]] of exponential narrative power – ranging from mundane to demigods, all while keeping the math small.

It quickly communicates that a tier 4 politician (e.g. a president) is _way_ more powerful than a tier 1 politician (e.g. a town mayor), because he gets to roll with _three d6's in his favor_.

It's a bit like taking [[D&D|D&D]] and saying every skill/level/modifier/etc has to fall into the levels 0, 3, 6, 9, 12, and 15. Rather than each level representing a [[d20#Each Number on a d20 Is 5%|5% Increase]], it represents a _15%_ increase – that's big.

Yes, you get the same result from a tier I vs tier 4 check as you would with a +3 vs a +12 check, but there's something to be said for deleting all little numbers between them because they aren't worth narratively tracking.

[^1]: since [[The average of any dice roll is half of its highest number plus .5|The average of any dice roll is half of its highest number plus .5]]
