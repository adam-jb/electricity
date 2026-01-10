
## Document Index

| File | Contents |
|------|----------|
| `uk-battery-arbitrage-regulations.md` | UK regulatory deep-dive: licence requirements, MRP rules, industry codes, G98/G99, timelines, costs |
| `uk-regulatory-flowchart.md` | VC-ready flowchart: UK approval process by scale (small/medium/VPP) |
| `uk_battery_arbitrage_business_plan.md` | Full UK business plan with revenue model and financials |
| `battery_cost_estimates.md` | Battery unit costs, installation costs, manufacturer comparisons |
| `battery-sizing-tradeoff.md` | Applies to UK only | **3.68kW (G98) vs larger (G99)**: 10-15% less arbitrage but avoids 4-6 month G99 bottleneck. Recommends G98 for scale. |
| `uk_grid_operator_models.md` | Applies to UK only, sets out company options from full electricity company onwards, and VLP route to just provide battery service and not full electricity provider. Also inclues details on all 4 sources of revenue for companies and VLPs, how those revenue sources interact |

| `research/hedge-fund-pain-points.md` | Unrelated research - hedge fund pain points |

---

You may code, however many asks of you will be research for start up problem spaces, pain points or products.

Ways of working to follow:
- store reports in .md files
- the reader of your reports is time pressed. Do not include any info which is not key.
- For all docs made, keep and update an index in CLAUDE.md so that you know where to find information as the research continues. The index should include any form of summary which will help you know which files to read later on
- do not duplicate infromation by creating new .md files. Good to have a library of .md files, however if a file already exists for a topic, rather than making another file, amalgamate them while preserving (and not duplicating) the content of both files
- reports should make clear you wrote them and the date, at the top
- reports should bear in mind project aims. Many reports will aim to assess specific cruxes
- claims should include links to back them up. 
- double check all your working: you should be highly confident in the responses you give. If you cant get certainty, you should be confident in your calibration (ie being able to state the correct level of confidence in such claims, even if that level is low)
- where something is achievable, eg battery installation, or getting approved for a licence, and the time or cost for this process to happen is more than £0 or a day, please give the wait time and financial costs involved. This goes for any other information which could influence the business model.
- assume any images you make will be used for VC-meetings to raise capital. Bear that in mind in the style

The user will not accept your claims at face value, but follow the links, so they can build a deep understanding of the market, system, any technicals involves, cruxes and key information. Your role is to help them obtain this profound understanding in minimal time. The above ways of working are to assist with this, however you should use your own judgement re other ways to achieve this goal.



### PRoject overview

overview:
- batteries are cheap
- rationally, mamy people in developed countries should buy them
- they dont though, see we could start an electricity company which gives them batteries, sells at a flat rate to people, and buys and sells from grid to arbitrage costs, and profit from batteries. also get money to balance the grid. 
- the unit costs need to work for this: battery costs low enough to pay for themselves in some fair amount of time




### Links

On the UK electricity market (23 registered suppliers in 2025): https://assets.publishing.service.gov.uk/media/68da73e049e17d00a56ffb60/Competition_in_UK_Electricity_Markets_2024.pdf



### Regulatory challenge in UK

In UK takes 9-18 months for OFGEM to register you as an electricity provider. Looks like their bar has gone up a lot for letting companies in, SO WOULD WANT EXPERT INPUT TO NAVIGATE THAT, OR BE CONFIDENT WE CAN NAVIGATE THAT, BUT MOST LIKELY RECRUIT PARTNERS OR ADVISORS TO HELP NAVIGATE IT.

  Originally was 75 working days (~3.5 months). Extended because:

  1. 29 suppliers collapsed between July 2021 - May 2022, costing consumers £2.7bn
  2. Ofgem was criticized for "failure to effectively regulate" - https://committees.parliament.uk/committee/127/public-accounts-committee/news/174285/pac-ofgem-failures-come-at-considerable-cost-to-energy-billpayers/
  3. They paused licensing entirely in Oct 2021 to build new financial resilience framework
  4. 9 months is now the statutory maximum for Ofgem assessment
  5. +6-12 months for industry code accession (runs partially parallel)

  Process Breakdown

  | Stage                | What happens                                                                            | Time        |
  |----------------------|-----------------------------------------------------------------------------------------|-------------|
  | Duly Made Check      | Application complete?                                                                   | ~2 weeks    |
  | Tier 1 Assessment    | Company details, directors, shareholders, licence history, basic suitability            | ~2-3 months |
  | Tier 2 Assessment    | Official docs, bank/solicitor/auditor details, interview, evidence of code body contact | ~3-4 months |
  | Financial Resilience | Adequate capital? Hedging strategy?                                                     | Throughout  |
  | Decision             | Authority approval                                                                      | ~1-2 months |

  Source: https://www.ofgem.gov.uk/sites/default/files/2025-06/Guidance_on_how_to_apply_for_a_gas_or_electricity_licence.pdf

  Rejection Rate

  Ofgem doesn't publish aggregate stats. What we know:

  - Only publicly documented refusal: Alaska Energy Ltd (June 2022) - https://www.ofgem.gov.uk/publications/alaska-energy-ltd-notice-refusal-application-electricity-supplier-licence
  - But context matters: market went from 70 suppliers (2018) → 23 (2022) after the crisis
  - Post-2022 rules are explicitly designed to be harder to pass
  - No supplier failures since summer 2022 - suggests tighter gatekeeping working

  My estimate: rejection/withdrawal rate likely 30-50% now vs near-zero pre-2019. This is inference based on the policy shift, not published data. Could submit FOI request to Ofgem for actual numbers.

  Key takeaway for VCs

  The 9-18 month wait exists because Ofgem got burned by letting in 50+ undercapitalized suppliers who then collapsed. The bar is now high but passable - you need to demonstrate genuine financial resilience and operational capability.





### meeting notes 9th Jan

Doubts / uncertainties / concerns
Ben: 
How much can be made by arbitrage?
How hard is it to become an energy company? For each country.
Can the business be easily scaled across nations? Related Q is how big is the opportunity?

Riccardo:
Less worried about market size - market is very big. The majority of customers with solar panels have no batteries (90% Netherlands, 70% Germany).
Battery pricing: can it be low enough? Are Base actually losing money right now and the battery costs are more than they are making out, meaning the model wouldn’t work in the EU
Base - are they making as much from being paid to balance the grid as they imply - is it any at all? (When they raised $200m they had 1000 batteries installed)
(Sophia - is this a problem if the claim for this revenue is in the future?)

Will:
If you frame yourself as an energy provider, you’re vulnerable to disruption from other energy providers who have other business models (eg Fuse Energy in the UK)
If we scale up a lot, will arbitrage income per new battery reduce?

Adam:
Unit costs
Is customer acquisition affordable?

Sophia:
Competition: are larger energy companies/players already thinking about this?
Are there hidden reasons people aren’t buying batteries for their homes already, when they are cost efficient already? Eg if reasons are only monetary then there is no upside to this business - want to target customers not thinking about batteries and want a lower energy bill

Sina:
Are batteries definitely the best solution? Might be overlooking something else



Further discussion
Sina: is there a market for smaller batteries, eg having multiple small batteries per home?

Riccardo: larger batteries cost less per kWH. So better overheads with bigger batteries. Though there are forces encouraging smaller batteries too (eg wanting to put a battery in an apartment).

Will: do EVs get used for this?

Riccardo: EV manufacturers don't like cars being used to balance the grid. A few cars allow this but not many.

Sophia: companies are considering using 2nd hand EV companies and repurpose them as home batteries. Could this lead to lower unit costs?

Will: unlike the US where people live in their own homes, but in Spain many more people in apartments. Is it easier if you need to install one big battery in one building, to power all apartments in the building?




Shopping list

The idea being that if we know all these with high confidence, we can decide what to do:


Get figures on total cost of batteries


Fermi estimate income you can make on electricity arbitrage


(this one top of list for Sophia) Understand regulations which block business model, and which countries *don’t* have those blockers. Eg becoming an energy provider. Include times for things to get approved (e.g. can take a long time in Hungary).


How much is paid to energy companies to balance the grid, by nation?


Find out if current energy providers’ are likely to act on this?


Update business model calculator to have correct unit costs, expected income from arbitrage, and anything else needed

Check Fuse Energy UK business model. Does it interact with this idea at all?




Blockers to assess nations for

Becoming an energy provider
Being able to sell back to grid
Installing batteries
???What else???


Things we could look for in a target region/nation

- Regulations allow for buying electricity from generators and selling to consumers (forming a REP)
- volatile electricity prices
- outages or other source of customer pain
- high electricity bills (customer pain; they have more to gain if we can charge less per KWh); and higher demand
- trend of increasing electricity usage - higher amplitude increases arbitrage income
- trend of increasingly volatility (ie more solar and wind generation in the pipeline)
- (this one is weaker imo) documented public favourability of batteries (ie some people have bought them already)

Random gpt search on how hard is it to become an energy provider:


Factor
Italy
Spain
Poland
Hungary
Regulator
ARERA
CNMC
URE
MEKH
License Required
Registration only
Registration + CNMC authorization
Full concession (OEE)
Full license
Capital/Guarantee
Low (market participation guarantees)
Financial guarantees required
Demonstrated financial capacity + potential security deposit
Financial capacity proof






Adam notes from Base articles part 1 and 2

You may want to skip 2nd part which felt more like a hype article/victory lap and much less valuable imo (the author invested in the company just before writing part 2 and I feel incentives might be funny there). Only update I got from it:
- *utilities are willing to pay even more than the free market, because Base can save them from making expensive transmission upgrades*. Base can use all their data to evidence how they can control grid load in real time, and offer to sell that service 

why make their own batteries & install themselves & vertically integrate:
- good unit economics if can vertically integrate battery production and installation (eg make design batteries to be easy to install, as installation expected to be an increasing % of cost, as battery production gets cheaper)
- vertical integration also makes easier to install, so can scale faster (install in 'minutes or seconds, not days or weeks')
- *to bring down costs, shift as much as possible from construction to manufacturing, where it can benefit from learning curves*

reasons to be in Texas:
- 6x more outages than there were a decade ago. Customer pain
- power prices in Texas are particularly volatile (large gap between low and high)
- isolated grid, so more volatile 
- deregulated, so can act as a REP

things I'd look for in a target region/nation:
- regulations allow for buying electricity from generators and selling to consumers (forming a REP)
- volatile electricity prices
- lack of sources of grid stability. eg no interconnectors 
- outages or other source of customer pain
- high electricity bills (customer pain; they have more to gain if we can charge less per KWh); and higher demand
- increasing electricity usage - higher amplitude increases arbitrage income
- trend of increasingly volatility (ie more solar and wind generation in the pipeline)
- (this one is weaker imo) documented public favourability of batteries (ie some people have bought them already)

my takes:
- I wonder what the minimum option would be which would plausibly turn a small amount of profit...
- key update is that the grid is more of a bottleneck than I thought. Specifically: transmission lines need to be sized for peak load. Batteries make it possible to smooth use of the transmission lines, reducing the peak demand. 
- similar update:  *the battery is more valuable to the market than it is to any one homeowner, so the market participant - Base, in this case – should own it.*
- another update was that the cost of transmission is a big chunk of overall electricity price, and its rising
- if you scale enough, might the gap between low and high electricity costs close with each additional battery? (as the discrepancy in supply-demand shrinks in each given moment)
- unit economics seem good (says a battery pays for itself within a few years), and may be about to get better due to Learning Curve (more batteries made = batteries cost less)
- batteries can also help maximize load factor and avoid expensive buildout. How do Base or such a company captures value from this preventative service? By 'Grid ancillary services': things that the grid pays market participants to do in order to stabilize the grid
- I wonder if batteries at the home is optimal. Possible large batteries could live by the regional transformers, which also reduces load on national grid (tho still would have more load for the 'final mile' of transmission of transformer to home)
- other than that there's nothing too mysterious going on? Ie they made the update above, realised there's more value in managing peak demand with batteries, made a very cool business model, then did all the things one expects of A-grade founders (create amazing team, etc). I say this because it has a feeling of 'do-ability'!
- *because the battery is larger than competitors’, **it can act as the single source of power for the home**, and therefore doesn’t require the installation of a separate critical loads panel like the Powerwall does* There are lots of small improvements like this one can do when vertically integrated
- there are risks, such as other companies installing batteries, or electric cars to be used for a similar thing, however the article suggests the EVs of today arent spec'd for this (true in my limited experience)

quotes I liked:
- "formula for start up success: find large fragmented industry with low NPS; vertically integrate a solution to simplify value product". REPs fits this. What else could?




Regulation research Italy:

 -> No permit needed for installations with less than 10 MW power rating. (source )
	-> Seems to be only limit on power rating, not capacity
-> However need to go through DSO to connect to grid (seems to cost around 200-500 eur per installation, not sure if we can bypass this with Riccardo’s idea of just plugging it in but probably not)
-> Up to 50kW installation fairly straight forward, above that less so


-> For full access to capacity market needs at least 1 MW total power rating as VPP
	-> Not clear yet what that means practically speaking
	-> Seems to be an UVAM pilot that is accessible (link)

-> Enel X and Sonnen seem to be doing this in Italy already

-> Seems to be a fairly large adaptation of batteries (especially with residential solar) in Italy, perhaps a pure software/provider play on existing installations to “make the most of it”?

-> There might be tax incentives on Solar, perhaps as a bundle there are some options that make the unit economics look more attractive

-> Given that you can just install up to 10 MW we might consider ordering a decent amount of batteries and install them in a random location to clear the 1 MW hurdle, as we onboard clients we transfer the battery location from our system to the end-user ?


