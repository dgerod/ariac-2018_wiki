# Scoring

Scores will be made up of an automatically calculated component and a score based on judges.
The automatically calculated component for each Trial is a combination of cost and performance metrics.
A team's final score will be calculated as the sum of scores for each of the competition Trials.
See [challenge.gov/challenge/ariac](https://www.challenge.gov/challenge/ariac/) for details on the judges' scoring.
Note that only automated metrics will be used during the qualification rounds of the competition.

## Stability

As outlined in the [update policy](https://bitbucket.org/osrf/ariac/wiki/2018/update_policy), changes to the scoring metrics may be made between rounds of the competition at the discretion of the competition controllers.
Qualifying teams will be made aware of the final scoring parameters in advance of the Finals of the competition.


## Cost metrics

The following values are calculated for a team's system setup.
As teams are to use the same system setup for all Trials, the values will remain unchanged between Trials.
The value in bold will be used in the final score calculation for a Trial.

1. Team System Cost (TC): Cost of a team's system. Sum of:
    1. $500 for each logical camera used.
    1. $200 for each depth camera used.
    1. $100 for each other sensor used (break beam, proximity, laser scanner).
1. Baseline System Cost (BC): Baseline system cost.
1. **Cost Factor** (CF): Teams that have the same system cost as the Baseline System Cost will have a Cost Factor of 1. Teams with a higher System Cost will have a Cost Factor <1 which will penalize their higher System Cost.

The generalized Cost Factor for a team is calculated as:

```
CF = (BC / TC)
```

where `BC = 1700` is the Baseline System Cost.

## Performance metrics

Performance metrics that cover both completion and efficiency are calculated for each Trial separately.
Completion captures the quality of the shipments submitted (that the shipments contain the correct products in the correct position/orientations); efficiency captures the responsiveness in fulfilling orders (that the orders were filled quickly).

There are up to two Orders requested during each Trial, each composed of up to two Shipments.
The following values are calculated for each Order requested in a Trial.
The values in bold will be used in the final score calculation for a Trial.

1. Shipment Completion Score*, sum of:
    1. Product presence: One point for each correct product in the shipping box.
    1. All products: Points totaling the number of products, if and only if all products are in the shipping box and no additional unwanted/faulty products are in the shipping box.
    1. Product pose: One point for each product that is in the correct pose (location and orientation) in the shipping box. The location must be within 3cm of the target and the orientation must be within 0.1 radians.
1. **Order Completion Score** (CS), sum of the completion score for each Shipment.
1. Order Time (OT): The time taken to complete the Order, measured from the time the Order was first requested.
1. Average Time (AT): Average time for all teams to complete the Order.
1. **Efficiency Factor** (EF):  Teams that have the average Order Time will have an Efficiency Factor of 1. Teams with a higher Order Time will have an Efficiency Factor <1 which will penalize their slower system response.

The generalized Efficiency Factor for an Order is calculated as:
```
EF = AT / OT
```

`CS{j}`, `EF{j}` are the values for the `j`th Order requested in a trial, `j = 1, 2`.

\*_note that products must be placed onto the base of the shipping box to count for scoring, not on top of other products._

## Trial score calculation

The final score for a trial is calculated as follows:
```
Trial Score = CF * AVG(CS)
            + EF1 * CS1
            + EF2 * CS2 * h
```

where `h = 3` is the high-priority factor that encourages quick response to the second, higher priority, order that is issued.