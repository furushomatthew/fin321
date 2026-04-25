# Stage 3 – Technical Specification
## FX Receivable Hedge Analysis – EUR/USD

**Author:** Matthew Furusho | Aerospace Division Treasury
**Date:** April 3, 2026
**Version:** 1.0 – Stage 3 Deliverable
**Source Model:** `furusho-matthew-stage2-model.xlsx`

---

## 1. Problem Statement

The Aerospace Division holds a confirmed EUR-denominated receivable of **€20,000,000** due from a European buyer on **April 3, 2027** (365 days). At the April 3, 2026 spot rate of **1.1544 USD/EUR**, the receivable has a current USD equivalent of approximately **$23,088,000**. The EUR/USD pair has traded within a 52-week range of roughly 1.0805–1.2134, implying peak-to-trough volatility of approximately 12%. An adverse move to the 52-week low alone would reduce USD proceeds by approximately **$1,478,000** versus today's spot value. Because the receivable represents a material single-currency cash inflow with no natural USD offset on the balance sheet, the exposure warrants a structured hedging decision prior to settlement.

---

## 2. Inputs (Known Variables)

All variables are defined as named ranges in the model. Yellow-highlighted cells in Section A are editable inputs; all other computed values derive from these.

| Named Range  | Description                         | Value             | Unit         | Source                                 |
|--------------|-------------------------------------|-------------------|--------------|----------------------------------------|
| `FC_AMT`     | EUR receivable notional             | 20,000,000        | EUR          | Stage 1 memo / contract                |
| `S0`         | Spot rate at inception              | 1.1544            | USD per EUR  | Investing.com, April 3, 2026           |
| `F0`         | 1-year forward rate                 | 1.0935            | USD per EUR  | Derived via CIP; confirmed with desk   |
| `R_USD`      | USD interest rate                   | 3.75%             | Annual, flat | Fed Funds upper bound, March 2026      |
| `R_EUR`      | EUR interest rate                   | 2.00%             | Annual, flat | ECB Deposit Facility Rate, Feb 2026    |
| `T_DAYS`     | Days to settlement                  | 365               | Days         | Apr 3, 2026 → Apr 3, 2027             |
| `K_PUT`      | Put option strike                   | 1.1544            | USD per EUR  | ATM, set equal to S0                   |
| `PREM_PUT`   | Put premium per unit of FC          | 0.019             | USD per EUR  | Stage 1 estimate; market quote needed  |
| `K_CALL`     | Call option strike (collar)         | 1.2000            | USD per EUR  | OTM, illustrative                      |
| `PREM_CALL`  | Call premium per unit of FC         | 0.010             | USD per EUR  | Illustrative; adjust with live quote   |

---

## 3. Assumptions & Constraints

- **Interest rate basis:** Simple (flat) annual rates applied as `Rate × (T_DAYS / 365)`. No compounding; no ACT/360 adjustment. All rates are nominal.
- **Day-count convention:** ACT/365 implied. A more rigorous model would apply ACT/360 for USD money markets and ACT/365 for EUR, per market convention.
- **Transaction costs:** Bid-ask spreads and broker fees are excluded. All computations use mid-market rates. A production model should widen rates by a spread assumption (e.g., ±2 pips on forward, ±0.5% on option premium).
- **CIP parity:** The forward rate `F0 = 1.0935` is stated as desk-derived. The CIP-implied rate is `S0 × (1 + R_USD) / (1 + R_EUR) = 1.1544 × 1.0375 / 1.02 ≈ 1.1944`. The material gap (~0.10) between the memo's forward and the CIP-implied rate is flagged in the model's Notes sheet and must be reconciled with a live forward quote before execution.
- **Option style:** European-style exercise assumed. No early exercise, no gamma/delta modeling, no Black-Scholes pricing — premiums are point estimates.
- **Credit and counterparty risk:** Not modeled. Forward and option strategies carry counterparty exposure to the executing bank.
- **Balance sheet:** The money market hedge requires drawing on a EUR credit facility; availability and cost of that facility are not verified in this model.
- **Collar structure:** Put is purchased, call is sold (zero-cost approximation). Net premium = PREM_PUT − PREM_CALL = $0.009/EUR.

---

## 4. Calculation Flow

### 4.1 Forward Contract Hedge

1. Record the agreed forward rate `F0` at inception.
2. Compute locked-in USD proceeds: `FC_AMT × F0 = 20,000,000 × 1.0935 = $21,870,000`.
3. No further computation required at maturity; proceeds are fixed regardless of `S_T`.

### 4.2 Money Market Hedge

1. **Borrow in EUR:** Compute the present value of the receivable to determine borrowing amount: `FC_AMT / (1 + R_EUR × T_DAYS/365) = 20,000,000 / 1.02 = 19,607,843 EUR`.
2. **Convert at spot:** Sell borrowed EUR at `S0`: `19,607,843 × 1.1544 = $22,635,294 USD`.
3. **Invest USD:** Grow USD proceeds for `T_DAYS` at `R_USD`: `22,635,294 × (1 + 0.0375 × 365/365) = $23,484,118 USD`.
4. **Repay EUR loan at maturity** using the receivable (€20M repays €19,607,843 × 1.02 exactly).
5. **Parity check:** Compare MM output to `FC_AMT × F0`. In the current model, the MM hedge yields ~$23,484,118 vs. the forward's $21,870,000 — a difference of ~$1,614,118 — confirming the CIP reconciliation issue noted in Section 3.

### 4.3 Put Option Hedge

1. **Pay premium upfront:** `Total_Put_Cost = PREM_PUT × FC_AMT = 0.019 × 20,000,000 = $380,000`.
2. **At maturity, evaluate payoff:** If `S_T < K_PUT`, exercise the put and sell EUR at `K_PUT`. If `S_T ≥ K_PUT`, sell EUR at market rate `S_T`.
3. **Net USD proceeds:** `MAX(S_T, K_PUT) × FC_AMT − Total_Put_Cost`.
4. At the current spot (S_T = S0 = 1.1544), net proceeds = `$23,088,000 − $380,000 = $22,708,000`.

### 4.4 Collar Strategy (Put + Call)

1. **Buy put** at `K_PUT = 1.1544`, pay `PREM_PUT = $0.019/EUR`.
2. **Sell call** at `K_CALL = 1.2000`, collect `PREM_CALL = $0.010/EUR`.
3. **Net collar cost:** `(PREM_PUT − PREM_CALL) × FC_AMT = 0.009 × 20,000,000 = $180,000`.
4. **At maturity payoff:**
   - If `S_T < K_PUT`: proceeds = `K_PUT × FC_AMT − Net_Cost = $23,088,000 − $180,000 = $22,908,000`
   - If `K_PUT ≤ S_T ≤ K_CALL`: proceeds = `S_T × FC_AMT − Net_Cost`
   - If `S_T > K_CALL`: proceeds capped at `K_CALL × FC_AMT − Net_Cost = $24,000,000 − $180,000 = $23,820,000`

---

## 5. Outputs

| Output | Description |
|--------|-------------|
| **Section B – Forward Proceeds** | Single locked-in USD amount: $21,870,000 |
| **Section C – MM Hedge Proceeds** | Step-by-step chain yielding $23,484,118; includes parity check vs. forward |
| **Section D – Option Costs & Net Proceeds** | Total put cost, total call premium, net collar cost, and put net proceeds at current spot |
| **Section E – Sensitivity Table** | 11-row table: `S_T` varies from 0.95× to 1.05× S0 in 1% steps; columns show USD proceeds for all five strategies (Unhedged, Forward, MM, Put, Collar) |
| **Section F – Summary Output** | Strategy comparison table: USD proceeds, delta vs. unhedged in USD and %, and qualitative tradeoff note; CFO recommendation cell reserved for Stage 4 |

---

## 6. Model Review — What Worked & What to Improve

### What Worked

- **Named ranges throughout Section A** make every formula auditable and self-documenting. Any downstream formula that references `FC_AMT` or `S0` is immediately interpretable.
- **The sensitivity table (Section E)** correctly parameterizes `S_T` as a multiplier on `S0`, producing a clean ±5% scenario range that supports visual comparison across all strategies.
- **The Notes & Assumptions sheet** provides full source attribution and flags the CIP discrepancy explicitly, which is appropriate practice for a model that will be reviewed by a CFO.
- **Collar payoff logic** correctly applies the three-region piecewise structure (floor, participation, cap) in the sensitivity table.

### What to Improve

- **CIP reconciliation:** The forward rate `F0 = 1.0935` is inconsistent with the CIP formula applied to the model's own inputs (`F0_CIP ≈ 1.1944`). The improved model should either (a) compute `F0` endogenously from `S0`, `R_USD`, `R_EUR`, and `T_DAYS`, or (b) accept a desk-quoted forward as an independent input and report the CIP-implied rate alongside it for the analyst to compare. This discrepancy currently causes the parity check to show a ~$1.6M gap, which undermines the MM hedge analysis.
- **Day-count convention:** Adopt ACT/360 for USD money market calculations and ACT/365 for EUR, consistent with interbank convention. This requires storing `T_DAYS` and computing the appropriate fraction per currency.
- **Transaction cost layer:** Add a dedicated inputs block for bid-ask spread (in pips) and broker fee (as a % or flat USD). These should flow through each strategy's net proceeds automatically.
- **Option premium sourcing:** Replace the flat $0.019 and $0.010 estimates with a Black-Scholes or Garman-Kohlhagen calculation driven by an implied volatility input (`SIGMA`). This makes the option analysis reproducible without a live desk quote.
- **Sensitivity chart:** The model does not yet include a line chart visualizing Section E. A chart overlaying all five strategies vs. `S_T` should be added and labeled as a primary deliverable for CFO presentation.
- **Named range for `F0`:** In the current model, `F0 = 1.0935` is entered as a hard-coded value. It should be promoted to a formal named input cell (or computed via CIP) so that scenario analysis on the forward rate is possible.

---

## 7. Sensitivity Plan

The sensitivity table (Section E) constructs 11 EUR/USD scenarios by multiplying the inception spot rate `S0 = 1.1544` by a multiplier ranging from 0.95 to 1.05 in steps of 0.01, producing `S_T` values from approximately 1.0967 to 1.2121 USD/EUR. This ±5% band captures the realistic near-term trading range based on the observed 52-week historical range of approximately ±6%.

For each `S_T` scenario, the table computes USD proceeds under all five strategies. The most informative comparisons are:

- **Forward vs. Unhedged:** Quantifies the opportunity cost of locking in when EUR strengthens, and the protection value when EUR weakens.
- **Put vs. Unhedged:** Isolates the cost of the premium floor; below `K_PUT`, the put outperforms; above, it underperforms by exactly the premium.
- **Collar vs. Put:** Shows the premium saving from selling the call, at the cost of capping upside above `K_CALL = 1.2000`.

The improved model should render this table as a labeled line chart with `S_T` on the x-axis and USD proceeds on the y-axis, with a vertical reference line at `S_T = S0` and a second line at `S_T = F0`.

---

## 8. Limitations & Next Steps

**Excluded from this model:**

- Dynamic or delta hedging strategies
- Credit and counterparty risk on derivative contracts
- Accounting treatment (ASC 815 / IFRS 9 hedge designation)
- Tax effects on premium payments or realized gains/losses
- Rolling or partial hedge structures
- Stochastic simulation of EUR/USD paths (Monte Carlo)

**How this feeds Stage 4:**

This specification provides the structured blueprint for the Stage 4 AI prompt. The named ranges in Section 2 will be passed directly as variable definitions; the calculation flows in Section 4 will be used to instruct formula construction; and the improvement notes in Section 6 will direct the AI to build the enhanced version rather than replicate the prototype. The explicit output list in Section 5 ensures the AI produces the exact tables, chart, and summary the CFO presentation requires.
