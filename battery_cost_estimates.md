# UK Battery Cost Estimates - Detailed Breakdown

## Retail Price Decomposition

The £4,800 typical retail installed price is NOT just hardware. It breaks down as:

| Component                | Cost        | % of Retail | Notes                                      |
|--------------------------|-------------|-------------|--------------------------------------------|
| Battery + Inverter       | £2,160      | 45%         | Hardware only (cells, BMS, inverter, enclosure) |
| Installation Labour      | £960        | 20%         | Electrician time + materials + scaffolding |
| Customer Acquisition     | £385        | 8%          | Marketing, sales calls, site surveys, admin |
| Warranty Reserve         | £290        | 6%          | 10-year warranty provision                 |
| Installer Margin         | £480        | 10%         | Installer profit                           |
| Distributor Margin       | £385        | 8%          | Wholesale markup                           |
| Overheads                | £140        | 3%          | Warehouse, insurance, office staff         |
| **Total Retail**         | **£4,800**  | **100%**    |                                            |

**Key insight**: Hardware is only 45% of retail. Even free batteries would only halve the price.

Sources:
- [Sunsave Battery Costs UK](https://www.sunsave.energy/solar-panels-advice/batteries/costs)
- [Logic4Training Electrician Rates](https://www.logic4training.co.uk/insights/electrician-day-rates-uk/)

---

## Cost Components at Each Scale

### Hardware Costs (Battery + Inverter + BMS ONLY)

| Units      | Cost/kWh | 10kWh System | Source & Reasoning                                                           |
|------------|----------|--------------|------------------------------------------------------------------------------|
| 1 (retail) | £216     | £2,160       | 45% of £4,800 retail installed price                                         |
| 100        | £250     | £2,500       | Trade pricing - Sunsynk + Pylontech kit at [ITS Technologies](https://www.itstechnologies.shop/) |
| 1,000      | £220     | £2,200       | Direct from [GivEnergy](https://givenergy.co.uk/wholesalers/) or [Pylontech UK](mailto:service.uk@pylontech.com.cn) |
| 10,000     | £180     | £1,800       | OEM/white-label via [AceOn](https://www.aceongroup.com/) or [Evlithium](https://www.evlithium.com/) |
| 100,000    | £120-150 | £1,200-1,500 | Factory-direct CATL/BYD/EVE at ~$125/kWh ([Ember](https://ember-energy.org/latest-insights/how-cheap-is-battery-storage/)) |

**Note**: Hardware at 100 units can be HIGHER than the retail hardware component because retail installers cross-subsidise hardware with installation margins. At scale you pay true cost but eliminate middleman margins.

### Installation Costs (Labour + Materials)

| Units   | Cost/Unit | Breakdown                                                                     |
|---------|-----------|-------------------------------------------------------------------------------|
| 1       | £960      | 1 day labour (£350) + materials (£200) + site visit (£150) + admin (£260)     |
| 100     | £800      | Repeat customer discount, batched site visits, standardised materials         |
| 1,000   | £550      | Dedicated 2-person crews doing 2/day, bulk materials purchasing               |
| 10,000  | £350      | In-house teams (40 electricians), fleet vehicles, zero acquisition overhead   |
| 100,000 | £250      | National fleet, "plug and play" pre-configured systems, same-day installs     |

Source: [Logic4Training UK Electrician Day Rates](https://www.logic4training.co.uk/insights/electrician-day-rates-uk/) - avg £335/day

### Soft Costs (Acquisition, Warranty, Margins, Overheads)

| Units   | Cost/Unit | Components                                                                    |
|---------|-----------|-------------------------------------------------------------------------------|
| 1       | £1,680    | Customer acquisition (£385) + warranty (£290) + margins (£865) + overhead (£140) |
| 100     | £400      | Reduced marketing, warranty reserve, minimal margin layer                      |
| 1,000   | £250      | Lower acquisition via B2B, bulk warranty negotiation                          |
| 10,000  | £150      | Near-zero acquisition, self-insured warranty pool                             |
| 100,000 | £75       | Zero acquisition (VPP model), actuarial warranty reserve only                 |

---

## Total Capex Summary

| Scale   | Hardware | Install | Soft Costs | **Total/Unit** | Fleet Cost | vs Retail |
|---------|----------|---------|------------|----------------|------------|-----------|
| 1       | £2,160   | £960    | £1,680     | **£4,800**     | -          | baseline  |
| 100     | £2,500   | £800    | £400       | **£3,700**     | £370k      | -23%      |
| 1,000   | £2,200   | £550    | £250       | **£3,000**     | £3.0M      | -38%      |
| 10,000  | £1,800   | £350    | £150       | **£2,300**     | £23M       | -52%      |
| 100,000 | £1,350   | £250    | £75        | **£1,675**     | £167.5M    | -65%      |

---

## Where the Savings Come From

| Scale     | Hardware Saving | Install Saving | Soft Cost Saving | Total Saving |
|-----------|-----------------|----------------|------------------|--------------|
| 100       | -£340 (worse)   | +£160          | +£1,280          | **£1,100**   |
| 1,000     | -£40 (worse)    | +£410          | +£1,430          | **£1,800**   |
| 10,000    | +£360           | +£610          | +£1,530          | **£2,500**   |
| 100,000   | +£810           | +£710          | +£1,605          | **£3,125**   |

**Key finding**: At 100-1,000 units, savings come primarily from **eliminating soft costs** (margins, acquisition). Hardware savings only kick in meaningfully at 10,000+ units when you access OEM/factory pricing.

---

## Updated Payback Analysis

| Scale   | Capex/Unit | Annual Profit/Unit | Payback  | Note                              |
|---------|------------|--------------------| ---------|-----------------------------------|
| 100     | £3,700     | £613 (net of 30% opex) | **6.0 years** | Revised down from £4,700        |
| 1,000   | £3,000     | £709 (net of 19% opex) | **4.2 years** | Revised down from £3,600        |
| 10,000  | £2,300     | £761 (net of 13% opex) | **3.0 years** | Revised down from £2,600        |
| 100,000 | £1,675     | £788 (net of 10% opex) | **2.1 years** | Revised down from £1,925        |

Annual profit assumes £876 gross per unit (£2.40/day × 365), less OpEx percentage.

---

## Key Sources

### Cost Breakdown
- Sunsave Battery Costs: https://www.sunsave.energy/solar-panels-advice/batteries/costs
- Logic4Training Electrician Rates: https://www.logic4training.co.uk/insights/electrician-day-rates-uk/
- GSL Energy Commercial Costs: https://www.gsl-energy.com/the-real-cost-of-commercial-battery-energy-storage-in-2025-what-you-need-to-know.html

### Scale Pricing
- Ember Battery Storage: https://ember-energy.org/latest-insights/how-cheap-is-battery-storage/
- ITS Technologies Trade: https://www.itstechnologies.shop/
- GivEnergy Wholesalers: https://givenergy.co.uk/wholesalers/
- AceOn OEM: https://www.aceongroup.com/

### Market Data
- MCS Installation Data: https://www.solarpowerportal.co.uk/battery-storage/mcs-bess-and-heat-pumps-drive-record-year-for-small-scale-renewables-in-2024
- APQC Inventory Carrying Costs: https://www.apqc.org/what-we-do/benchmarking/open-standards-benchmarking/measures/inventory-carrying-cost-percentage

---

*Updated: January 2026*
*Corrected to properly separate hardware (45%) from installation (20%) and soft costs (35%)*
