# Scoring

Scores will be automatically calculated for each Trial as a combination of cost and performance metrics. A team's final score will be calculated as the sum of scores for each of the competition Trials.


## Cost metrics

The following values are calculated for a team's system setup.
As teams are to use the same system setup for all Trials, the values will remain unchanged between Trials.
The value in bold will be used in the final score calculation for a Trial.

1. System Cost (SC): Cost of a team's system. Sum of:
    1. $500 for each logical camera used.
    1. $100 for each other sensor used (break beam, proximity, laser scanner).
1. Average Cost (AC): Average system cost for all teams.
1. **Cost Factor** (CF): Teams that have the average System Cost will have a Cost Factor of 1. Teams with a higher System Cost will have a Cost Factor <1 which will penalize their higher System Cost.

The generalized Cost Factor for a team is calculated as:

```
CF = [{(AC / SC) - 1} * m] + 1
```

where `m = 4` is the cost factor multiplier.

## Performance metrics

Performance metrics that cover both completion and efficiency are calculated for each Trial separately.
Completion captures the quality of the kits submitted (that the kits contain the correct parts in the correct position/orientations); efficiency captures the responsiveness in assembling kits (that the orders were filled quickly).

There are up to two Orders requested during each Trial.
The following values are calculated for each Order requested in a Trial.
The values in bold will be used in the final score calculation for a Trial.

1. **Completion Score** (CS), sum of:
    1. Part presence: One point for each correct part on the tray.
    1. All parts: Points totaling the number of parts, if and only if all parts are on the tray and no additional unwanted parts are on the tray.
    1. Part pose: One point for each part that is in the correct pose (location and orientation) on the tray. The location must be within 3cm of the target and the orientation must be within 0.1 radians.
1. Order Time (OT): The time taken to complete the Order, measured from the time the Order was first requested.
1. Average Time (AT): Average time for all teams to complete the Order.
1. **Efficiency Factor** (EF):  Teams that have the average Order Time will have an Efficiency Factor of 1. Teams with a higher Order Time will have an Efficiency Factor <1 which will penalize their slower system response.

The generalized Efficiency Factor for an Order is calculated as:
```
EF = AT / OT
```

`CS{i}`, `EF{i}` are the values for the `i`th Order requested in a trial, `i = 1,2`.

## Trial score calculation

The final score for a trial is calculated as follows: 
```
Trial Score = CF * (CS1 + CS2)/2
            + EF1 * CS1
            + EF2 * CS2 * h
```

where `h = 3` is the high-priority factor that encourages quick response to the second, higher priority, order that is issued.