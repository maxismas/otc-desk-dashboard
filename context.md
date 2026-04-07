# OTC Desk — Master Context File
> Last updated: April 2026 | Owner: Max Betro | Status: Living document

---

## 1. Business Overview

We operate a group of OTC desks providing fiat and crypto OTC trading and invoicing services to institutional and business clients. The group is built on the **Flux** platform (trading + invoicing), using **Fireblocks** as the custody and transaction infrastructure.

### Active Entities

| Entity | Jurisdiction | Status | Regulatory License |
|---|---|---|---|
| **40 Acres** (40A) | El Salvador | Active | BSP License: 664bd64379e50005ac479693 (El Salvador Central Bank) · DASP License: PSAD-0046 (CNAD) |
| **Perpolis** (PPLS) | Canada | Active | Registration No: M23871938 |

### Inactive / Pending Entities

| Entity | Jurisdiction | Status | Blocker |
|---|---|---|---|
| Lunar Ark | Dubai (UAE) | Pending | Awaiting VARA license |
| Becfin | Austria | Pending | Awaiting regulator feedback |
| Paidly | Comoro Island | Pending | LP and Ops team activation in progress — high-risk clients only. Head of Paidly & UBO: Elton Lu. Operations conducted by Emana (Indian entity, hiring in progress). Only LP is Rockwallet — note: Rockwallet is closing. |
| Lunar Rails LTD | Cayman Islands | Pending | Custodial license — application not yet started |

---

## 2. Entity Profiles

### 2.1 40 Acres (40A)

- **Full name:** 40 Acres Sociedad de S.V
- **UBO:** Francesco Vivoli & Mark Singh
- **Address:** Calle Cuscatlan #4312, Colonia Escalón, San Salvador, El Salvador
- **Operating hours:** 10:00 AM GST to 5:00 PM CST (UTC-6)
- **Client service email:** clientservice@40acres.pro
- **Trading platform:** https://trading.40acres.pro/
- **Manager portal:** https://40acres.fluxpayments.tech/manager
- **Currencies traded:** EUR, GBP, USD, CAD (via Aquanow LP)
- **Key note:** Timestamps on trades shown in local timezone; CSV exports are UTC. El Salvador Compliance and Finance must convert to local time for regulatory compliance.

### 2.2 Perpolis / PPLS (Agency)

- **Full name:** Perpolis Ltd.
- **UBO/CEO:** Nathan Montgomery — nathan@perpolis.ca — Signal: +1 (587) 892-6065
- **MLRO:** Mark A. — compliance@perpolis.ca — WhatsApp: +1-905-650-8413
- **Address:** 210-128 West Hastings St, Vancouver, BC, Canada V6B 1G8
- **Website:** https://www.perpolis.ca/
- **Trading platform:** https://perpolis.fluxpayments.tech/
- **Manager portal:** https://perpolis.fluxpayments.tech/manager
- **Operating hours:**
  - Trade execution: 12am–2pm PST (7am start temporary)
  - Trade acceptance: 7am–3pm PST (Canadians only)
- **Currencies traded:** BTC, BCH, ETH, USDC, BSV, LTC, CAD, EUR (USDT for Nodestar only)
- **Telegram contacts:**
  - Operations: +1 (236) 978-6844
  - Finance (new): +1 (604) 712-9558

---

## 3. Products

### 3.1 Flux Invoicing (Crypto → Fiat)

Clients create invoices payable in **USDT or USDC**. Settlement proceeds are paid out in fiat within **~48 hours**. Available via both 40A and PPLS.

**Invoice payment flow:**
1. Client pays invoice on-chain
2. System confirms on-chain settlement
3. Ops and Finance receive email notification
4. Invoice appears as Paid in Manager portal
5. Ops/Finance manually approve fiat payout (net of fees)
6. Funds sent to client's whitelisted address

**Treasury monitoring trigger:** When cumulative Fireblocks fee wallet balance reaches **$50,000 USD** across USDC + USDT, Ops coordinates an OTC/treasury trade with AQN to convert to CAD. LP wires fiat to PPLS / Lunar Rails.

### 3.2 Flux Trading (Crypto OTC)

Clients execute crypto-to-crypto or crypto-to-fiat trades via the integrated Flux trading workflow.

**Trade lifecycle:**
1. **Pre-trade (Compliance):** Client completes KYC via Sumsub → Compliance sets to User Accepted → client submits settlement wallet for whitelisting (auto-screened via Elliptic)
2. **Trade initiation:** Client selects pair, enters notional, chooses whitelisted address → system generates deposit address → client sends crypto → funds auto-screened
3. **Execution:** RFQ sent to LP → auto-accepted if within policy → Fireblocks tx created → Ops manually approves Fireblocks transfer to LP
4. **Settlement:** LP sends counter-asset to merchant wallet → system screens → draft payout prepared net of fees → Slack alert → Ops/Finance manually approve → funds sent to client's whitelisted address
5. **Reporting:** Trade auto-marked complete → Finance records references

---

## 4. Team & Roles

### Internal Team Contacts

| Name | Role | Entity | Contact |
|---|---|---|---|
| Max Betro | Coordinator / Owner | Group | — |
| Kevin | Operations | 40 Acres | kevin@40acres.pro |
| Sofia | Compliance | 40 Acres | sofia@40acres.pro |
| Karla | Finance | 40 Acres | karla@40acres.pro |
| Nathan Montgomery | CEO/UBO | Perpolis | nathan@perpolis.ca · Signal: +1 (587) 892-6065 |
| Mark A. | MLRO / Compliance | Perpolis | compliance@perpolis.ca · WhatsApp: +1-905-650-8413 |
| Elton Lu | Head / UBO | Paidly | — |
| Ronnie | Operations | Group | — |
| Faith | Finance | Group | — |

---

## 5. Banking Channels

### 5.1 40 Acres Banking

| Channel | Status | Currencies | Settlement | Notes |
|---|---|---|---|---|
| BCB | NO-GO | EUR, GBP, CAD, USD | 24–48 hrs | KYB renewal requested — relationship not being renewed. Migrating to Lorum + One.io |
| The Kingdom Bank (TKB) | CONDITIONAL | GBP, EUR, USD | Slow / variable | GBP channel live testing with clients. Full go pending dedicated IBAN (500 EUR). EUR 49k stuck in transit |
| Aquanow LP | GO | EUR, GBP, USD | 24–48 hrs fiat out | Max 1M per currency per withdrawal. API or portal. No docs required |
| Lorum | COMING SOON | TBD | TBD | Application in progress — replacing BCB |
| One.io | COMING SOON | TBD | TBD | Application in progress — replacing BCB |

**BCB details (legacy — for reference):**
- SEPA Instant: up to 1M EUR, settles instantly
- Regular SEPA: no limit, cutoff 1pm UK time
- Frequent KYB requests; funds held if invoices/KYB docs not submitted
- CSM: Yasmin Levi & Thand Mahlangu (Slack)

**TKB details:**
- GBP IBAN cost: 500 EUR (one-off, pending decision)
- Must alert TKB before receiving USD
- Invoice required per transaction
- CSM: Damaris (Telegram)
- Critical: EUR 49,000 stuck in transit TKB → BCB — escalation with TKB rep required

### 5.2 Perpolis Banking

| Channel | Status | Currencies | Settlement | Notes |
|---|---|---|---|---|
| One (Bank) | GO | GBP, EUR, USD (invoicing) | 24–48 hrs | No hard limit with proper docs. Invoice required above $50k |
| Apaylo | CONDITIONAL | CAD only | 24–48 hrs | Domestic Canadian banks only. Cannot send internationally |
| Oneify | NO-GO | Unknown | — | No access. Nathan to advise |
| Aquanow LP | GO | EUR, GBP, USD, CAD | 1–2 hrs LP / 24–48 hrs fiat | Min withdrawal 25k USD/EUR/GBP · 50k CAD. Elton (Admin) must whitelist beneficiary |
| One LP | GO | GBP, EUR, USD | Under 1–2 hrs | Via One Bank rail. No hard limit |

---

## 6. Banking Details (Sending Instructions)

### Apaylo (CAD settlements — both desks)
- **Beneficiary:** Apaylo Finance Technology Inc.
- **Address:** 210-4500 Highway 7, Woodbridge, ON L4L4Y7
- **Currency:** CAD
- **Swift BIC:** CUCXCATTVAN
- **Routing:** 082814492 | **Bank:** 828 | **Transit:** 14492
- **Account:** 100004434080
- **Bank:** Northern Credit Union Ltd., 280 McNabb St, Sault Ste Marie, ON P6A5N9
- **Reference:** APL7484
- ⚠️ Apaylo can only send to domestic Canadian bank accounts via EFT. Clients can only send to Apaylo via domestic wire.

### One.io — Perpolis (EUR — Primary)
- **Account name:** Perpolis Ltd.
- **IBAN:** MT16CFTE28004000000000005270072
- **Bank:** OpenPayd Financial Services Malta Ltd.
- **BIC:** CFTEMTM1XXX
- Supports SEPA CT and SEPA Instant. SWIFT on track for Q1 2026.

### One.io — Perpolis (GBP — Primary)
- **IBAN:** GB74RRCC04135700001073
- **BIC:** CLRBGB22XXX
- **Sort Code:** 04-13-57 | **Account:** 00001073
- **Address:** ONE.io, 6th Floor, King's House, 9-10 Haymarket, London SW1Y 4BP

### One.io — Perpolis (EUR — Backup, untested)
- **IBAN:** LI34 0881 1010 3471 Y219 E

### One.io — Perpolis (GBP SWIFT — International)
- **IBAN:** GB45 CLRB 0405 1101 2638 76

### Aquanow — EUR Deposit (PPLS)
- **Bank:** Bank Frick and Co Aktiengesellschaft, Landstrasse 14, Balzers, Liechtenstein
- **Swift/BIC:** BFRILI22
- **Account:** LI79088110103471Y143E
- **Beneficiary:** CLTS Technologies Ltd, 1400-1095 West Pender St, Vancouver, BC V6E2M6
- **Intermediary Bank:** Deutsche Bundesbank | **BIC:** MARKDEFF
- ⚠️ Reference code must be included on wire or deposit may be delayed

### Aquanow — CAD Deposit (PPLS)
- **Beneficiary:** CLTS Technologies Ltd, 1400-1095 West Pender St, Vancouver, BC V6E2M6
- **Bank:** Servus Credit Union Ltd., 102-420 2nd Street SW, Calgary, AB T2P3K4
- **BIC/SWIFT:** CUCXCATTCAL
- **Routing:** CC089966439
- **Account/IBAN:** 684714220060
- ⚠️ Funds received from third parties will not be accepted — Aquanow only processes transfers from the onboarded legal entity

---

## 7. Liquidity Providers (LPs)

| LP | Code | Trading Hours | Settlement | Currencies | Pre-funding | Min Trade | Contact |
|---|---|---|---|---|---|---|---|
| Aquanow | AQN | 24/7 | Instant (portal) | BTC, USDT, USDC, ETH, DAI, EUR, CAD | No | See AQN table | Adrian Seto (Telegram) |
| ONE.io | ONE | 24/7 | 2–3 hrs after 6pm BST | BTC, BCH, USDT, USDC, ETH, DAI, EUR, CAD | No (pre-fund BCH if indic >1%) | 25K USD equiv. | Alex Brathwaite |
| Rockwallet | RWT | 24/7 | 9am–6pm EST | BTC, BCH, USDT, USDC, ETH, DAI, MNEE, BSV | No (pre-fund BCH if indic >1%, BSV) | 50K USD equiv. | Harbi Likhari |
| BCB | BCB | 6am–8pm UK weekdays | 4pm UK | BTC, ETH, LTC, USDC, USDT, CAD, BSV, BCH | Pre-fund if >500K | 50K USD equiv. | Jame McKeon |
| SH Digital | SHD | 8am–6pm GMT (weekends ok) | 8am–6pm GMT | BTC, USDT, USDC, ETH, BCH, CAD, USD, EUR | No | 25K USD equiv. | Tomer Mazar |

### Aquanow Min Trade/Withdrawal Sizes

| Asset | Min Withdraw | Min Trade Size | Min Size |
|---|---|---|---|
| BTC | 0.001 | 1e-7 | 0.002 |
| ETH | 0.02 | 1e-7 | 0.15 |
| USDT | 100 | 0.01 | 10 |
| USDC | 100 | 0.01 | 10 |
| USD | 25,000* | 0.01 | 10 |
| CAD | 50,000* | 0.01 | 10 |
| EUR | 25,000* | 0.01 | 10 |
| GBP | 25,000* | 0.01 | 10 |

*Convenience charge applies if below minimum: 150 CAD / 75 USD / 50 EUR / 50 GBP. Fee is normally waived on first test transfer — notify AQN in chat.

---

## 8. Client Pricing (What We Charge)

| Trade Type | Fee |
|---|---|
| Crypto to Crypto | 0.5% |
| Crypto to Fiat | 1.0% |

> Note: These are the standard client-facing fees. LP/channel costs are separate (see Section 8 — Fee Structures). The spread between what we pay LPs and what we charge clients is the margin.

**Global Disbursement (CAD via ONE — Perpolis):** An additional **2% service fee** is charged to clients for CAD disbursements where ONE conducts a forex trade on our behalf.

---

## 9. Client Onboarding

### One Bank (Perpolis)

**Account fees:**
- Annual fee: £6,600 per entity
- Application fee: €1,500 (refundable, was €2,000)
- Set up fee: €500 (one-off)
- Monthly maintenance: €250

**Transaction fees:**
- SEPA pay-in (B2B): €20 + 0.25%
- SEPA pay-out (B2B): €20 + 0.15%
- SWIFT pay-in USD/GBP/EUR: €50 + 1.00%
- SWIFT pay-out USD/GBP/EUR: €50 + 0.75%
- FPS (GBP outbound): 50p
- CHAPS (GBP outbound): £20
- SWIFT outbound: £12
- SEPA outbound: £2
- Inbound: Free
- Crypto → Fiat: 0.90%
- Fiat → Crypto: 1.00%
- FX: 1%

**Additional fees:**
- SEPA transfer refund/cancellation: €250
- Account reactivation: €1,000
- Internal transfers (Kingdom Bank users): Free

**Global Disbursement (CAD settlements via ONE):**
For CAD settlements, ONE conducts a forex trade with our EUR/GBP and sends directly to client. Charge client a **2% service fee**.

| Type | Amount | Fee |
|---|---|---|
| Same currency — below 50k | 0.40% (min £50) |
| Same currency — 50k–1m | 0.30% (min £50) |
| Same currency — above 1m | 0.20% (min £50) |
| With FX — below 50k | 1.50% (min £100) |
| With FX — 50k–1m | 1.25% (min £100) |
| With FX — above 1m | 1.00% (min £100) |

### Aquanow LP (both desks)
- BTC spread: 0.4–0.9 bps
- Fiat withdrawal fees: shown as 0 on portal — to be confirmed
- Convenience charge below minimum: 150 CAD / 75 USD / 50 EUR / 50 GBP

### BCB, TKB, Apaylo
- Fees not yet documented — pending confirmation from Kevin (BCB/AQN) and Lisa (Apaylo)

---

## 9. Client Onboarding

> Full onboarding SLA and checklist to be added — document pending.

**40 Acres onboarding flow:**
- Ops monitors clientservice@40acres.pro daily
- New client request → create entry in 40A client onboarding tracker
- Notify #40acres-clients-onboarding Slack channel
- Reply to client requesting preliminary information
- Compliance (Sofia) reviews KYC/AML and sets client to User Accepted
- Finance (Karla) pre-approves document checklist and signs off on source-of-funds narrative

**Perpolis onboarding flow:**
- Client completes KYC via Sumsub
- Ops notifies Compliance that new client has submitted application
- Compliance (Mark A.) reviews and sets client to User Accepted
- Client submits settlement wallet for whitelisting
- Wallet screened automatically via Elliptic
- Approved → Active | Rejected → client must resubmit

**Trading platform:** From next month, the trade sheet will be deprecated. All trading will be conducted exclusively via the Flux trading platform (40A and PPLS).

---

## 11. Compliance & Country Risk

### Risk Framework
Country risk is assessed on a 5-tier scale:
- **Low** — Can onboard
- **Medium** — Can onboard
- **Medium High** — Enhanced KYC/AML review required
- **High** — Restricted — senior compliance sign-off required
- **Prohibited** — Cannot onboard under any circumstances

### Compliance Tools
- **KYC:** Sumsub
- **Wallet screening:** Elliptic (automatic)
- **Custody:** Fireblocks

### Compliance Rules
- Ops must not proceed on any trade until Compliance gives written direction
- Escalate immediately for: RFI, Approve with Exception, or Reject/Block Trade outcomes
- All wallet addresses must be whitelisted before use — only Admin can add beneficiaries in Aquanow

### Notable Country Notes
- **El Salvador (SV):** High risk per framework — home jurisdiction of 40 Acres. Regulatory compliance requires trade timestamps converted from UTC to El Salvador local time.
- **UAE (AE):** Medium High — home jurisdiction of Lunar Ark (pending). Enhanced review applies.
- **Canada (CA):** Medium — home jurisdiction of Perpolis. CAD via Apaylo (domestic only).
- **New Zealand (NZ):** Listed as Prohibited in current risk framework — verify with compliance.

---

## 12. Systems & Tools

| System | Purpose | Access |
|---|---|---|
| Flux (40A) | Trading + invoicing platform | https://trading.40acres.pro / https://40acres.fluxpayments.tech/manager |
| Flux (PPLS) | Trading + invoicing platform | https://perpolis.fluxpayments.tech / https://perpolis.fluxpayments.tech/manager |
| Fireblocks | Custody, transaction approval, fee wallets | One fee wallet per desk required |
| Sumsub | KYC onboarding | Used by Compliance |
| Elliptic | Wallet screening | Automatic on all incoming/outgoing |
| Slack / Front | Client communication monitoring | #40acres-clients-onboarding channel |

**Fireblocks fee wallets:**
- One fee wallet per desk must be created
- Purpose: accumulate invoice fees + support treasury conversion
- Share wallet details with Product for automation
- Note: Fee automation may change — until confirmed live, fees may land in same wallet as deposits

---

## 11. Open Items & Gaps

| # | Item | Owner | Status |
|---|---|---|---|
| 1 | TKB — trace EUR 49,000 stuck in transit to BCB | Max | Funds stuck |
| 2 | TKB GBP IBAN — needed for full go (cost 500 EUR) | Kevin | TBD |
| 3 | Lorum onboarding — 40 Acres banking replacement | Max | In progress |
| 4 | One.io onboarding — 40 Acres banking replacement | Max | In progress |
| 5 | AQN Perpolis EUR/GBP/USD fiat-out — Elton to whitelist beneficiary | Ronnie | TBD |
| 6 | One → test bank return tx — pending Finance approval | Ronnie | Chased Mar 31 |
| 7 | Apaylo transaction fees — awaiting Lisa | Lisa | Messaged |
| 8 | AQN & BCB transfer fees (40 Acres) — Kevin to confirm | Kevin | TBD |
| 9 | Oneify — Nathan to confirm access and viability | Ronnie | Chasing Nathan |
| 10 | AQN AWS server status — impacted by Abu Dhabi situation | Ops | Confirm current status |
| 11 | 40 Acres contact details for Ops, Ops Telegram, Finance — missing from entity profile | Max | To fill in |
| 12 | BCB, TKB, Apaylo fee structures — not documented | Kevin / Lisa | Pending |
| 13 | VARA license for Lunar Ark (Dubai) | — | Pending regulator |
| 14 | Becfin (Austria) — regulator feedback | — | Pending |
| 15 | Paidly (Comoro Island) — LP and Ops activation | — | Pending |
| 16 | Lunar Rails LTD (Cayman) — custodial license application | — | Not started |

---

## 12. What's Still Needed in This Context File

The following sections are missing and should be added as documents become available:

1. **Client onboarding checklist** — full document list required per entity (KYC, KYB, source of funds, corporate docs). Currently partial.
2. **40 Acres internal contacts** — Ops email/Telegram and Finance contact are blank in the entity profile.
3. **Trade sheet / pricing model** — how we price trades to clients (spread, markup over LP rate). Referenced in PPLS doc ("shortcut method on trade sheet") but not documented here.
4. **Fee charged to clients** — we have what we pay channels/LPs but not what we charge clients. Need client-facing fee schedule per desk.
5. **Aquanow bank details for 40 Acres** — CAD details referenced but not fully documented. EUR details need confirmation.
6. **TKB full fee schedule** — available once IBAN is obtained.
7. **Lorum and One.io (40 Acres)** — currencies, limits, fees, banking details once onboarding completes.
8. **Paidly operating procedures** — high-risk client desk, needs its own workflow once activated.
9. **Rockwallet and SH Digital detailed procedures** — listed as LPs but no procedure documented.
10. **Compliance escalation matrix** — who to contact for each type of compliance outcome, per desk.
11. **Channel validation final report** — testing period dates and executive summary still missing from the v1.0 draft.
12. **Ops canned responses** — referenced in PPLS database but not included here.
