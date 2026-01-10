
To the National Grid (now called NESO - National Energy System Operator), a single home battery is invisible. You must "aggregate" hundreds or thousands of batteries so they look like one large power plant (a VPP).


## Alternative business model: VLP

VLP = Virtual Lead Party

A VLP turns privately owned home batteries into grid infrastructure, pays owners a slice of the value, and keeps the compounding, recurring margin from market access and optimisation.

Because VLP-related regs came into force in 2024, the market for VLPs isnt saturated (as one can see from the lower number of batteries installed in the UK). 




## VLP-related Regs
P344: allow VLPs to participate in BM market.

P415: allows VLPs to participate in wholesale electricity market.

This means you no longer need to be a full electricity company to do arbitrage at a professional level.



## high level takes on VLP vs Elec company

VLP: deepends on customer wanting to invest capital in own battery, incentivises that but customer still has to do it, free cash for customers with battery already; stuck arbitraging wholesale markets. How is it free cash - monetising an otherwise idle asset with minimal downside.
Hidden costs borne by the customer for VLP:
- Some incremental degradation (small but real)
- Opportunity cost (can’t always do perfect self-arb)
- Loss of some autonomy (unless override)
But in practice:
- These costs are small relative to the payment
- Hence high opt-in rates when explained well


elec comapny who gives out batteries for arb profit: need loads of capital up front, captures all the arb themselves in retail market (more £££), can offer customers lower bills - free money for everyone, not just those willing to invest capital in battery

Some downsides of elec company:
- depreciating assets
- technology risk
- warranty risk
- regulatory risk
- bad debt
- policy levies
- hedging risk
- political risk (price caps)

even more from Chatgpt (it's kind of making me want to do it):
- capital-heavy
- politically exposed
- operationally complex
- slow to iterate

upsides of elec company model:
- would accelerate battery roll out faster
- at scale make larger profits

VLPs are easier companies to exit: companies can buy you and plug you into their existing stack.



#### Key cruxes for VLP vs electricity company

It's close enough that interviewing consumers and understanding if they would find the VLP offer, which is capital intensive for them, attractive.






## UK revenue sources:

### arb


### Frequency response: Can get paid by NESO to instantly absorb or discharge power to keep the grid at exactly 50Hz. 

you can't do everything at once with your battery: your trading algo will have to trade off income from arbitrage, frequency response, etc. Because the alternative is always there, wholesale arbitrage (not retail) ends up being the floor for the price of frequency response: prices for frequency response might be higher than this but never lower.

Don't count on this being much. *While a BESS portfolio could typically earn over GBP 110,000 per MW per year from frequency services, this figure dropped to below GBP 30,000 per MW per year in 2023, according to BloombergNEF. In 2024, frequency prices in the UK were already less than half the European average due to an oversupply of battery capacity.* source: https://www.rabobank.com/knowledge/d011469493-backup-power-for-europe-part-2-the-uk-s-bess-leadership-and-evolving-revenue-stacks

however it has increased lately. What causes this?

G99 batteries should be set up for this. Will G98 work for it too?

 (Gemini): the biggest reason companies shifted away from 50Hz balancing. Frequency Response involves thousands of tiny "micro-cycles" (charging and discharging every few seconds). This generates heat and chemical stress. If you do pure Frequency Response, you might kill a battery in 6–8 years. If you do Arbitrage and Balancing, it might last 12–15 years.



### NESO pays you to "turn down" or "turn up" your total fleet's demand to fix real-time supply gaps.



### NESO also pays you as part of 'capacity market'. A "retainer" paid by the government to ensure you are available during winter peak stress events. 

Overview of capacity market: https://www.neso.energy/what-we-do/energy-markets/electricity-market-reform-emr-delivery-body/capacity-market






## Trading off these revenue sources

Balancing grid demand. Eg when grid cant meet demand you can bid £/MWh (eg £200/MWh). If you win bid you discharge said MW for the time window agreed in the bid (Eg 15 mins at £200/MWh would get you £50)
Something in favour of VLP: VLP vs. Elec Co influence: As a VLP, you get "Direct Control" (P344). This means NESO sees your batteries as a single "Virtual Power Plant." If you are just a small Elec Co without VLP status, you can't access this lucrative market directly; you have to sell your flexibility to a 3rd party who takes a 20–30% cut.
Consider: Utilization Factor. You only "win" BM instructions about X% of the time: want to consider what those will be.

Frequency Response (FR). Paid in £/MW/h (price per Megawatt, per hour of availability). 
EG If the clearing price is £10/MW/h and you commit 3.6kW (0.0036MW). $0.0036 \times £10 = \mathbf{£0.036\text{ per hour}}$. Over a year (8,760 hours), if you win every auction: £315.36 gross.
To earn this, you must keep the battery at ~50% charge so you have "room" to either charge or discharge instantly.  You cannot do full-depth arbitrage while doing FR because you must be ready to both charge and discharge instantly.

Capacity Market (CM) vs. Arbitrage: The CM is a "retainer" that pays you to be available. 
Influenced by 'De-rating Factor'. One maps max hours a battery can discharge for (eg 5kW with 10kWH capacity can discharge for 2 hours max) to the de-rating factor (plotted here https://modoenergy.com/research/en/gb-capacity-market-2025-bess-derating-factors-confirmed-target-capacity). Then (derating factor * MWhcapacity * £MW rate) = £amount you get paid to commit to that battery discharging when there's an emergency.
High-price arbitrage days and "Capacity Stress Events" usually happen at the same time (e.g., a cold Tuesday at 5:30 PM).
Naive way to model this is assume zero income from capacity market, tho in fact there may be more to squeeze out of it.

Arbitrage. 
Influencing Parameters: Round-Trip Efficiency (RTE). If your battery is only 80% efficient, you lose 20% of the energy you "bought" before you can sell it. In 2026, premium LFP batteries hit ~90% RTE.





## Considerations in making a model which optimises the 4 revenue sources (from Gemini)

The "50% SoC" Rule: If you model Frequency Response (Dynamic Containment), you must reduce your Arbitrage capacity by 50% for that hour. You cannot sell the same electron twice.

The "Efficiency Tax": Always multiply your "Charge" costs by $1.15$ (to account for the 15% energy loss during the round-trip). If you buy for 5p, your cost-basis is actually 5.75p. IRL I think it might be lower or higher than 15% depending on the specific battery.

Degradation rate: how many cycles you can do before the battery capacity drops below the 70% warranty threshold?

interactions:
- Your "Arbitrageable Capacity" (arb) is reduced by the De-rated volume if you earn via CM
- Arb reduced if you do Dynamic Containment (FR), you must keep the battery at ~50% charge. You can flex the 50% a little to do 'micro arbitrage', but doesnt sound like you'll make much on this if arb is your main one. 
If one has time overnight to do Dynamic Containment for a few horus and then charge battery before hgih prices in the morning (Arbitrage), can the Dynamic Containment be used as extra income for retail then? or cant be so selective with time of day to earn for Dynamic Containment?
- BM vs arb. One bids for BM, and only bid where BM income will exceed arb. so some possible upside. But if you are elec provider, can expect VLPs to bid lower than you as they have a lower arbitrage income to lose, so would expect close to nothing from this stream
Some interactions between the non-arb revenue sources, however for now lazily assuming these are less important.




## Gemini takes on VLP vs elec company: VLP cant capture full value of the arbitrage, so make much less per battery than full electricity provider. So I'd go with that one

Feature,VLP (Aggregator),Full Provider (Utility)
Max Sell Price,~12p (Wholesale Peak),~28p (Retail Price Cap)
Target Buyer,National Grid (NESO),The End Consumer
Saturation Impact,High (Ancillary prices crash first),Low (Retail prices are sticky)
Ease of Entry,High (6 months to set up),Low (18-24 months + £Millions)

#### Considering income streams specifically
Stream,Main Parameter,VLP Advantage,Elec Co Advantage
BM,Grid Volatility,Direct market access,None
Freq. Response,50Hz Stability,Lower admin fees,None
Capacity Market,National Adequacy,Easier aggregation,None
Arbitrage,Gas/Renewable spread,"Zero ""Retail"" overhead",Access to 28p retail rate

#### gemini estimates costs and income between electricity company and VLP, with profit under 10k units higher for VLP, and higher for full company it higher scale
Metric,Option A: VLP (Aggregator),Option B: Licensed Supplier
Core Revenue,Wholesale + BM + CM,Retail Arbitrage (28p rate)
Gross Revenue/Unit,£388,£887
OpEx (Staff/IT),(£40),(£150)
Bad Debt Risk,£0 (Grid pays you),(£129)
Policy Levies,£0,(£236)
Net Profit per Unit,£348,£372
Fleet Profit (10k),£3.48M,£3.72M

there are other benefits of VLP: 
- need far far less capital



## Gemini takes on company types 

Profit much higher for full electricity provider or VLP. Other company options (White label partner or Licence Lite) much lower profit at scale.

Level,"Regulatory ""Badge""",Description,Est. Net Profit (per 10k units)
1. White Label Partner,None (uses partner's license),"You brand the app, but a company like Octopus or E.ON does the billing and grid trading. You take a commission.","£1.2M - £1.8M (Lower risk, lower reward)"
2. Virtual Lead Party (VLP),P344 / P415 Registered,You are NOT a supplier. You don't bill customers. You aggregate batteries and trade them directly on the Wholesale and BM markets.,£3.2M - £3.6M (Pure tech play; no bad debt)
3. Licence Lite,Junior Supply License,"You act as a supplier but outsource the expensive ""grid settlement"" and ""balancing"" to a bigger utility.",£2.5M - £3.0M (Stuck in the middle; high overhead)
4. Full Licensed Supplier,Full Ofgem License,"You are a utility. You bill 28p/kWh. You manage bad debt, smart meters, and customer support.","£3.5M - £4.2M (Highest reward, but huge capital risk)"






## Electricity company costs, which VLP exempt from

These numbers are all  Gemini 3, however I think we could get these down by being a dope modern company, esp operating costs. And would need to check latest figures to be sure.

An energy supplier isn't just a pipe for electricity; it’s a bank and a call centre.

Maybe can have less bad debt by better-than-average customer screening analytics. And reduce operating costs by being a leaner modern company.

Bad Debt (£60–£100/yr): Suppliers must pay the grid and generators regardless of whether the customer pays them. 

Operating Costs (~£230/yr): This covers billing software (like Kraken or Gentrack), 24/7 call centres, and the "Smart Meter Rollout" levy.

Policy Levies (~£230/yr): Social schemes like the "Warm Home Discount" and environmental subsidies.

The Math (per kWh):A typical household uses ~2,700 kWh/year. Supplier Costs: £279 (Operating/Debt) + £44 (Profit/EBIT) = £323 per year.
Per kWh cost: £0.11. Tho OFGEM estimate it's higher, so check later figures.




## Wholesale vs retail market

Wholesale: prices reflect system marginal cost





## UK system actors, from ChatGPT

### Policy & regulation
- **DESNZ**
  - Energy policy
  - Net Zero strategy
- **OFGEM**
  - Economic regulator
  - Market oversight
- **HM Treasury**
  - Public funding
  - Fiscal mechanisms

### System operation & planning
- **NESO (National Energy System Operator)**
  - Real-time system balancing
  - Network planning
  - Future energy scenarios

### Networks (regulated monopolies)
- **Transmission Network Owners (TNOs)**
  - National Grid Electricity Transmission (England & Wales)
  - Scottish Power Transmission
  - Scottish Hydro Electric Transmission
- **Distribution**
  - **DNOs (Distribution Network Operators)**
    - UKPN (UK Power Networks)
    - SSE Networks
    - SP Energy Networks
    - Northern Powergrid
    - Electricity North West
    - National Grid Electricity Distribution
  - **IDNOs / VLPs**
    - Independent and virtual network providers

### Generation & flexibility
- **Generators**
  - Gas
  - Nuclear
  - Wind (onshore / offshore)
  - Solar
  - Hydro & biomass
- **Storage providers**
  - Batteries
  - Pumped hydro
- **Flexibility**
  - Demand Side Response (DSR)
  - Aggregators
  - Virtual Power Plants (VPPs)

### Markets & trading
- **Wholesale market**
  - Power exchanges
  - OTC bilateral trading
- **Balancing Mechanism**
  - Operated by NESO
- **Capacity Market**
- **Ancillary services**
  - Frequency response
  - Reserves
  - Stability / inertia

### Retail & consumers
- **Energy suppliers**
  - Large suppliers
  - Challenger suppliers
- **Consumers**
  - Domestic
  - Small & medium enterprises (SMEs)
  - Industrial & commercial (I&C)
- **Prosumers**
  - Consumer-generators
  - On-site storage

### Data, codes & settlement (cross-cutting)
- **Elexon**
  - Balancing & Settlement Code (BSC)
- **LCCC**
  - Contracts for Difference (CfDs)
- **ESC**
  - Capacity Market settlement
- **Codes & governance**
  - BSC
  - CUSC
  - DCUSA
  - Grid Code
  - SEC
- **Metering & data**
  - DCC
  - Meter Asset Providers (MAPs)
  - Meter Operators (MOPs)






## Why not just buy cheap batteries wholesale and sell them cheap on consumer market

Not sure I have a really good answer to this. 






