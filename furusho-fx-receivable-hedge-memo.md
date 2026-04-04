# FX Receivable Exposure & Hedging Strategy – EUR/USD Decision Memo

**Created by:** [Your Name]
**Updated by:** [Your Name]
**Date Created:** April 3, 2026
**Date Updated:** April 3, 2026
**Version:** 1.0
**LLM Used:** Claude (Anthropic)

---

## Executive Summary (≤150 words)

Our aerospace division expects to receive €20,000,000 from a European customer on approximately April 3, 2027 — one year from today. At today's EUR/USD spot rate of 1.1544, this receivable is worth roughly **$23,088,000 USD**. However, because the euro can fluctuate materially over a 12-month horizon, the actual USD proceeds we collect could be significantly higher or lower than this estimate. EUR/USD has ranged from 1.0805 to 1.2079 over just the past 52 weeks — a swing of nearly 12%. Left unhedged, our receivable carries meaningful downside risk. This memo outlines the nature of the exposure, why it warrants attention, and three hedging strategies worth evaluating. Follow-on stages will build a quantitative model, produce a technical specification, and deliver a final recommendation with a structured AI-assisted analysis.

---

## Background & Objectives

**Scenario:** U.S. Aerospace Manufacturer (Scenario 4)

Our firm has contracted to deliver aerospace components to a European buyer. The contract is denominated in euros, and full payment of **€20,000,000** is scheduled one year from today (April 3, 2027). Once the euro is converted to USD, these proceeds flow directly into our operating budget. The finance team therefore needs certainty — or at minimum, a floor — on what we will receive in dollars.

**The exposure in plain terms:**

| Parameter | Value |
|---|---|
| Receivable Currency | EUR |
| Receivable Amount | €20,000,000 |
| Payment Date | ~April 3, 2027 (1 year) |
| Spot Rate (April 3, 2026) | 1.1544 USD/EUR (Investing.com) |
| Implied USD Value at Spot | ~$23,088,000 |
| 1-Year Forward Rate | 1.0935 USD/EUR |
| Forward-Implied USD Value | ~$21,870,000 |
| USD Interest Rate | 3.75% (Fed Funds upper bound) |
| EUR Interest Rate | 2.00% (ECB Deposit Facility Rate) |

**Why the forward differs from spot:** The forward rate reflects the interest rate differential between the U.S. (3.75%) and the Eurozone (2.00%). U.S. rates are higher, so the USD trades at a forward premium against the euro — meaning our locked-in forward rate of 1.0935 is below today's spot of 1.1544. This is not a penalty; it is the market's arbitrage-free pricing of currency risk through time.

**Primary objectives of this analysis:**
1. Quantify the potential USD gain or loss from leaving the receivable unhedged.
2. Evaluate three hedging families against the unhedged baseline.
3. Select and recommend the strategy best aligned with our risk tolerance and cost constraints.

---

## Methods

### The Risk: What Could Go Wrong for USD Proceeds

EUR/USD has shown it can move sharply in either direction. If the euro weakens against the dollar — for example, falling from 1.1544 today back to its recent low of 1.0805 — our €20M receivable would yield only $21,610,000 instead of the $23,088,000 implied by today's spot. That is a potential **shortfall of approximately $1,478,000** relative to current expectations, with no hedge in place. This type of downside is the core business risk we are managing.

The current macro environment adds further uncertainty: the Fed is holding rates at 3.50%–3.75%, the ECB deposit rate is at 2.00%, Middle East tensions are driving energy price volatility, and markets are pricing in possible ECB rate hikes in 2026. Any of these factors could shift EUR/USD materially in either direction over the next 12 months.

---

### Three Hedge Families

**1. Forward Contract**

A forward contract locks in the rate today at which we will convert our euros in one year. Based on interest rate parity, the indicative 1-year forward is **1.0935 USD/EUR**, giving us a guaranteed USD inflow of approximately **$21,870,000**.

- **Pros:** Complete certainty on the USD amount received; no premium cost; simple to execute with a bank counterparty; ideal for budget planning and cash flow forecasting.
- **Cons:** We give up all upside if the euro strengthens above 1.0935 by settlement. There is also counterparty credit risk, and early termination can be costly if the contract must be unwound.

---

**2. Currency Options (Put on EUR)**

Purchasing a EUR put option (the right, but not the obligation, to sell euros at the strike price) lets us establish a floor on our USD proceeds while retaining upside if the euro appreciates. The scenario specifies a put premium of **$0.019 per EUR**, which on €20M equals a total premium cost of **$380,000**.

- Strike (K): Set at or near today's spot, 1.1544 USD/EUR.
- Floor USD proceeds (at strike): ~$23,088,000 minus $380,000 premium = ~$22,708,000 net floor.
- **Pros:** Downside is capped; upside is preserved if EUR strengthens; flexible — the option can be exercised or left to expire.
- **Cons:** The premium of ~$380,000 is an upfront, nonrefundable cost. If EUR stays near current levels, the premium erodes net proceeds relative to the forward.

---

**3. Money Market Hedge**

A money market hedge replicates the forward synthetically using the spot market and the two countries' interest rates. We would borrow the present value of the €20M receivable today at the EUR borrowing rate, convert to USD at spot, and invest those USD at the USD deposit rate for one year. When the receivable is paid, we use it to repay the EUR loan.

- **Pros:** Uses existing banking facilities; no derivative documentation required; economically equivalent to a forward under covered interest rate parity; effective for firms with established EUR credit lines.
- **Cons:** Requires upfront borrowing capacity in EUR; ties up balance sheet; more operationally complex than a forward contract; interest rate assumptions must hold for the hedge to perform as expected.

---

## Limitations & Next Steps

**Known limitations and assumptions:**
- The forward rate of 1.0935 is taken from the scenario parameters and may differ slightly from live bank quotes depending on bid-ask spread and creditworthiness.
- Option premiums ($0.019 per EUR put; $0.024 per EUR call) are scenario inputs and do not reflect live market quotes.
- The money market hedge assumes borrowing at the ECB deposit rate (2.00%) as a proxy; actual corporate borrowing rates will include a credit spread above this benchmark.
- EUR/USD volatility is not yet quantified; Stage 2 will incorporate implied volatility to assess option value more rigorously.

**Next Steps — Four-Stage Project Plan:**

- **Stage 2 – Excel Model Build:** Construct a working `.xlsx` prototype that computes unhedged, forward, option, and money market hedge outcomes across a range of EUR/USD scenarios at maturity. Output will include net USD proceeds, hedge cost, and P&L sensitivity tables.

- **Stage 3 – Technical Specification:** Document the Stage 2 model architecture and design an enhanced version with sufficient precision for an AI system or developer to reconstruct it independently — including inputs, formulas, outputs, and edge cases.

- **Stage 4 – Final Analysis & Recommendation:** Use model results to select the optimal hedge strategy, draft a structured AI prompt for reproducibility, and present the final recommendation to the CFO with supporting data.

**Owner:** Treasury / FX Risk Management Team
**Timeline:** Stages 2–4 to be completed over the next three weeks.

---

## References

- Investing.com. (2026, April 3). *EUR/USD Historical Data*. https://www.investing.com/currencies/eur-usd-historical-data
- Yahoo Finance. (2026, April 3). *EUR/USD (EURUSD=X) Quote*. https://finance.yahoo.com/quote/EURUSD=X/
- U.S. Bank Asset Management Group. (2026, March 18). *Federal Reserve holds interest rates steady*. https://www.usbank.com/investing/financial-perspectives/market-news/federal-reserve-interest-rate.html
- European Central Bank. (2026, February 5). *Monetary policy decisions*. https://www.ecb.europa.eu/press/pr/date/2026/html/ecb.mp260205~001d26959b.en.html
- Trading Economics. (2026). *United States Fed Funds Interest Rate*. https://tradingeconomics.com/united-states/interest-rate
- Trading Economics. (2026). *Euro Area Deposit Facility Rate*. https://tradingeconomics.com/euro-area/deposit-interest-rate
