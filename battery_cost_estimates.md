
written by claude on 9th Jan 2026

---
  Probability Distribution of Daily Arbitrage Profit

  Price Distribution (Based on Agile Data)

  From historical Agile data, I can construct a reasoned distribution:

  | Price Band      | % of Half-Hours | Reasoning                                                                                                                                |
  |-----------------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------|
  | < 0p (negative) | ~1.6%           | 284 plunge periods in 12 months ÷ 17,520 half-hours (https://www.sunsave.energy/solar-panels-advice/exporting-to-the-grid/agile-octopus) |
  | 0-10p           | ~8%             | "Often under 10p on windy/sunny days" - roughly 4 hours/day on good days                                                                 |
  | 10-15p          | ~12%            | Off-peak night rates typically fall here                                                                                                 |
  | 15-20p          | ~25%            | Around average off-peak (19.4p)                                                                                                          |
  | 20-25p          | ~28%            | Clustered around mean (21.9p)                                                                                                            |
  | 25-35p          | ~18%            | Moderate peak periods                                                                                                                    |
  | 35-50p          | ~6%             | High peak (avg peak 39.3p)                                                                                                               |
  | > 50p           | ~1.4%           | ~11 days/year with 50p+ spikes (https://www.capture.energy/blog/octopus-agile-prices-explained-how-the-tariff-works)                     |

  Arbitrage Opportunity Window

  For a 10kWh battery doing 1 cycle/day:
  - Buy window: 4 cheapest half-hours (~2 hours) at avg ~12p/kWh
  - Sell window: 4 most expensive half-hours at avg ~38p/kWh
  - Flat rate charged to customer: 24.5p/kWh

  Daily Profit Probability Distribution (per 10kWh battery)

  | Percentile        | Daily Spread (p/kWh) | Daily Gross Profit | Reasoning                               |
  |-------------------|----------------------|--------------------|-----------------------------------------|
  | P10 (bad day)     | 12p                  | £1.08              | Low wind, low demand, compressed spread |
  | P25               | 18p                  | £1.62              | Below-average arbitrage day             |
  | P50 (median)      | 24p                  | £2.16              | Typical day: buy at ~12p, sell at ~36p  |
  | P75               | 32p                  | £2.88              | Good spread day                         |
  | P90 (good day)    | 45p                  | £4.05              | High volatility, negative/spike pricing |
  | P99 (exceptional) | 70p+                 | £6.30+             | Plunge + spike same day                 |

  Expected value (mean): ~£2.40/day per 10kWh battery

  Assumptions: 90% round-trip efficiency applied, 1 cycle/day

  ---
  Scale Economics: 100 to 100,000 Units

  Hardware Costs at Scale

  | Units      | Battery Cost/kWh | 10kWh Battery Cost | Source                                                                                                                                      |
  |------------|------------------|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
  | 1 (retail) | £480             | £4,800             | https://www.sunsave.energy/solar-panels-advice/batteries/costs                                                                              |
  | 100        | £380             | £3,800             | ~20% volume discount via wholesale (https://decogroup.co.uk/collections/solar-panel-batteries)                                              |
  | 1,000      | £300             | £3,000             | Commercial scale pricing (https://www.gsl-energy.com/the-real-cost-of-commercial-battery-energy-storage-in-2025-what-you-need-to-know.html) |
  | 10,000     | £220             | £2,200             | Large containerised pricing (~£180-240/kWh)                                                                                                 |
  | 100,000    | £150-180         | £1,500-1,800       | Near utility-scale ($125/kWh ≈ £100/kWh for equipment + £50-80 for distributed install)                                                     |

  Installation Costs at Scale

  | Units   | Install Cost/Unit | Reasoning                                                                                                                   |
  |---------|-------------------|-----------------------------------------------------------------------------------------------------------------------------|
  | 1       | £1,200            | Retail installer, one-off job                                                                                               |
  | 100     | £900              | Bulk contract, repeat work discount (~25%)                                                                                  |
  | 1,000   | £600              | Dedicated crews, standardised process                                                                                       |
  | 10,000  | £400              | In-house teams, scheduling efficiency                                                                                       |
  | 100,000 | £250-300          | VPP-style mass deployment, "plug and play" systems (https://ember-energy.org/latest-insights/how-cheap-is-battery-storage/) |

  Total Capex per Unit

  | Scale   | Hardware | Install | Total/Unit | Total Fleet Cost |
  |---------|----------|---------|------------|------------------|
  | 100     | £3,800   | £900    | £4,700     | £470,000         |
  | 1,000   | £3,000   | £600    | £3,600     | £3.6M            |
  | 10,000  | £2,200   | £400    | £2,600     | £26M             |
  | 100,000 | £1,650   | £275    | £1,925     | £192.5M          |

  ---
  Fleet Revenue & Payback

  Annual Revenue per Unit (10kWh)

  | Percentile     | Daily Profit | Annual Profit |
  |----------------|--------------|---------------|
  | P25            | £1.62        | £591          |
  | P50 (Expected) | £2.40        | £876          |
  | P75            | £2.88        | £1,051        |

  Fleet Economics Summary

  | Scale   | Capex/Unit | Annual Revenue/Unit | Simple Payback | Fleet Annual Revenue |
  |---------|------------|---------------------|----------------|----------------------|
  | 100     | £4,700     | £876                | 5.4 years      | £87,600              |
  | 1,000   | £3,600     | £876                | 4.1 years      | £876,000             |
  | 10,000  | £2,600     | £876                | 3.0 years      | £8.76M               |
  | 100,000 | £1,925     | £876                | 2.2 years      | £87.6M               |

  ---
  Operational Costs (Annual, % of Revenue)

  | Cost Item            | 100 units | 1,000 units | 10,000 units | 100,000 units |
  |----------------------|-----------|-------------|--------------|---------------|
  | Platform/software    | 15%       | 8%          | 4%           | 2%            |
  | Customer support     | 10%       | 6%          | 4%           | 3%            |
  | Maintenance/warranty | 5%        | 5%          | 5%           | 5%            |
  | Total OpEx           | 30%       | 19%         | 13%          | 10%           |

  Net Annual Profit

  | Scale   | Gross Revenue | OpEx     | Net Profit | Net Margin |
  |---------|---------------|----------|------------|------------|
  | 100     | £87,600       | £26,280  | £61,320    | 70%        |
  | 1,000   | £876,000      | £166,440 | £709,560   | 81%        |
  | 10,000  | £8.76M        | £1.14M   | £7.62M     | 87%        |
  | 100,000 | £87.6M        | £8.76M   | £78.84M    | 90%        |

  ---
  Key Sources

  - https://www.ofgem.gov.uk/information-consumers/energy-advice-households/energy-price-cap-explained
  - https://energy-stats.uk/octopus-agile-tariff-pricing/
  - https://www.gsl-energy.com/the-real-cost-of-commercial-battery-energy-storage-in-2025-what-you-need-to-know.html
  - https://ember-energy.org/latest-insights/how-cheap-is-battery-storage/
  - https://www.sunsave.energy/solar-panels-advice/batteries/costs
  - https://decogroup.co.uk/collections/solar-panel-batteries
  - https://www.logic4training.co.uk/insights/electrician-day-rates-uk/
  - https://mobilityforesights.com/product/uk-virtual-power-plant-market

  ---
  Summary

  - Expected daily profit: £2.40/unit (P50), range £1.08 (P10) to £4.05 (P90)
  - Payback improves dramatically at scale: 5.4 years (100 units) → 2.2 years (100,000 units)
  - At 100,000 units: £78.84M net annual profit on £192.5M capex (41% annual return)




## Prices checked by Adam (if they havent been checked they cannot be relied on)

single unit: 9.6kWH £2.5k + vat https://decogroup.co.uk/products/swatten-9-6kwh-battery
 Excludes inverter and install

an even cheaper single unit : 9.6kWH £2.0k + vat  https://www.itstechnologies.shop/products/givenergy-9-5-kwh-li-ion-battery-gen-3
  Excludes inverter and install

single unit less per kWH: 5.1kWH £650 + vat https://www.tradesparky.com/solarsparky/batteries/dyness/dyness-dl50c-512kwh-lithium-iron-phosphate-battery
  Excludes inverter and install
  Can stack 2 of these in parallel (up to 50 in parallel if you need)
To ask of these:
- inverter needs
- install needs
- other equipment needed
- does it count as G98 and not G99? The size of the inverter determines this
- can I get good deals if go wholesale? May have to talk to suppliers as LLMs seem unable to find wholesale discounters online




## Ideas for cheaper batteries

What is a battery actually? What is the difference between buying one giant battery and lots of small ones?

a battery is a collection of cells which hold electricity. Put into small or large boxes. And can plug into a grid.

the expensive part of the battery are the bits which hold electricity. So in theory making lots of small ones should cost little more than one big one, if the net storage capacity is the same in either case.






## Containerised street-level storage
alternative business model... problem a nightmare of planning permission for UK. But easier to find giant batteries for it at low cost.

not hyped to explore further.



 ## Ideas for faster and cheaper battery installs

- Plug-and-play systems (Anker SOLIX style) where customer self-installs

- Standardised rapid-install protocols compressing electrician time to <2 hours

- Social housing bulk contracts where you install 50+ units in one building visit



## Thoughts on vertical integration
if going for scale of operation, which being an electricity provider would involve, there is more alignment with integrating battery making into the operation, to get those margins which pay off more at scale. Includes installation ease and speed (eg standardisation means we can have our own installation engineers who do this very fast and very well)




