# Learning from travel diaries to enrich synthetic populations

## Research question

Can travel diaries used during training help generate more realistic combinations of transport attributes than a model trained on demographics and transport attributes alone?

The aim is a synthetic population suitable for activity-based transport modelling. Start with Greater Melbourne; extend geographically only after testing transferability.

## The idea in one example

Consider a household with two employed adults, one child and one car. We know their ages, occupations, income and home area. We want to add:

- Each member's driving-licence category.
- The number of bicycles in the household.
- Each worker's recent weekday working-from-home (WFH) frequency.

These attributes should form plausible combinations within the household. Getting the overall number of drivers or bicycles right does not necessarily reproduce those combinations. Different households with similar demographics should still have different plausible outcomes.

## Proposed approach

1. **Build a demographic core.** Use an established household-consistent synthesis method with Census information. Retain household links, age, sex, employment, student status, occupation, household composition, income, dwelling characteristics and geography. Keep household vehicle counts where definitions align.
2. **Learn from VISTA households.** Train a joint household model using demographics, transport attributes and travel-diary summaries: trips, purposes, modes, timing and time away from home. Begin with a probabilistic latent-class model that represents shared household patterns without assigning rigid personas.
3. **Enrich synthetic households.** Supply only the core attributes and geographic context. Generate licence, bicycle and WFH attributes together. Travel diaries are training information; synthetic households do not need diaries.
4. **Allow conditional completion.** If attributes are added later, condition on values already assigned rather than generating each module independently.

An inferred mobility profile adds no new observed information about a synthetic person. Its possible benefit is helping the model learn useful dependencies from limited survey data. This benefit must be demonstrated.

## Data and scope

The published VISTA dictionaries include car-licence categories, household bicycle counts and previous-week WFH indicators. Use these measured variables rather than assumed attitudes or PT-pass ownership. Bicycle count is not individual bicycle availability; recent WFH is not a permanent preference.

Proposed model-development data are VISTA 2022–23 and 2023–24, with 2024–25 reserved for a later-period test. Confirm missingness, coding consistency and sample support before fixing the design. Align Census and survey definitions and dates; attaching newer mobility attributes to a 2021 demographic core does not establish a representative current-year population.

## The decisive test

Compare the same household model trained **with and without travel-diary information**. Include household donor matching and a strong joint generator as practical benchmarks. All methods receive the same available predictors, including occupation, cars and geography.

Split data by household before training. For unseen households, hide the target attributes and all diaries. Compare generated combinations with observed distributions using survey weights and household-level uncertainty estimates.

Prioritise:

- Driver counts relative to household cars and workers.
- Bicycles combined with driving licences and WFH.
- Joint accuracy within relevant household groups, not just overall totals.
- Valid records and realistic diversity.
- Performance with smaller training samples and in the later survey period.

Check that gains survive any population calibration. Then run a limited AToM comparison with fixed parameters and independent travel observations. Different simulation outputs show sensitivity; improved agreement demonstrates utility.

## Contribution and decision rule

The proposed contribution is evidence that **behavioural information during training improves joint transport-attribute synthesis when behaviour is unavailable at generation time**. Joint synthesis, latent classes and modular outputs are not sufficient novelty on their own.

Proceed first with the held-out survey experiment. If the method only beats separate attribute models, the evidence supports joint modelling, not behavioural training. If it does not reliably improve on the matched model without diaries, retain the simpler approach.

Full activity-schedule generation and household adaptation to interventions belong to a separate study.
