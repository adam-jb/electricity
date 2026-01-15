# Payments Platform: Compute & Code Infrastructure

**Author:** Claude (AI Research Assistant)
**Date:** 15 January 2026

---

## Table of Contents

- [Flow](#flow)
- [US Side: You Don't Need to Be a Bank](#us-side-you-dont-need-to-be-a-bank)
  - [Transfer Service](#1-transfer-service-core)
  - [Ledger Service](#2-ledger-service)
  - [Compliance Service](#3-compliance-service)
- [Cost Optimisation](#cost-optimisation)
- [Build vs Buy Decision Matrix](#build-vs-buy-decision-matrix)
- [Timeline & Team](#timeline--team)
- [Key Risks & Mitigations](#key-risks--mitigations)
- [Claude's Take on Security](#claude-take-on-security)
- [Info on Services We Might Use](#info-on-services-we-might-use)
  - [Direct NACHA Files](#direct-nacha-files)
  - [FedNow (Instant US Payments)](#fednow-instant-us-payments)
  - [KYC Providers (Persona / Onfido)](#kyc-providers-persona--onfido)
  - [KYC with Plaid Identity](#kyc-with-plaid-identity)
  - [OFAC SDN List](#ofac-sdn-list)
  - [AML Monitoring](#aml-monitoring)
  - [PSP License Egypt](#psp-license-egypt)
  - [InstaPay Egypt](#instapay-egypt)
  - [OTC Crypto / OTC Liquidity](#otc-crypto--otc-liquidity)
  - [AML Monitoring in USA: Legal Requirements](#aml-monitoring-in-usa-legal-requirements)
- [Security Architecture](#security-architecture)
- [Security Checklist for MVP](#security-checklist-for-mvp)
- [Useful Links](#useful-links)


---

## Flow
 STEP    ACTION                          WHO DOES IT         COMPLIANCE CHECK
  ────────────────────────────────────────────────────────────────────────────
  1       User signs up                   Your app            → KYC (Persona/Onfido verifies identity)

  2       User links US bank account      Plaid               (Plaid connects to their bank)

  3       User initiates $500 transfer    Your app            → Sanctions screening (OFAC check on sender + recipient)
                                                              → AML transaction monitoring (is this suspicious?)

  4       Pull $500 from user's bank      Plaid (ACH pull)    → Plaid sends to YOUR US bank account
                                                                 (not Circle directly)

  5       You convert USD → USDC          Circle API          Your system calls Circle to mint USDC
                                                              (money moves: your bank → Circle → USDC in your wallet)

  6       Send USDC to Egypt partner      On-chain tx         USDC leaves your wallet → partner's wallet

  7       Partner converts USDC → EGP     Egypt partner       Partner handles their own compliance

  8       Partner pays recipient          Egypt partner       Bank transfer or mobile money

  Key clarification: Plaid doesn't send money to Circle directly. Plaid pulls money into your US bank account, then you use Circle's API to convert that USD to USDC.

  ---
  Where each compliance check happens:
  ┌──────────────────┬─────────────────────────┬─────────────────────────────────────────────────────────────────────────────────────────┐
  │      Check       │          When           │                                           Why                                           │
  ├──────────────────┼─────────────────────────┼─────────────────────────────────────────────────────────────────────────────────────────┤
  │ KYC              │ User signup (once)      │ Verify identity before allowing any transfers. Legal requirement for money transmission │
  ├──────────────────┼─────────────────────────┼─────────────────────────────────────────────────────────────────────────────────────────┤
  │ Sanctions (OFAC) │ Every transfer (step 3) │ Check sender AND recipient aren't on OFAC/EU/UN sanctions lists. Must block if match    │
  ├──────────────────┼─────────────────────────┼─────────────────────────────────────────────────────────────────────────────────────────┤
  │ AML monitoring   │ Every transfer (step 3) │ Flag suspicious patterns: sudden large amounts, structuring, high-risk corridors        │
  └──────────────────┴─────────────────────────┴─────────────────────────────────────────────────────────────────────────────────────────┘





  ## US Side: You Don't Need to Be a Bank

  You need a Money Transmitter License (MTL), not a bank charter. Different thing:
  ┌──────────────┬───────────────────────────────────┬──────────────┬────────────────────────────────────────┬────────────────────────────────────────────────────────┐
  │    Option    │            What it is             │     Time     │                  Cost                  │                       Trade-off                        │
  ├──────────────┼───────────────────────────────────┼──────────────┼────────────────────────────────────────┼────────────────────────────────────────────────────────┤
  │ Own MTL      │ License in each state you operate │ 12-24 months │ $500k-1M+ legal/compliance             │ Full control, but nightmare (50 states, ongoing exams) │
  ├──────────────┼───────────────────────────────────┼──────────────┼────────────────────────────────────────┼────────────────────────────────────────────────────────┤
  │ BaaS partner │ Operate under their MTL           │ 2-4 weeks    │ $0 setup, higher per-tx fees (~0.5-1%) │ Fast launch, they handle compliance                    │
  ├──────────────┼───────────────────────────────────┼──────────────┼────────────────────────────────────────┼────────────────────────────────────────────────────────┤
  │ Sponsor bank │ Bank sponsors your program        │ 2-6 months   │ Varies                                 │ Middle ground                                          │
  └──────────────┴───────────────────────────────────┴──────────────┴────────────────────────────────────────┴────────────────────────────────────────────────────────┘
  Recommendation: Use a BaaS partner (Unit, Bridge, Stripe Treasury). You avoid the MTL entirely - they're the licensed entity, you're their customer.

  Relevant providers:
  - Bridge (bridge.xyz) - Built for stablecoin payouts, has MTL
  - Unit (unit.co) - Full BaaS, can hold customer funds
  - Zero Hash (zerohash.com) - Crypto-native, MTL in all states





## Cost optimisation: made fully possible by becoming Category B in Egypt

  ---
  Cost Minimums: Component by Component

  1. US Money Intake (ACH Pull)
  ┌──────────────────────────┬────────────┬────────────┬──────────────────────────────────────────────────────────────┐
  │          Method          │  Cost/tx   │ Complexity │                       What's required                        │
  ├──────────────────────────┼────────────┼────────────┼──────────────────────────────────────────────────────────────┤
  │ Plaid + BaaS             │ $0.30-0.50 │ Low        │ Just API integration                                         │
  ├──────────────────────────┼────────────┼────────────┼──────────────────────────────────────────────────────────────┤
  │ Direct ACH (Dwolla/Moov) │ $0.10-0.20 │ Medium     │ Own bank account, ACH origination agreement                  │
  ├──────────────────────────┼────────────┼────────────┼──────────────────────────────────────────────────────────────┤
  │ Direct NACHA files       │ $0.01-0.03 │ High       │ MTL + sponsor bank relationship, build NACHA file generation │
  ├──────────────────────────┼────────────┼────────────┼──────────────────────────────────────────────────────────────┤
  │ FedNow (instant)         │ $0.01-0.05 │ High       │ Bank partnership, newer rails                                │
  └──────────────────────────┴────────────┴────────────┴──────────────────────────────────────────────────────────────┘
  Floor: ~$0.02/tx with own MTL + direct bank integration + NACHA files

  What it takes: Own MTL (12-24mo, $500k+), bank sponsor relationship, build ACH file generation/reconciliation

  ---
  2. USD → USDC Conversion
  ┌──────────────────────────┬────────────────────────┬────────────────────────────────────────┐
  │          Method          │        Cost/tx         │            What's required             │
  ├──────────────────────────┼────────────────────────┼────────────────────────────────────────┤
  │ Circle mint via API      │ $0                     │ Wire USD to Circle, they mint USDC 1:1 │
  ├──────────────────────────┼────────────────────────┼────────────────────────────────────────┤
  │ Circle via bank transfer │ $0 (but 1-2 day delay) │ Standard ACH/wire to Circle            │
  └──────────────────────────┴────────────────────────┴────────────────────────────────────────┘
  Floor: $0 - Circle doesn't charge to mint/redeem USDC. They profit from the float (investing reserves in T-bills).

  Source: https://developers.circle.com/circle-mint/docs/getting-started-with-circle-mint

  ---
  3. Blockchain Transfer (USDC to Egypt Partner)
  ┌──────────────────────────────┬───────────────┬──────────┐
  │            Chain             │    Cost/tx    │ Finality │
  ├──────────────────────────────┼───────────────┼──────────┤
  │ Solana                       │ $0.0001-0.001 │ ~400ms   │
  ├──────────────────────────────┼───────────────┼──────────┤
  │ Tron                         │ $0.001-0.01   │ ~3s      │
  ├──────────────────────────────┼───────────────┼──────────┤
  │ Ethereum L2 (Base, Arbitrum) │ $0.01-0.05    │ ~2s      │
  ├──────────────────────────────┼───────────────┼──────────┤
  │ Ethereum mainnet             │ $0.50-5.00    │ ~12s     │
  └──────────────────────────────┴───────────────┴──────────┘
  Floor: ~$0.0005 on Solana

  ---
  4. Compliance
  ┌──────────────────┬─────────────────┬──────────────────────────────────────────────────────────────────────────────────────────┐
  │    Component     │  Minimum cost   │                                      How to achieve                                      │
  ├──────────────────┼─────────────────┼──────────────────────────────────────────────────────────────────────────────────────────┤
  │ KYC              │ $0.50-1.00/user │ Volume discounts with Persona/Onfido (50k+ users), or use Plaid Identity ($0.50)         │
  ├──────────────────┼─────────────────┼──────────────────────────────────────────────────────────────────────────────────────────┤
  │ Sanctions (OFAC) │ $0              │ Download OFAC SDN list yourself, build matching logic. Free.                             │
  ├──────────────────┼─────────────────┼──────────────────────────────────────────────────────────────────────────────────────────┤
  │ AML monitoring   │ $0-0.05/tx      │ Build rules engine yourself (not hard for basic patterns) vs $500+/mo for Sardine/Unit21 │
  └──────────────────┴─────────────────┴──────────────────────────────────────────────────────────────────────────────────────────┘
  Floor: ~$0.50/user (KYC) + ~$0/tx (DIY sanctions + AML)

  DIY Sanctions approach:
  - OFAC publishes SDN list as XML: https://sanctionslist.ofac.treas.gov/Home/SdnList
  - Update daily via cron job
  - Fuzzy match sender/recipient names against list
  - Flag matches for manual review

  DIY AML approach (basic):
  Flag if:
  - Single tx > $3,000 (CTR threshold is $10k, but flag lower for review)
  - Cumulative 24hr > $5,000 from same user
  - New user + large first tx
  - Recipient in high-risk region
  - Structuring pattern (multiple $900 txs)

  ---
  5. Egypt Payout (THE BIG ONE)

  This is where most cost lives. Someone must:
  1. Accept your USDC
  2. Provide EGP liquidity
  3. Execute payout
  ┌─────────────────────────────┬──────────┬──────────────────────────────────────────────────────────────────────────────────────┐
  │          Approach           │   Cost   │                                   What's required                                    │
  ├─────────────────────────────┼──────────┼──────────────────────────────────────────────────────────────────────────────────────┤
  │ PSP partner (Paymob, Fawry) │ 1.5-3%   │ Just API integration                                                                 │
  ├─────────────────────────────┼──────────┼──────────────────────────────────────────────────────────────────────────────────────┤
  │ Direct bank partnership     │ 0.5-1%   │ Egypt entity, relationship with CIB/Banque Misr                                      │
  ├─────────────────────────────┼──────────┼──────────────────────────────────────────────────────────────────────────────────────┤
  │ OTC desk + own payout       │ 0.2-0.5% │ Egypt entity, OTC relationship (e.g., Cumberland, Circle), agent network or bank API │
  ├─────────────────────────────┼──────────┼──────────────────────────────────────────────────────────────────────────────────────┤
  │ Own liquidity + license     │ 0.1-0.3% │ Full PSP license, hold EGP float, manage FX risk                                     │
  └─────────────────────────────┴──────────┴──────────────────────────────────────────────────────────────────────────────────────┘
  Floor: ~0.2-0.3% with own Egypt entity + OTC liquidity + direct bank/mobile money rails

  What it takes:
  - Egyptian subsidiary (LLC registration ~$2-5k, ongoing ~$5k/yr)
  - CBE sandbox or PSP license
  - OTC desk relationship for USDC→EGP (Cumberland, FalconX, or Circle's OTC)
  - Direct integration with InstaPay (Egypt's instant payment system) or Vodafone Cash API

  ---
  Fully Optimized Cost Summary
  ┌─────────────────┬───────────────────────────────┬─────────────────────┐
  │    Component    │        Optimized cost         │     Complexity      │
  ├─────────────────┼───────────────────────────────┼─────────────────────┤
  │ ACH pull        │ $0.02                         │ Very high (own MTL) │
  ├─────────────────┼───────────────────────────────┼─────────────────────┤
  │ USD→USDC        │ $0.00                         │ Low                 │
  ├─────────────────┼───────────────────────────────┼─────────────────────┤
  │ Blockchain      │ $0.001                        │ Low                 │
  ├─────────────────┼───────────────────────────────┼─────────────────────┤
  │ Sanctions/AML   │ $0.00                         │ Medium (DIY)        │
  ├─────────────────┼───────────────────────────────┼─────────────────────┤
  │ KYC (amortized) │ $0.01*                        │ Low                 │
  ├─────────────────┼───────────────────────────────┼─────────────────────┤
  │ Egypt payout    │ $0.50-1.00 (0.3% on $200 avg) │ Very high           │
  ├─────────────────┼───────────────────────────────┼─────────────────────┤
  │ TOTAL           │ ~$0.55-1.05/tx                │                     │
  └─────────────────┴───────────────────────────────┴─────────────────────┘
  *KYC: $0.50/user ÷ ~50 txs/user lifetime = ~$0.01/tx

  vs current estimate of $1.80-3.50/tx — that's 40-70% reduction

  ---
  Realistic "High Effort" Path

  If you're willing to handle complexity but not spend 2 years on MTL:
  ┌────────────┬─────────────────────────────────────────┬───────────────┐
  │ Component  │                Approach                 │     Cost      │
  ├────────────┼─────────────────────────────────────────┼───────────────┤
  │ US intake  │ BaaS (Bridge/Zero Hash) - they have MTL │ $0.10-0.20/tx │
  ├────────────┼─────────────────────────────────────────┼───────────────┤
  │ Conversion │ Circle direct                           │ $0.00         │
  ├────────────┼─────────────────────────────────────────┼───────────────┤
  │ Blockchain │ Solana                                  │ $0.001        │
  ├────────────┼─────────────────────────────────────────┼───────────────┤
  │ Compliance │ DIY sanctions + basic AML rules         │ $0.00         │
  ├────────────┼─────────────────────────────────────────┼───────────────┤
  │ KYC        │ Plaid Identity or Persona (volume deal) │ $0.50/user    │
  ├────────────┼─────────────────────────────────────────┼───────────────┤
  │ Egypt      │ Own entity + OTC + direct rails         │ 0.3-0.5%      │
  └────────────┴─────────────────────────────────────────┴───────────────┘
  Realistic optimized: ~$0.80-1.20/tx on $200 transfer




---

## Build vs Buy Decision Matrix

| Component | Recommendation | Rationale |
|-----------|----------------|-----------|
| US bank integration | **Buy** (Plaid) | 6+ months to build, $500k+ |
| Blockchain rails | **Buy** (Circle) | Compliance, custody handled |
| KYC | **Buy** (Persona) | Regulatory expertise built-in |
| Ledger | **Build** | Core competency, simple enough |
| Transfer orchestration | **Build** | Core product, must own |
| Egypt payout | **Partner** | Must use licensed local entity |



### Minimum Team in Claude's view (I - Adam - dispute this - too big too slow). Maybe team of 2-3 better imo

| Role | Count | Notes |
|------|-------|-------|
| Backend engineer | 2 | One senior, one mid |
| Frontend/mobile | 1 | React Native + web |
| DevOps/Infra | 0.5 | Can be part-time or contractor |
| Compliance | 1 | Critical for MTL process |

**Total: 4-5 people for MVP**

---

## Key Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| US Money Transmitter License | Partner with licensed entity (e.g., Stripe Treasury, Unit, Synapse) instead of own license. Own MTL takes 12-24 months, $500k+ legal |
| Egypt partner reliability | Have 2+ payout partners; build failover logic |
| Blockchain volatility | Never hold crypto > minutes; instant conversion via Circle |
| Downtime during transfer | Idempotent operations + state machine allows safe retries |

---



## Useful Links

- Circle USDC API: https://developers.circle.com/
- Plaid API: https://plaid.com/docs/
- AWS compliance programs: https://aws.amazon.com/compliance/programs/
- NestJS framework: https://nestjs.com/
- Medici ledger library: https://github.com/flash-oss/medici
- Unit (Banking-as-a-Service with MTL): https://www.unit.co/
- Egypt Central Bank FinTech sandbox: https://www.cbe.org.eg/en/financial-technology/regulatory-sandbox

---


## Security Architecture

| Layer | Implementation |
|-------|----------------|
| **Encryption at rest** | AES-256 (RDS, S3 default) |
| **Encryption in transit** | TLS 1.3 everywhere |
| **Secrets management** | AWS Secrets Manager / HashiCorp Vault |
| **Auth** | OAuth2 + JWT (short-lived tokens), refresh token rotation |
| **API security** | Rate limiting, request signing for partner APIs |
| **Wallet security** | HSM-backed keys for blockchain ops (Circle handles this) |
| **Audit logging** | Immutable logs to S3 + CloudWatch |

---



## Security Checklist for MVP

  Must have before launch:
  - TLS everywhere
  - Circle custody (don't hold keys yourself)
  - MFA on admin accounts
  - Rate limiting
  - Secrets in Secrets Manager (not env vars)
  - Basic fraud rules (velocity, new recipient delay)
  - Audit logging to immutable store
  - Input validation / parameterized queries

  Can wait until scale:
  - Pentest
  - HSM for self-custody
  - SOC2 certification (~$30-50k)
  - Device fingerprinting
  - Advanced behavioral fraud detection





## Claude take on security
  ---
  Security Architecture

  Threat Model
  ┌──────────────────────────┬────────────────────────────────────┬───────────────────────────┐
  │          Asset           │               Threat               │          Impact           │
  ├──────────────────────────┼────────────────────────────────────┼───────────────────────────┤
  │ User credentials         │ Account takeover                   │ Fraudulent transfers      │
  ├──────────────────────────┼────────────────────────────────────┼───────────────────────────┤
  │ USDC wallet keys         │ Key theft                          │ Total loss of funds       │
  ├──────────────────────────┼────────────────────────────────────┼───────────────────────────┤
  │ User PII                 │ Data breach                        │ Regulatory + reputational │
  ├──────────────────────────┼────────────────────────────────────┼───────────────────────────┤
  │ API keys (Plaid, Circle) │ Credential leak                    │ Unauthorized transactions │
  ├──────────────────────────┼────────────────────────────────────┼───────────────────────────┤
  │ Database                 │ SQL injection, unauthorized access │ Data theft, manipulation  │
  └──────────────────────────┴────────────────────────────────────┴───────────────────────────┘
  Security Controls by Layer

  1. Authentication & Access
  ┌────────────────────┬───────────────────────────────────────────────────────────────────────────┐
  │      Control       │                              Implementation                               │
  ├────────────────────┼───────────────────────────────────────────────────────────────────────────┤
  │ User auth          │ OAuth2 + JWT (15min expiry), refresh token rotation                       │
  ├────────────────────┼───────────────────────────────────────────────────────────────────────────┤
  │ MFA                │ TOTP (Google Auth) or SMS for high-risk actions (new recipient, large tx) │
  ├────────────────────┼───────────────────────────────────────────────────────────────────────────┤
  │ Session management │ Redis-backed sessions, invalidate on password change                      │
  ├────────────────────┼───────────────────────────────────────────────────────────────────────────┤
  │ Admin access       │ SSO (Google Workspace/Okta), require MFA, audit all actions               │
  ├────────────────────┼───────────────────────────────────────────────────────────────────────────┤
  │ API auth           │ API keys with HMAC request signing for partner integrations               │
  └────────────────────┴───────────────────────────────────────────────────────────────────────────┘
  2. Wallet & Key Management (CRITICAL)
  ┌───────────────────────┬────────────────────────────────────────────────┬───────────────────────┐
  │       Approach        │                    Security                    │         Cost          │
  ├───────────────────────┼────────────────────────────────────────────────┼───────────────────────┤
  │ Circle Custody        │ Circle holds keys in HSM, you never touch them │ Free (use Circle API) │
  ├───────────────────────┼────────────────────────────────────────────────┼───────────────────────┤
  │ Self-custody with HSM │ AWS CloudHSM or GCP Cloud HSM                  │ ~$1,000/mo            │
  ├───────────────────────┼────────────────────────────────────────────────┼───────────────────────┤
  │ Self-custody with MPC │ Fireblocks, Fordefi                            │ ~$500-2000/mo         │
  └───────────────────────┴────────────────────────────────────────────────┴───────────────────────┘
  Recommendation: Use Circle's custody. You never hold private keys = you can't lose them.

  If you must self-custody:
  - Keys generated in HSM, never exported
  - Multi-sig (2-of-3) for any withdrawal
  - Cold wallet for reserves (>90% of funds)
  - Hot wallet for operations (<10%, daily limit)
  - Automatic sweep: hot → cold when threshold exceeded

  3. Data Protection
  ┌──────────────┬────────────────────────────────────────────────────────────────┐
  │    Layer     │                            Control                             │
  ├──────────────┼────────────────────────────────────────────────────────────────┤
  │ In transit   │ TLS 1.3 everywhere, HSTS, cert pinning on mobile               │
  ├──────────────┼────────────────────────────────────────────────────────────────┤
  │ At rest      │ AES-256 (database, S3), encrypt PII columns specifically       │
  ├──────────────┼────────────────────────────────────────────────────────────────┤
  │ PII handling │ Tokenize sensitive fields (SSN, bank account), separate PII DB │
  ├──────────────┼────────────────────────────────────────────────────────────────┤
  │ Secrets      │ AWS Secrets Manager or Vault, never in code/env files in repo  │
  ├──────────────┼────────────────────────────────────────────────────────────────┤
  │ Backups      │ Encrypted, tested restore monthly, geo-redundant               │
  └──────────────┴────────────────────────────────────────────────────────────────┘
  4. Application Security
  ┌─────────────────────┬────────────────────────────────────────────────────────────────┐
  │       Control       │                         Implementation                         │
  ├─────────────────────┼────────────────────────────────────────────────────────────────┤
  │ Input validation    │ Whitelist validation, parameterized queries (no SQL injection) │
  ├─────────────────────┼────────────────────────────────────────────────────────────────┤
  │ Rate limiting       │ Per-user: 10 req/s, Per-IP: 100 req/s, escalating blocks       │
  ├─────────────────────┼────────────────────────────────────────────────────────────────┤
  │ CORS                │ Whitelist only your domains                                    │
  ├─────────────────────┼────────────────────────────────────────────────────────────────┤
  │ CSP                 │ Strict Content-Security-Policy headers                         │
  ├─────────────────────┼────────────────────────────────────────────────────────────────┤
  │ Dependency scanning │ Dependabot/Snyk, block PRs with critical vulns                 │
  ├─────────────────────┼────────────────────────────────────────────────────────────────┤
  │ Penetration testing │ Annual third-party pentest (~$10-30k)                          │
  └─────────────────────┴────────────────────────────────────────────────────────────────┘
  5. Fraud Prevention
  ┌───────────────────────┬─────────────────────────────────────────────────────────┐
  │        Control        │                          Logic                          │
  ├───────────────────────┼─────────────────────────────────────────────────────────┤
  │ Velocity limits       │ Max $X/day per user, max Y txs/day                      │
  ├───────────────────────┼─────────────────────────────────────────────────────────┤
  │ New recipient delay   │ First tx to new recipient: 24hr hold (or reduced limit) │
  ├───────────────────────┼─────────────────────────────────────────────────────────┤
  │ Device fingerprinting │ Flag new device + large tx                              │
  ├───────────────────────┼─────────────────────────────────────────────────────────┤
  │ Behavioral            │ Flag if tx pattern suddenly changes                     │
  └───────────────────────┴─────────────────────────────────────────────────────────┘
  6. Monitoring & Incident Response
  ┌──────────────────┬──────────────────────────────────────────────────────────────────────┐
  │    Component     │                                 Tool                                 │
  ├──────────────────┼──────────────────────────────────────────────────────────────────────┤
  │ Log aggregation  │ Datadog, or cheaper: Logtail/Papertrail                              │
  ├──────────────────┼──────────────────────────────────────────────────────────────────────┤
  │ Alerting         │ PagerDuty for critical (wallet anomaly, auth spike)                  │
  ├──────────────────┼──────────────────────────────────────────────────────────────────────┤
  │ Audit trail      │ Immutable logs to S3 (separate account), retain 7 years              │
  ├──────────────────┼──────────────────────────────────────────────────────────────────────┤
  │ Incident runbook │ Document: who to call, how to freeze wallets, regulator notification │
  └──────────────────┴──────────────────────────────────────────────────────────────────────┘
  ---




## Info on services we might use

 Summary Table
  ┌───────────────────┬─────────────────┬────────────────────────────────┬────────────────────────────────┐
  │       Term        │    Category     │          What it does          │         Your use case          │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ NACHA files       │ US payments     │ Batch ACH instructions         │ Pull USD from users cheaply    │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ FedNow            │ US payments     │ Instant bank transfers         │ Instant funding (future)       │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ BaaS              │ US licensing    │ Operate under their MTL        │ Launch without own license     │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ Persona/Onfido    │ KYC             │ Document + selfie verification │ Verify user identity at signup │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ Plaid Identity    │ KYC             │ Bank-verified identity         │ Cheaper/faster KYC alternative │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ OFAC SDN          │ Compliance      │ Sanctions list                 │ Block prohibited persons       │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ AML Monitoring    │ Compliance      │ Detect suspicious patterns     │ Flag/report money laundering   │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ PSP License Egypt │ Egypt licensing │ Legal to process payments      │ Needed to operate directly     │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ InstaPay          │ Egypt payments  │ Instant EGP transfers          │ Fast payout to recipients      │
  ├───────────────────┼─────────────────┼────────────────────────────────┼────────────────────────────────┤
  │ OTC               │ Egypt liquidity │ USDC→EGP conversion            │ Get EGP at good rates          │
  └───────────────────┴─────────────────┴────────────────────────────────┴────────────────────────────────┘
  ---


#### Direct NACHA Files

  What it is: NACHA (National Automated Clearing House Association) is the organization that runs ACH - the US bank-to-bank transfer system. A NACHA file is a standardized text file format that instructs banks to move money.

  How it works:
  1. You create a .txt file in NACHA format containing payment instructions
  2. Upload to your bank's SFTP server (or API)
  3. Bank submits to ACH network
  4. Settlement in 1-2 business days (or same-day ACH for small fee)

  Example NACHA file (simplified):
  101 123456789 9876543211234567890COMPANY NAME        BANK NAME
  5200COMPANY NAME                    1234567890PPDPAYROLL   230115   1091000010000001
  62212345678901234567890123456789012345678900000010000               1091000010000002
  ...

  How you'd use it:
  - Pull funds from customer bank accounts (debits)
  - Batch hundreds/thousands of transactions into one file
  - Submit once per day

  Requirements:
  - Bank account with ACH origination privileges
  - ODFI (Originating Depository Financial Institution) agreement with your bank
  - Usually requires MTL or being a registered business

  Cost: ~$0.01-0.03 per transaction (vs $0.30+ via Plaid)



## FedNow (Instant US Payments)

  What it is: Federal Reserve's instant payment system, launched July 2023. Money moves in seconds, 24/7/365, directly between banks.

  How it works:
  1. User initiates payment in your app
  2. Your system sends request to your bank via FedNow API
  3. Fed validates and moves funds instantly
  4. Recipient bank credits account in <30 seconds
  5. Settlement is immediate and final

  How you'd use it:
  - Instant funding of user's transfer (no 1-2 day ACH wait)
  - Could enable "instant send" as premium feature

  Current state:
  - ~1,400 banks connected (as of late 2025), growing
  - Not all banks support it yet
  - API access varies by bank

  Cost: ~$0.01-0.05 per transaction

  Limitation: Requires bank partnership that offers FedNow access. Most fintechs don't have this yet.



## KYC Providers Persona / Onfido

  Persona / Onfido

  What they are: Identity verification services. User uploads ID + takes selfie, they verify it's real and matches.

  How it works:
  1. User clicks "Verify Identity" in your app
  2. Opens Persona/Onfido widget (embedded iframe or redirect)
  3. User uploads driver's license/passport
  4. User takes live selfie
  5. AI checks:
     - Document is real (not photoshopped)
     - Face matches document
     - Document not expired
     - Name/DOB extraction
  6. Returns verification result to your backend via webhook

  What they check:
  - Document authenticity (security features, fonts, holograms)
  - Liveness detection (not a photo of a photo)
  - Face match (selfie vs ID photo)
  - Database checks (optional: SSN verification, address verification)

  Cost: $2-5 per verification. Claude thinks that at volume (>50,000) it gets much cheaper.

  Links:
  - Persona: https://withpersona.com
  - Onfido: https://onfido.com


  #### KYC with Plaid Identity

Cheaper than Persona or Onfido at smaller scale

  What it is: KYC via bank login. Instead of uploading documents, user logs into their bank, and Plaid pulls verified identity data from the bank.

  How it works:
  1. User clicks "Verify via Bank"
  2. Opens Plaid Link widget
  3. User logs into their bank (Chase, BofA, etc.)
  4. Plaid pulls identity data the bank has on file:
     - Legal name
     - Address
     - Phone
     - Email
     - SSN (last 4 or full)
  5. Bank already verified this when account was opened

  Advantage:
  - Faster (no document upload)
  - Higher completion rate (users already trust bank login)
  - Cheaper ($0.50-1.50 vs $2-5)

  Disadvantage:
  - Only works if user has US bank account
  - Some regulators prefer document-based KYC



#### OFAC SDN list 

The Specially Designated Nationals list. US Treasury's list of people, companies, and countries you're legally prohibited from doing business with. Terrorists, drug traffickers, sanctioned regimes, etc.

Full list: https://sanctionslist.ofac.treas.gov/Home/SdnList

  How it works:
  1. Download the list (XML/CSV format, ~30MB)
  2. Parse into searchable database
  3. On every transfer, check sender name + recipient name against list
  4. If match → block transaction, file SAR (Suspicious Activity Report)

  The list contains:
  - ~12,000 individuals and entities
  - Names (including aliases/alternate spellings)
  - Addresses
  - DOBs
  - Passport numbers
  - Associated countries


#### AML Monitoring

  What it is: Anti-Money Laundering monitoring. Detecting suspicious transaction patterns that might indicate money laundering, terrorist financing, or fraud.

 Common rules Claude suggests:
  ┌─────────────────────────────┬───────────────────────────────────┬─────────────────────────────────────────────────┐
  │            Rule             │              Trigger              │                       Why                       │
  ├─────────────────────────────┼───────────────────────────────────┼─────────────────────────────────────────────────┤
  │ Large transaction           │ >$3,000 single tx                 │ Potential structuring, needs review             │
  ├─────────────────────────────┼───────────────────────────────────┼─────────────────────────────────────────────────┤
  │ Structuring                 │ Multiple txs just under threshold │ Classic money laundering technique              │
  ├─────────────────────────────┼───────────────────────────────────┼─────────────────────────────────────────────────┤
  │ Velocity                    │ >X txs per day/week               │ Unusual activity                                │
  ├─────────────────────────────┼───────────────────────────────────┼─────────────────────────────────────────────────┤
  │ Round amounts               │ Exact $1,000, $2,000              │ Suspicious (legitimate txs usually odd amounts) │
  ├─────────────────────────────┼───────────────────────────────────┼─────────────────────────────────────────────────┤
  │ New account + high activity │ <30 days old + large volume       │ Account farming                                 │
  ├─────────────────────────────┼───────────────────────────────────┼─────────────────────────────────────────────────┤
  │ High-risk country           │ Certain destinations              │ FATF grey/blacklist countries                   │
  ├─────────────────────────────┼───────────────────────────────────┼─────────────────────────────────────────────────┤
  │ Pattern change              │ Sudden change in behavior         │ Compromised account or new criminal use         │
  └─────────────────────────────┴───────────────────────────────────┴─────────────────────────────────────────────────┘
  What happens when flagged:
  1. Transaction held for manual review
  2. Compliance officer reviews
  3. If suspicious → file SAR with FinCEN
  4. If clearly bad → close account, report

  Cost:
  - DIY: $0 (just code)
  - Enterprise (Sardine, Unit21, Alloy): $500-2000/mo base + per-tx fees


#### PSP License Egypt

  What it is: Payment Service Provider license from the Central Bank of Egypt. Required to legally process payments in Egypt.

  What it allows:
  - Accept payments from customers
  - Hold customer funds (e-wallets)
  - Transfer money between accounts
  - Connect to Egyptian payment rails (InstaPay, etc.)

  How to get it:
  ┌────────────────────┬─────────────────────────────────────────────────────────┬─────────────┐
  │       Stage        │                      What happens                       │    Time     │
  ├────────────────────┼─────────────────────────────────────────────────────────┼─────────────┤
  │ Pre-application    │ Informal discussions with CBE                           │ 1-2 months  │
  ├────────────────────┼─────────────────────────────────────────────────────────┼─────────────┤
  │ Application        │ Submit business plan, financials, tech docs, AML policy │ -           │
  ├────────────────────┼─────────────────────────────────────────────────────────┼─────────────┤
  │ Review             │ CBE evaluates application                               │ 3-6 months  │
  ├────────────────────┼─────────────────────────────────────────────────────────┼─────────────┤
  │ Sandbox (optional) │ Test with limited users/volume                          │ 6-12 months │
  ├────────────────────┼─────────────────────────────────────────────────────────┼─────────────┤
  │ Full license       │ Approval to operate commercially                        │ -           │
  └────────────────────┴─────────────────────────────────────────────────────────┴─────────────┘
  Requirements:
  - Egyptian registered company (LLC or JSC)
  - Minimum capital (varies, typically EGP 5-25M / ~$100-500k)
  - Local directors/management
  - Office in Egypt
  - Detailed AML/KYC policies
  - Technology audit
  - Insurance

  Alternative: Use CBE Regulatory Sandbox first (https://www.cbe.org.eg/en/financial-technology/regulatory-sandbox) - lets you operate with limited scope while testing.

  Cost: ~$50-150k total (legal, capital, setup)




## InstaPay Egypt

  What it is: Egypt's instant payment system, launched 2022. Bank-to-bank transfers in seconds, 24/7.

  How it works:
  1. Sender initiates transfer via bank app or third-party
  2. Request goes to sender's bank
  3. Bank routes through InstaPay (run by EBC - Egyptian Banks Company)
  4. Recipient bank credits account instantly
  5. Settlement between banks happens separately (not your problem)

  How you'd use it:
  - Final leg of payout: Your Egypt partner sends EGP to recipient via InstaPay
  - Instant delivery vs 1-2 day standard bank transfer

  Integration:
  - You don't integrate directly (requires bank license)
  - Your Egypt PSP partner (Paymob, Fawry) has InstaPay access
  - Or: partner directly with an Egyptian bank that offers InstaPay API

  Cost: ~EGP 5-15 per transaction (~$0.10-0.30)

  Coverage: All major Egyptian banks connected




#### OTC Crypto / OTC Liquidity

  What OTC is: Over-The-Counter trading. Large trades done directly between two parties, not on a public exchange. Used to avoid slippage on large amounts.

  Why it matters for you:
  You need to convert USDC → EGP. Two options:

  Option A: Exchange
  Put USDC on Binance/Kraken → Trade for EGP → Withdraw
  Problem:
  - Slippage on large orders
  - Exchange fees (0.1-0.5%)
  - EGP pairs have low liquidity
  - Withdrawal delays

  Option B: OTC Desk
  Contact OTC desk → Agree on rate → Send USDC → Receive EGP
  Advantages:
  - Fixed rate agreed upfront (no slippage)
  - Lower fees for large volume (0.1-0.3%)
  - Direct settlement
  - Can handle $100k+ daily

  How OTC works in practice:

  1. You: "I need to sell 50,000 USDC for EGP"

  2. OTC desk quotes: "We'll give you EGP 2,480,000"
     (Rate: 49.60 EGP/USD, vs market 49.70 = 0.2% spread)

  3. You agree

  4. You send 50,000 USDC to their wallet address

  5. They send EGP 2,480,000 to your Egyptian bank account
     (or your Egypt partner's account)

  6. Done in <1 hour

  OTC providers that handle emerging market currencies:
  ┌────────────────────────────┬──────────────────┬───────────┬───────────────────────────────────┐
  │          Provider          │     Coverage     │ Min trade │               Notes               │
  ├────────────────────────────┼──────────────────┼───────────┼───────────────────────────────────┤
  │ Cumberland (cumberland.io) │ Global           │ $100k     │ DRW subsidiary, very established  │
  ├────────────────────────────┼──────────────────┼───────────┼───────────────────────────────────┤
  │ Circle OTC                 │ Global           │ $100k     │ Direct from USDC issuer           │
  ├────────────────────────────┼──────────────────┼───────────┼───────────────────────────────────┤
  │ FalconX                    │ Global           │ $50k      │ Good for smaller volumes          │
  ├────────────────────────────┼──────────────────┼───────────┼───────────────────────────────────┤
  │ Yellow Card                │ Africa focus     │ $10k      │ Specializes in African currencies │
  ├────────────────────────────┼──────────────────┼───────────┼───────────────────────────────────┤
  │ BVNK                       │ Emerging markets │ $25k      │ Good EGP coverage                 │
  └────────────────────────────┴──────────────────┴───────────┴───────────────────────────────────┘
  "OTC Liquidity" means:
  Having a reliable OTC partner who can consistently convert your USDC to EGP at predictable rates. Without this, you're exposed to:
  - Exchange rate fluctuation between customer payment and payout
  - Inability to fulfill large volumes
  - Delays

  How you'd set this up:
  1. Establish relationship with 2+ OTC desks (redundancy)
  2. Negotiate rates based on expected volume
  3. Set up settlement accounts (their USDC wallet, your EGP account)
  4. Automate via API (some offer this) or manual daily batches

  Cost: 0.1-0.5% spread on the exchange rate





### AML Monitoring in USA: Legal Requirements

  In the US (under Bank Secrecy Act / FinCEN regulations), you must have a written AML program with these components:

  Required Elements
  ┌──────────────────────────────┬───────────────────────────────────────────────────────────────────┬───────────────────────────────────┐
  │         Requirement          │                           What it means                           │    Penalty for non-compliance     │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ Written AML Policy           │ Documented procedures for detecting/reporting suspicious activity │ Up to $1M/day per violation       │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ Compliance Officer           │ Named individual responsible for AML program                      │ Personal liability for officer    │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ Training                     │ All relevant staff trained on AML, documented annually            │ Regulatory criticism, enforcement │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ Independent Testing          │ Third-party audit of AML program (annual or biennial)             │ Required for MSBs                 │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ Customer Due Diligence (CDD) │ Know who your customers are, their expected activity              │ Account closures, enforcement     │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ Transaction Monitoring       │ Systematic review of transactions for suspicious patterns         │ SARs, enforcement                 │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ SAR Filing                   │ File Suspicious Activity Reports within 30 days of detection      │ Criminal penalties possible       │
  ├──────────────────────────────┼───────────────────────────────────────────────────────────────────┼───────────────────────────────────┤
  │ Record Keeping               │ Retain records for 5 years                                        │ Fines                             │
  └──────────────────────────────┴───────────────────────────────────────────────────────────────────┴───────────────────────────────────┘
  Specifically Required Filings
  ┌───────────────────────────────────┬──────────────────────────────┬─────────────────────────────────────────────────────────┐
  │              Report               │             When             │                        Threshold                        │
  ├───────────────────────────────────┼──────────────────────────────┼─────────────────────────────────────────────────────────┤
  │ SAR (Suspicious Activity Report)  │ Suspicious activity detected │ $2,000+ (or any amount if terrorism suspected)          │
  ├───────────────────────────────────┼──────────────────────────────┼─────────────────────────────────────────────────────────┤
  │ CTR (Currency Transaction Report) │ Cash transactions            │ >$10,000 in cash (not applicable for digital transfers) │
  └───────────────────────────────────┴──────────────────────────────┴─────────────────────────────────────────────────────────┘
  What "Transaction Monitoring" Must Include

  FinCEN doesn't prescribe exact rules, but expects you to detect:

  - Structuring (breaking up transactions to avoid reporting)
  - Unusual transaction patterns for customer profile
  - Transactions with high-risk jurisdictions
  - Rapid movement of funds (in-and-out quickly)
  - Round dollar amounts in unusual patterns
  - Multiple accounts controlled by same person

  Practical Minimum for a Startup

  1. Write an AML policy (template available, ~10-20 pages)
  2. Name a compliance officer (can be a founder initially)
  3. Build basic transaction monitoring (the rules I showed earlier)
  4. Set up SAR filing process (via FinCEN's BSA E-Filing system: https://bsaefiling.fincen.treas.gov)
  5. Document everything (audit trail of all decisions)
  6. Annual training (can be online course + quiz)
  7. Independent review (every 12-18 months, ~$5-15k)

  If using BaaS partner: They handle most of this. You still nee