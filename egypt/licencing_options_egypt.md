

Egypt PSP License Categories

  The Central Bank of Egypt categorizes payment service providers. Here's the framework:

  CBE Payment License Categories
  ┌────────────┬───────────────────────────────────────────────────────────────────────────┬─────────────────────┐
  │  Category  │                           Activities Permitted                            │ Capital Requirement │
  ├────────────┼───────────────────────────────────────────────────────────────────────────┼─────────────────────┤
  │ Category A │ Full PSP: e-wallets, payment acceptance, money transfer, bill payment     │ EGP 50M (~$1M)      │
  ├────────────┼───────────────────────────────────────────────────────────────────────────┼─────────────────────┤
  │ Category B │ Limited PSP: payment facilitation, aggregation, specific payment services │ EGP 25M (~$500k)    │
  ├────────────┼───────────────────────────────────────────────────────────────────────────┼─────────────────────┤
  │ Category C │ Payment technology provider (no funds handling)                           │ EGP 5M (~$100k)     │
  └────────────┴───────────────────────────────────────────────────────────────────────────┴─────────────────────┘
  Category B Specifically

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
