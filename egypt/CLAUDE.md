

### If you are doing research (not coding)
However many asks of you will be research for start up problem spaces, pain points or products.

Ways of working to follow:
- store reports in .md files
- the reader of your reports is time pressed. Do not include any info which is not key.
- For all docs made, keep and update an index in CLAUDE.md so that you know where to find information as the research continues. The index should include any form of summary which will help you know which files to read later on
- do not duplicate infromation by creating new .md files. Good to have a library of .md files, however if a file already exists for a topic, rather than making another file, amalgamate them while preserving (and not duplicating) the content of both files
- reports should make clear you wrote them and the date, at the top
- reports should bear in mind project aims. Many reports will aim to assess specific cruxes
- claims should include links to back them up. 
- double check all your working: you should be highly confident in the responses you give. If you cant get certainty, you should be confident in your calibration (ie being able to state the correct level of confidence in such claims, even if that level is low)
- where something is achievable, and the time or cost for this process to happen is more than £0 or a day, please give the wait time and financial costs involved. This goes for any other information which could influence the business model.
- assume any images you make will be used for VC-meetings to raise capital. Bear that in mind in the style

The user will not accept your claims at face value, but follow the links, so they can build a deep understanding of the market, system, any technicals involves, cruxes and key information. Your role is to help them obtain this profound understanding in minimal time. The above ways of working are to assist with this, however you should use your own judgement re other ways to achieve this goal.


## Project info

A payment transfer service for Egyptian customers, particularly those overseas in USA and such nations, sending money home. Many such customers lack the ability to do so now.

USP of this version:
- transfer instantly or within 24hrs
- easier for customers to see where the money is in the system if the transfer isn't instant
- don't charge for transfers initially
- easier for population, eg freelancers
- compliant with Sharia law (think taking a commission is against sharia)


traditional banking transfer:
Your App → Payment Processor API → Originating Bank → SWIFT Network → Correspondent Bank(s) → Egyptian Bank → Recipient

Chatgpt thinks blockchain much lower margins: Blockchain Costs Are Front-Loaded
- Regulatory risk
- Custody/key management
- Audit
- Partner risk management 
- Reputation management



## Document Index

| File | Contents |
|------|----------|
| `payments-platform-architecture.md` | Full technical architecture. **K8s option** ($260/mo) vs **no-K8s option** ($110/mo with Render/Vercel/Neon). Egypt partner integration flow (Paymob, Fawry, Yellow Card). Costs, security, build-vs-buy, 3-4mo MVP timeline |

| `licencing_options_egypt.md` | Egypt PSP License Categories and their costs and what is appropriate for each |

| `architecture_diagrams.md` | How the system could work, infra to use for each element of system, rough costs involved; how data flows  |

---

## Developing and Egyptian regs
 Bank of Egypt: the Regulatory Sandbox offers a live testing environment for FinTech innovators who are developing new business models that are currently hindered by stringent authorization requirements and regulatory uncertainty.
https://www.cbe.org.eg/en/financial-technology/regulatory-sandbox



