# FX Receivable Exposure & Hedging Strategy – EUR/USD Decision Memo

**Created by:** Matthew Furusho
**Updated by:** Matthew Furusho
**Date Created:** April 3, 2026
**Date Updated:** April 3, 2026
**Version:** 1.0
**LLM Used:** Claude (Anthropic)

---

## Executive Summary

Our aerospace division expects to receive €20,000,000 from a European buyer on April 3, 2027. At today's EUR/USD spot rate of 1.1544, that receivable is worth approximately **$23,088,000 USD**. Because EUR/USD has swung nearly 12% over the past 52 weeks, leaving this exposure unhedged puts a material portion of those proceeds at risk. This memo outlines the exposure, the downside risk, three hedging strategies, and next steps for Stages 2–4.

---

## Exposure

| Parameter | Value |
|---|---|
| Currency / Amount | EUR / €20,000,000 |
| Payment Date | April 3, 2027 (1 year) |
| Spot Rate (April 3, 2026) | 1.1544 USD/EUR |
| USD Value at Spot | ~$23,088,000 |
| 1-Year Forward Rate | 1.0935 USD/EUR |
| USD Interest Rate | 3.75% (Fed Funds) |
| EUR Interest Rate | 2.00% (ECB Deposit Facility) |

---

## Risk

If the euro weakens to its recent 52-week low of 1.0805, our €20M receivable would yield only ~$21,610,000 — a **shortfall of ~$1,478,000** versus today's spot value. The current macro environment heightens this uncertainty: the Fed holds rates at 3.50–3.75%, the ECB sits at 2.00% with hike risk building, and Middle East tensions continue to drive energy-led inflation on both sides of the Atlantic.

---

## Three Hedge Strategies

**1. Forward Contract** — Lock in 1.0935 today for a guaranteed ~$21,870,000.
- *Pros:* Zero premium; full certainty; simple to execute.
- *Cons:* No upside participation if EUR strengthens; costly to unwind early.

**2. EUR Put Option** — Buy the right to sell EUR at strike 1.1544; premium = $0.019/EUR (~$380,000 total).
- *Pros:* Downside floor with full upside retained; flexible.
- *Cons:* Upfront nonrefundable premium reduces net proceeds.

**3. Money Market Hedge** — Borrow PV of €20M today, convert at spot, invest USD for one year; repay loan with receivable at maturity.
- *Pros:* No derivative documentation; replicates forward synthetically.
- *Cons:* Ties up balance sheet; requires EUR credit facility.

---

## Next Steps

- **Stage 2 – Excel Model:** Build a working `.xlsx` prototype that computes and compares hedge outcomes across a range of EUR/USD scenarios at maturity.
- **Stage 3 – Technical Specification:** Document the model and design an improved version precise enough for an AI to reconstruct independently.
- **Stage 4 – Final Analysis & Recommendation:** Choose a hedge strategy using model results, write a structured AI prompt, and present the case to the CFO.

---

## References

- Investing.com. (2026, April 3). *EUR/USD Historical Data*. https://www.investing.com/currencies/eur-usd-historical-data
- U.S. Bank Asset Management Group. (2026, March 18). *Federal Reserve holds interest rates steady*. https://www.usbank.com/investing/financial-perspectives/market-news/federal-reserve-interest-rate.html
- European Central Bank. (2026, February 5). *Monetary policy decisions*. https://www.ecb.europa.eu/press/pr/date/2026/html/ecb.mp260205~001d26959b.en.html
- Trading Economics. (2026). *Euro Area Deposit Facility Rate*. https://tradingeconomics.com/euro-area/deposit-interest-rate
