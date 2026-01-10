# UK Regulatory Analysis: Residential Battery Arbitrage Business Model

## Business Model Summary
A company charges residential customers a flat rate (at avg kWh price), installs batteries at their properties, buys electricity when grid prices are below average, sells/uses when above, and profits from the spread.

---

## DUAL REVENUE STREAMS: CONFIRMED VIABLE

**Yes, you can operate BOTH revenue streams simultaneously:**

| Revenue Stream | Mechanism | Regulatory Route |
|----------------|-----------|------------------|
| **Supply to consumers** | Charge flat rate, buy low on wholesale | Requires Ofgem **Supply Licence** |
| **Sell flexibility to grid** | Export/curtail via Balancing Mechanism, DFS, etc. | Requires **Virtual Lead Party (VLP)** registration with Elexon |

These are **complementary, not mutually exclusive**. Many existing suppliers (Octopus, OVO) combine both. The VLP registration allows you to aggregate customer batteries and trade their flexibility in wholesale/balancing markets while simultaneously being their retail supplier.

**Sources:**
- [Elexon - Becoming a Virtual Lead Party](https://www.elexon.co.uk/bsc/market-entry/becoming-virtual-lead-party/)
- [Ofgem P483 Decision](https://www.ofgem.gov.uk/publications/p483-balancing-and-settlement-code-bsc-changes)

---

## REGULATORY TIMELINE & COST SUMMARY

### Total Setup Costs (Estimate)

| Item | One-off Cost | Ongoing Cost | Timeline |
|------|-------------|--------------|----------|
| Ofgem Supply Licence | £350-£1,050 | Licence fees (volume-based) | **9-18 months** |
| Industry Code Accession (BSC) | £500 | £125/month + volume charges | 3-6 months |
| Industry Code Accession (SEC) | £541 | Volume-based | 1-2 months |
| Industry Code Accession (DCUSA, REC, etc.) | ~£1,000-2,000 | ~£30/customer/year combined | 2-4 months |
| VLP Qualification & Testing | ~£2,000-5,000 | £125/month | 3-6 months |
| **TOTAL REGULATORY SETUP** | **~£5,000-10,000** | **Variable** | **12-24 months** |

### Per-Installation Costs

| Item | Cost | Timeline |
|------|------|----------|
| G98 notification (≤3.68kW) | Free (installer admin ~£50) | Post-install, 28 days |
| G99 application (>3.68kW) | £300-750 | **4-6 months currently** |
| G100 (if export-limited) | Additional £300-700 | +2-4 weeks |
| PAS 63100 compliance uplift | +10-20% on install cost | N/A |

---

## DETAILED REGULATORY REQUIREMENTS

### 1. Ofgem Electricity Supply Licence - **CRITICAL**

**This is the gating requirement. Without it, MRP rules block your core profit mechanism.**

| Aspect | Detail |
|--------|--------|
| **Application Fee** | £350-£1,050 |
| **Timeline** | **Up to 9 months** (extended from 75 working days due to market conditions) |
| **Industry Code Qualification** | Can take **up to 12 months additional** - start BEFORE licence application |
| **Capital Requirements** | Not publicly specified; assessed case-by-case under Condition 4B (Financial Responsibility) |
| **Ongoing Compliance** | Conditions 4A-4D, price cap rules, customer protection obligations |

**Key Licence Conditions:**
- **4A**: Operational capability
- **4B**: Financial responsibility principle (capital adequacy)
- **4C**: Ongoing fit and proper requirement
- **4D**: Protecting Domestic Customer Credit Balances
- **19A**: Financial information reporting

**Process:**
1. Engage with code administrators (MRASCo, Elexon, SECAS) **before** applying
2. Submit application to Ofgem
3. Ofgem assessment (up to 9 months)
4. Complete industry code qualification (can run in parallel)
5. Licence granted

**Sources:**
- [Ofgem - Supply Licence Timeline Decision](https://www.ofgem.gov.uk/decision/supply-licence-applications-reasons-decision-amend-time-period-assessment-and-remove-tacit-authorisation)
- [Ofgem - Licence Application Guidance](https://www.ofgem.gov.uk/decision/updating-licence-application-guidance-decision)
- [GOV.UK - Apply for Licence](https://www.gov.uk/find-licences/gas-electricity-supply-licence)

---

### 2. Virtual Lead Party (VLP) Registration - **FOR GRID TRADING**

**Required to aggregate customer batteries and trade flexibility in Balancing Mechanism.**

| Aspect | Detail |
|--------|--------|
| **Accession Fee** | £500 |
| **Monthly Charge** | £125 (+VAT) |
| **Testing (PTS)** | £999 (+VAT) per half-day slot |
| **Timeline** | **3-6 months** |
| **Qualification** | Self-assessment process audited by KPMG |

**Process:**
1. Submit Expression of Interest to Elexon (market.entry@elexon.co.uk)
2. Complete BSC Accession (£500)
3. Party Registration (BSCP65/01 form)
4. Register Secondary BMUs (BSCP15/4.14 form)
5. Obtain MSID pairs for each SBMU
6. Complete CVA and SVA qualification
7. Pass KPMG audit and PAB approval

**Sources:**
- [Elexon - Becoming a VLP](https://www.elexon.co.uk/bsc/market-entry/becoming-virtual-lead-party/)
- [Elexon - VLP Guidance Note](https://bscdocs.elexon.co.uk/guidance-notes/virtual-lead-party/v-3-0/id-62e244fcd3ac240007b673a0)

---

### 3. Smart Energy Code (SEC) Signatory - **FOR SMART METER DATA**

| Aspect | Detail |
|--------|--------|
| **Application Fee** | £540 |
| **Share Purchase** | £1 (mandatory for energy licensees) |
| **Timeline** | Next SECCo Board meeting after application (~1 month) |
| **Requirement** | Submit Accession Agreement + Party Contact Details Form |

**Process:**
1. Pay £541 via bank transfer
2. Sign Accession Agreement (do not date)
3. Submit to SECAS (at least 1 week before next Board meeting)
4. Receive countersigned agreement + Party ID

**Sources:**
- [Smart Energy Code - Becoming a SEC Party](https://smartenergycodecompany.co.uk/becoming-a-sec-party/)

---

### 4. DNO Grid Connection (G98/G99)

| Standard | Threshold | Cost | Timeline |
|----------|-----------|------|----------|
| **G98** | ≤3.68kW (single-phase) / ≤11.04kW (three-phase) | Free (installer admin ~£50) | Notify within 28 days post-install |
| **G99** | >3.68kW or any battery with export | £300-750 | **Official: 8-12 weeks; Current reality: 4-6 months** |
| **G100** | If export limitation required (~10% of cases) | Additional £300-700 | +2-4 weeks |

**At Scale Considerations:**
- DNOs process applications individually - 1,000+ applications = significant bottleneck
- Some DNO regions have grid constraints → possible curtailment or reinforcement charges
- Scottish Power typically most expensive (£700+)
- Consider G98-compliant battery sizing (≤3.68kW) to avoid G99 delays

**Grid Reinforcement Risk:**
In rare cases, DNO may require grid reinforcement before approval. Costs can be "hundreds or even thousands of pounds" - but rarely requested.

**Sources:**
- [Sunsave - G99 Expert Guide](https://www.sunsave.energy/solar-panels-advice/planning-permission/g99-application)
- [Capture Energy - G98/G99 Guide](https://www.capture.energy/blog/g98-and-g99-applications-for-solar-and-battery-storage)
- [Blue Ape - G99 Application Guide](https://www.blueaperenewables.co.uk/g99-application/)

---

### 5. PAS 63100:2024 - Battery Fire Safety

**Mandatory since 31 March 2024 for all new domestic installations.**

| Aspect | Requirement |
|--------|-------------|
| **Preferred Location** | Outbuildings, external, detached/fire-rated garages |
| **Prohibited Locations** | Voids, roof spaces, lofts, unprotected escape routes |
| **Indoor Requirement** | REI 30 fire-rated separation from habitable rooms |
| **Max per compartment** | 20kWh |
| **Max per dwelling** | 40kWh (standard) / 80kWh (external/fire-rated) |
| **Second-life batteries** | NOT PERMITTED |
| **Cost Impact** | +10-20% on installation cost for indoor compliance |

**Note:** PAS 63100 is a "specification" not a legal requirement per se, BUT:
- Insurers may require compliance
- MCS installers expected to follow it
- Local authorities may adopt it

**Sources:**
- [BSI - PAS 63100:2024](https://knowledge.bsigroup.com/products/electrical-installations-protection-against-fire-of-battery-energy-storage-systems-for-use-in-dwellings-specification)
- [Atlantic Renewables - BESS Standards 2024](https://www.atlanticrenewables.co.uk/contact-us/news-blog/understanding-the-new-british-standards-for-battery-energy-storage-systems-2024.html)

---

### 6. Industry Code Accession Summary

| Code | Purpose | Joining Cost | Ongoing Cost |
|------|---------|--------------|--------------|
| **BSC** (Balancing & Settlement) | Wholesale trading, VLP participation | £500 | £125/month + volume-based |
| **SEC** (Smart Energy Code) | Smart meter data access | £541 | Volume-based |
| **DCUSA** (Distribution) | Use of distribution network | ~£500 | ~£0.04/customer/year |
| **REC** (Retail Energy Code) | Retail market operations | ~£500 | ~£1.80/customer/year |

**Total Industry Code Costs:**
- One-off: ~£2,000-3,000
- Ongoing: ~£30/customer/year (all codes combined)
- **Timeline to full accession: 6-12 months** (can run parallel to licence application)

**Sources:**
- [Ofgem - Energy Codes](https://www.ofgem.gov.uk/energy-regulation/how-we-regulate/energy-codes)
- [Ofgem - Industry Charges Appendix](https://www.ofgem.gov.uk/sites/default/files/2024-12/Appendix_4_Industry_charges.pdf)

---

## CRITICAL REGULATORY BARRIERS (Detailed)

### 1. Maximum Resale Price (MRP) Rules - **SEVERITY: CRITICAL**

**This is the most significant barrier to the business model as described.**

Under the Electricity Act 1989 and Ofgem's MRP Direction:
- When electricity is resold for domestic use, you **cannot charge more than you paid**
- This applies to any "accommodation" including residential properties
- The reseller can only recover: unit rates, standing charges, and metering fees paid to their supplier

**Impact on your model:**
- You CANNOT charge a "flat rate" that would sometimes be higher than your wholesale cost
- The arbitrage profit mechanism (buy low, charge average) is **illegal under MRP rules** without a full supply licence

**Sources:**
- [Ofgem MRP Direction (2014)](https://www.ofgem.gov.uk/sites/default/files/docs/2014/03/mrp_direction.pdf)
- [Ofgem Reselling Gas and Electricity Call for Input (Oct 2025)](https://www.ofgem.gov.uk/call-for-input/reselling-gas-and-electricity-maximum-resale-price-direction)

**Workaround:** Obtain a full electricity supply licence

---

### 2. Energy Act 2023 - Storage Classification - **SEVERITY: MEDIUM**

The Energy Act 2023 (effective 26 Dec 2023) now explicitly classifies electricity storage as generation:
- Storage operators require a **generation licence** (or exemption)
- Class A exemption applies for generation under 10MW (or 50MW declared net capacity)
- At residential scale (5-20kWh per unit), this is NOT a barrier - exemption applies

**However:** This does NOT exempt you from supply licence requirements.

**Sources:**
- [Norton Rose Fulbright - Energy Act 2023 Storage](https://www.nortonrosefulbright.com/en/knowledge/publications/bc3890ae/uk-energy-act-2023-electricity-storage)
- [Energy Act 2023 Part 7](https://www.legislation.gov.uk/ukpga/2023/52/part/7/crossheading/electricity-storage)

---

## HELPFUL POLICIES & SCHEMES

### 1. Flexibility Market Asset Registration (FMAR) - **BENEFIT: HIGH**
- Single registration point for all flexibility markets (local + national)
- Implementation expected 2025-26
- Significantly reduces administrative burden

**Source:** [Ofgem FMAR Decision](https://www.ofgem.gov.uk/sites/default/files/2025-03/Flexibility-Market-Asset-Registration-Decision.pdf)

### 2. Demand Flexibility Service (DFS) - Now Year-Round - **BENEFIT: HIGH**
- Became year-round balancing tool November 2024 (not just winter emergency)
- Derogation approved until March 2027
- Additional revenue stream: estimated £50-200/year per battery

**Source:** [Ofgem DFS Decision](https://www.ofgem.gov.uk/decision/proposed-amendments-balancing-terms-and-conditions-related-third-iteration-demand-flexibility-service)

### 3. Market-wide Half-Hourly Settlement (MHHS) - **BENEFIT: HIGH (2026-2030)**
- Full implementation expected by 2030
- Enables true time-of-use pricing
- Creates price signals essential for battery arbitrage

**Source:** [CMS UK Clean Flexibility Roadmap](https://cms-lawnow.com/en/ealerts/2025/08/uk-clean-flexibility-roadmap-powering-up-britain-s-clean-energy-flex-appeal)

### 4. BSC P483 (August 2025) - **BENEFIT: HIGH**
- Removes half-hourly settlement barrier for aggregators
- Consumers can access flexibility revenues before MHHS rollout
- Critical enabler for VPP models

### 5. Clean Power 2030 Target - **BENEFIT: HIGH (policy tailwind)**
- Government targets 23-27 GW battery storage by 2030 (up from 4.5 GW in 2024)
- Strong political support for storage deployment
- Likely continued favourable policy development

**Source:** [House of Commons BESS Briefing](https://commonslibrary.parliament.uk/research-briefings/cbp-7621/)

---

## COMPLETE TIMELINE: LAUNCH TO OPERATION

```
Month 0-1:   Begin industry code engagement (Elexon, SECAS, RECCo)
Month 1:     Submit SEC accession (£541) → approved within weeks
Month 1-3:   Begin BSC/VLP qualification process (£500 + testing)
Month 2:     Submit Ofgem supply licence application (£350-£1,050)
Month 3-6:   Complete VLP qualification (KPMG audit)
Month 6-9:   Continue Ofgem assessment; complete remaining code accessions
Month 9-12:  Ofgem licence decision (may extend to 12+ months)
Month 12+:   BEGIN CUSTOMER OPERATIONS

PARALLEL TRACK (can start earlier):
- Battery sourcing & installer partnerships
- Customer acquisition pipeline
- Platform/software development
- DNO relationship building
```

**Total time to full operation: 12-18 months**

---

## REGULATORY SUMMARY TABLE

| Regulation | Severity | Cost | Timeline | Workaround? |
|------------|----------|------|----------|-------------|
| MRP (Maximum Resale Price) | **CRITICAL** | N/A | N/A | Get supply licence |
| Supply Licence | **CRITICAL** | £350-£1,050 | 9-18 months | White-label partnership |
| Industry Codes (all) | HIGH | ~£3,000 | 6-12 months | Required |
| VLP Registration | MEDIUM | £500 + £125/mo | 3-6 months | Required for grid trading |
| DNO G99 at scale | HIGH | £300-750 each | 4-6 months each | Use ≤3.68kW batteries (G98) |
| PAS 63100:2024 | MEDIUM-HIGH | +10-20% install | N/A | Compliant installations |
| SEC Signatory | MEDIUM | £541 | 1 month | Required for smart data |
| TPI regulation (future) | MEDIUM | TBD | TBD | Monitor |

---

## BOTTOM LINE

**The business model IS legally viable, but ONLY if you:**

1. **Obtain a full Ofgem electricity supply licence** (or white-label with licensed supplier)
   - Without this, MRP rules prevent charging a flat rate above your cost
   - Timeline: 9-18 months; Cost: £350-£1,050 + code accession

2. **Register as a Virtual Lead Party** to trade grid flexibility
   - Timeline: 3-6 months; Cost: £500 + £125/month

3. **Comply with PAS 63100:2024** for all installations
   - Adds 10-20% to installation cost

4. **Manage DNO relationships** - G99 at scale requires dedicated resourcing
   - Consider ≤3.68kW batteries to qualify for faster G98 route

5. **Become SEC signatory** for smart meter data access
   - Timeline: 1 month; Cost: £541

**Total regulatory setup: £5,000-10,000 over 12-18 months**

The regulatory environment is increasingly supportive of flexibility/storage, with recent improvements (P483, FMAR, DFS year-round) actively enabling this type of business model.

---

*Last verified: January 2026*
