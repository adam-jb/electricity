

My (Adam's) headline: CBE doesn't publish detailed English documentation on exact Category B limitations, so unclear if we'd - in the long term - want Category A in order to get best margins.


## Egypt PSP License Categories

There are a few available. Better licence means lower cost while doing more of the chain of the transfer ourselves.

  The Central Bank of Egypt categorizes payment service providers. CBE Payment License Categories:
  ┌────────────┬───────────────────────────────────────────────────────────────────────────┬─────────────────────┐
  │  Category  │                           Activities Permitted                            │ Capital Requirement │
  ├────────────┼───────────────────────────────────────────────────────────────────────────┼─────────────────────┤
  │ Category A │ Full PSP: e-wallets, payment acceptance, money transfer, bill payment     │ EGP 50M (~$1M)      │
  ├────────────┼───────────────────────────────────────────────────────────────────────────┼─────────────────────┤
  │ Category B │ Limited PSP: payment facilitation, aggregation, specific payment services │ EGP 25M (~$500k)    │
  ├────────────┼───────────────────────────────────────────────────────────────────────────┼─────────────────────┤
  │ Category C │ Payment technology provider (no funds handling)                           │ EGP 5M (~$100k)     │
  └────────────┴───────────────────────────────────────────────────────────────────────────┴─────────────────────┘

  Category B is the mid-tier license - you can facilitate payments but with restrictions:

  What Category B allows:
  - Payment aggregation (collecting payments on behalf of merchants)
  - Payment facilitation/gateway services
  - Specific remittance services (with additional approvals)
  - Bill payment services

  What Category B does NOT allow (need Category A):
  - Issuing e-wallets that hold customer funds
  - Full money transfer services
  - Acting as a payment institution with stored value



## Category B vs Category A
Based on CBE's framework, here's the key difference for your use case:

  Category A vs Category B for Money Transfer
  ┌──────────────────────────────────────────────────────────────┬────────────┬─────────────────┐
  │                           Activity                           │ Category A │   Category B    │
  ├──────────────────────────────────────────────────────────────┼────────────┼─────────────────┤
  │ Receive funds from abroad and pay out to Egyptian recipients │ Yes        │ Unclear/Limited │
  ├──────────────────────────────────────────────────────────────┼────────────┼─────────────────┤
  │ Hold customer funds (e-wallets)                              │ Yes        │ No              │
  ├──────────────────────────────────────────────────────────────┼────────────┼─────────────────┤
  │ Full remittance license                                      │ Yes        │ No              │
  ├──────────────────────────────────────────────────────────────┼────────────┼─────────────────┤
  │ Payment facilitation/aggregation                             │ Yes        │ Yes             │
  ├──────────────────────────────────────────────────────────────┼────────────┼─────────────────┤
  │ Bill payments                                                │ Yes        │ Yes             │
  ├──────────────────────────────────────────────────────────────┼────────────┼─────────────────┤
  │ Act as intermediary for licensed entity                      │ Yes        │ Yes             │
  └──────────────────────────────────────────────────────────────┴────────────┴─────────────────┘
  The Critical Question

  Can Category B do inbound remittance (US → Egypt)?

  Likely no as the primary operator. Category B is designed for:
  - Payment aggregation (collecting payments for merchants)
  - Payment gateway services
  - Facilitating transactions for Category A licensees

  Inbound remittance (receiving money from abroad, converting, paying out) typically requires:
  - Holding funds temporarily (even briefly)
  - FX conversion authority
  - Direct relationship with recipient

  These are Category A activities.

  Your Options
  ┌─────────────────────────────────────┬──────────────────┬──────────────────────────────────────────────────────────────────────────────────────────┐
  │              Approach               │  License needed  │                                       How it works                                       │
  ├─────────────────────────────────────┼──────────────────┼──────────────────────────────────────────────────────────────────────────────────────────┤
  │ Partner with Category A PSP         │ None             │ Paymob/Fawry handles Egypt side, you send them USDC, they pay out                        │
  ├─────────────────────────────────────┼──────────────────┼──────────────────────────────────────────────────────────────────────────────────────────┤
  │ Get Category B + partner for payout │ Category B       │ You handle some facilitation, but still need Category A partner for actual fund movement │
  ├─────────────────────────────────────┼──────────────────┼──────────────────────────────────────────────────────────────────────────────────────────┤
  │ Get Category A                      │ Category A       │ Full control, but higher capital (EGP 50M vs 25M), longer process                        │
  ├─────────────────────────────────────┼──────────────────┼──────────────────────────────────────────────────────────────────────────────────────────┤
  │ CBE Sandbox                         │ Sandbox approval │ Test the model, CBE may grant specific permissions outside normal categories             │
  └─────────────────────────────────────┴──────────────────┴──────────────────────────────────────────────────────────────────────────────────────────┘
  My Honest Assessment

  Confidence: Medium. CBE doesn't publish detailed English documentation on exact Category B limitations. The categories exist but the precise boundaries for cross-border remittance are not crystal clear from public sources.

  Recommendation:
  1. For MVP: Partner with existing Category A PSP (Fawry, Paymob, Yellow Card)
  2. If pursuing own license: Engage Egyptian fintech lawyer (~$3-5k) to get definitive answer on whether Category B covers your specific flow
  3. Consider sandbox route - CBE may be flexible for innovative models



## Claude opinions
  For Your Use Case
  ┌────────────────────────────────────────────────────┬────────────────────────────────────┐
  │                 If you want to...                  │              You need              │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┤
  │ Partner with existing PSP (Paymob, Fawry)          │ No Egypt license needed            │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┤
  │ Operate your own payout network                    │ Category A or B depending on scope │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┤
  │ Just receive USDC and instruct partners to pay out │ Possibly Category B or sandbox     │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┤
  │ Hold EGP float and issue wallets                   │ Category A                         │
  └────────────────────────────────────────────────────┴────────────────────────────────────┘
  Regulatory Sandbox vs License

  The CBE sandbox lets you test without a full license:
  ┌───────────────────┬──────────────────────────────────────┬──────────────┐
  │      Aspect       │               Sandbox                │ Full License │
  ├───────────────────┼──────────────────────────────────────┼──────────────┤
  │ Time to get       │ 2-4 months                           │ 6-12+ months │
  ├───────────────────┼──────────────────────────────────────┼──────────────┤
  │ User limit        │ Capped (e.g., 1,000-10,000 users)    │ Unlimited    │
  ├───────────────────┼──────────────────────────────────────┼──────────────┤
  │ Transaction limit │ Capped                               │ Unlimited    │
  ├───────────────────┼──────────────────────────────────────┼──────────────┤
  │ Duration          │ 12-24 months (renewable)             │ Permanent    │
  ├───────────────────┼──────────────────────────────────────┼──────────────┤
  │ Path forward      │ Must apply for full license to scale │ N/A          │
  └───────────────────┴──────────────────────────────────────┴──────────────┘
  Recommendation for MVP:
  1. Launch with Egypt PSP partner (no license needed)
  2. Apply to CBE sandbox in parallel
  3. If volume justifies, pursue Category B license
