# Stage 4 – Final Analysis & Strategic Recommendation
## FX Receivable Hedge Analysis – EUR/USD

**Author:** Matthew Furusho | Aerospace Division Treasury  
**Date:** April 3, 2026  
**Version:** 1.0 – Stage 4 Final Deliverable  
**Source Model:** `furusho-matthew-stage4-model.xlsx`  
**LLM Assist:** Claude (Anthropic)

---

## A. Exposure Summary

The Aerospace Division holds a confirmed EUR-denominated receivable of **€20,000,000** due from a European buyer on **April 3, 2027** (365 days). At the April 3, 2026 spot rate of **1.1544 USD/EUR**, this receivable carries a current USD equivalent of approximately **$23,088,000**.

### FX Risk

EUR/USD has traded within a 52-week range of approximately 1.0805–1.2134, implying peak-to-trough volatility of roughly 12%. An adverse move to the 52-week low would reduce USD proceeds to approximately $21,610,000 — a **shortfall of ~$1,478,000** versus today's spot equivalent. Because this receivable represents a single-currency, unhedged inflow with no natural USD offset on the balance sheet, it constitutes a material and unmitigated FX risk requiring a structured hedging decision before settlement.

### Business Context

The macro environment elevates this risk. The Federal Reserve holds the upper bound of the Fed Funds rate at 3.75%, while the ECB Deposit Facility sits at 2.00% with potential further divergence. This interest rate differential, historically a reliable driver of EUR/USD, biases the exchange rate toward EUR weakness on a carry basis — consistent with a 1-year forward rate of **1.0935 USD/EUR**, representing a ~5.3% discount to spot. For an aerospace division with USD-denominated operating costs and USD-denominated reporting, locking in cash flow certainty is not merely prudent; it is a fiduciary obligation.

---

## B. Summary of Hedge Outcomes

The following table summarizes USD proceeds under each strategy at the current spot rate (S_T = 1.1544) as the base case:

| Strategy | USD Proceeds | vs. Unhedged (USD) | vs. Unhedged (%) | Key Characteristic |
|---|---|---|---|---|
| Unhedged (at spot S0) | $23,088,000 | — | — | Full upside & downside |
| Forward Contract | $21,870,000 | ($1,218,000) | (5.28%) | Complete certainty; zero premium |
| Money Market Hedge | $23,484,118 | +$396,118 | +1.72% | Replicates forward synthetically |
| Put Option (ATM floor) | $22,708,000 | ($380,000) | (1.65%) | Floor + full upside; costs premium |
| Collar Strategy | $22,908,000 | ($180,000) | (0.78%) | Bounded range; minimal net cost |

> **Note on Money Market vs. Forward Discrepancy:** The Money Market Hedge yields $23,484,118 versus the Forward's $21,870,000 — a difference of ~$1,614,118. This gap signals a CIP inconsistency: the desk-quoted forward rate of 1.0935 does not reconcile with the CIP-implied rate of approximately 1.1944 using the model's own inputs. The MM hedge result is arithmetically correct given the stated rates; the forward rate must be confirmed with a live desk quote before execution.

### Forward Hedge

Locking in $21,870,000 today provides complete cash flow certainty regardless of where EUR/USD settles at maturity. The cost is opportunity cost — if EUR appreciates to 1.20, the firm forgoes up to $2,130,000 in additional proceeds. However, for budget-driven businesses, the ability to plan around a known USD inflow outweighs speculative upside. Zero premium, zero optionality.

### Money Market Hedge

The MMH replicates a forward contract synthetically by borrowing the present value of the receivable in EUR (€19,607,843), converting at spot, and investing USD for one year. At the stated rates, this yields $23,484,118 — superior to the desk-quoted forward. However, this result depends on the CIP discrepancy noted above. In practice, the MMH also encumbers the balance sheet (requires a EUR credit facility), introduces counterparty risk through the borrowing relationship, and demands treasury infrastructure to execute cleanly. Parity with the forward should be assumed once rates are reconciled.

### Put Option Hedge

Purchasing an ATM put at K_PUT = 1.1544 for $0.019/EUR ($380,000 total) establishes a USD floor of $22,708,000 while retaining full upside participation if EUR strengthens. This is the most flexible strategy: the firm captures appreciation above 1.1544 without limit, and accepts the premium as the cost of optionality. If EUR trades at or above 1.1707 at maturity (the breakeven accounting for the premium), the put outperforms the unhedged position on a risk-adjusted basis.

### Collar Strategy

Combining a long put (1.1544 strike) with a short call (1.2000 strike) reduces the net premium cost to $180,000 (vs. $380,000 for the standalone put). Proceeds are bounded between $22,908,000 (floor) and $23,820,000 (cap). The collar is optimal when management wants meaningful downside protection at low out-of-pocket cost and is willing to accept a ceiling on upside. Given the current rate differential bias toward EUR weakness, capping upside at 1.2000 is arguably a modest concession.

### No Hedge (Baseline)

Leaving the exposure unhedged provides full sensitivity to EUR/USD at maturity. At spot (1.1544), proceeds are $23,088,000. At the 52-week low (1.0805), proceeds fall to $21,610,000. At the 52-week high (1.2134), they rise to $24,268,000. This is not a strategy; it is a posture. For a material single-currency receivable in a volatile macro environment, "no hedge" is an active decision to bear risk that could otherwise be transferred.

---

## C. Sensitivity Interpretation

The sensitivity table models USD proceeds across eleven EUR/USD scenarios from 0.95× to 1.05× S0 (1.0967 to 1.2121):

| S_T Mult. | S_T (USD/EUR) | Unhedged | Forward | MM Hedge | Put Net | Collar Net |
|---|---|---|---|---|---|---|
| 0.95 | 1.0967 | $21,933,600 | $21,870,000 | $23,484,118 | $22,708,000 | $22,908,000 |
| 0.96 | 1.1082 | $22,164,480 | $21,870,000 | $23,484,118 | $22,708,000 | $22,908,000 |
| 0.97 | 1.1198 | $22,395,360 | $21,870,000 | $23,484,118 | $22,708,000 | $22,908,000 |
| 0.98 | 1.1313 | $22,626,240 | $21,870,000 | $23,484,118 | $22,708,000 | $22,908,000 |
| 0.99 | 1.1429 | $22,857,120 | $21,870,000 | $23,484,118 | $22,708,000 | $22,908,000 |
| 1.00 | 1.1544 | $23,088,000 | $21,870,000 | $23,484,118 | $22,708,000 | $22,908,000 |
| 1.01 | 1.1659 | $23,318,880 | $21,870,000 | $23,484,118 | $22,938,880 | $23,138,880 |
| 1.02 | 1.1775 | $23,549,760 | $21,870,000 | $23,484,118 | $23,169,760 | $23,369,760 |
| 1.03 | 1.1890 | $23,780,640 | $21,870,000 | $23,484,118 | $23,400,640 | $23,600,640 |
| 1.04 | 1.2006 | $24,011,520 | $21,870,000 | $23,484,118 | $23,631,520 | $23,820,000 |
| 1.05 | 1.2121 | $24,242,400 | $21,870,000 | $23,484,118 | $23,862,400 | $23,820,000 |

### EUR Depreciation Scenarios (S_T < S0)

When EUR weakens below spot, the Forward Hedge and Put/Collar floors dominate. The unhedged position underperforms by up to $1,154,400 at the −5% scenario versus the put floor. The forward delivers a fixed $21,870,000 regardless of spot movement — but notably, the forward trails even the put floor ($22,708,000) in all depreciation scenarios. This reflects the CIP gap: in a properly reconciled model, forward and MM proceeds would converge. The current model's forward rate of 1.0935 is significantly below CIP-implied (1.1944), making the put floor and collar more attractive on a pure proceeds basis.

### EUR Appreciation Scenarios (S_T > S0)

When EUR strengthens, the unhedged position outperforms all hedged strategies above the S0 crossover. The put begins participating in EUR gains above 1.1544, reaching $23,862,400 at +5% — nearly matching the unhedged position net of the premium cost. The collar caps at $23,820,000 for all S_T above 1.2000 (≈+3.9%), forgoing further upside. The forward remains fixed at $21,870,000 regardless, representing pure opportunity cost in appreciation scenarios.

The sensitivity analysis confirms: **the put and collar provide the best risk-adjusted outcomes across both tails**, with the collar winning on cost efficiency in most scenarios.

---

## D. Strategic Recommendation

**Recommended Strategy: Collar (Long Put at 1.1544 / Short Call at 1.2000)**

The collar strategy is recommended as the primary hedge for the €20,000,000 receivable, with the put option as a fallback if management requires full upside participation.

**Rationale from the model:**

1. The collar establishes a hard USD floor of $22,908,000 — protecting $1,298,000 of proceeds versus the worst 52-week scenario — at a net premium of only $180,000 (vs. $380,000 for the standalone put).
2. The short call cap of 1.2000 is materially above current spot (1.1544) and above the 12-month average trading range center. Giving up upside above 1.2000 is a low-probability concession.
3. Unlike the forward, the collar preserves approximately $1,950,000 of upside participation between spot and the cap — aligning hedged outcomes with favorable macro scenarios without bearing full FX risk.
4. Unlike the MMH, the collar requires no balance sheet encumbrance and no EUR credit facility.

**If the forward rate can be confirmed at approximately CIP-parity (~1.1944 USD/EUR)**, the analysis changes materially — a forward at 1.1944 would lock in $23,888,000, outperforming every other strategy in all depreciation scenarios and nearly matching the unhedged position at spot. In that case, the Forward Contract becomes the dominant recommendation.

---

## E. Executive Justification

**Cash Flow Stability:** The collar guarantees a minimum USD inflow of $22,908,000, enabling finance to commit this revenue to the FY2027 operating budget with confidence. A $180,000 net premium is 0.78% of the notional — a modest insurance cost for a material single-payment exposure.

**Budget Certainty:** The aerospace business operates on multi-year program economics. FX volatility in a single receivable of this size can shift quarterly earnings meaningfully. The collar compresses the range of outcomes to [$22,908,000 – $23,820,000], a band of $912,000 — versus an unhedged range of [$21,610,000 – $24,268,000+] over the 52-week implied swing. Narrowing this variance reduces forecast risk for the CFO and the board.

**Liquidity Impact:** The net collar premium of $180,000 is payable at inception and is non-refundable. This is a modest use of operating cash relative to the size of the exposure. The standalone put requires $380,000 upfront; the forward requires no premium but forfeits $1,218,000 of proceeds versus spot. On a cash basis, the collar is the most efficient hedge.

**Optionality Value:** Unlike the forward, which eliminates all EUR upside, the collar retains meaningful participation between 1.1544 and 1.2000. At current EUR/USD, this range captures a potential additional $1,820,000 above the floor — fully available to the firm without additional cost.

**Premium Costs:** The $180,000 net collar premium should be classified as a hedging cost in the income statement (or deferred and matched against the underlying revenue at settlement, subject to hedge accounting designation under ASC 815 / IFRS 9).

**Accounting Consideration (Optional):** If the collar is designated as a cash flow hedge under ASC 815, changes in fair value of the hedging instrument flow through OCI rather than P&L until the receivable settles. This reduces earnings volatility during the hedging period and simplifies the hedge performance documentation. Treasury should evaluate formal hedge designation with the accounting team prior to execution.

---

## F. Structured AI Prompt

---

### Appendix: AI Prompt – FX Hedge Spreadsheet Generator

```
# GOAL
Generate a complete, professional Excel workbook (.xlsx) that models and compares five EUR/USD
FX hedging strategies for a EUR-denominated receivable. The model must be fully formula-driven,
use named ranges throughout, apply color coding per the specification below, and include a
sensitivity table and summary output section suitable for CFO presentation.

# INPUT VARIABLES
Use these exact values. Do not infer, default, or substitute any variable.

FC_AMT       = 20,000,000   (EUR receivable notional)
S0           = 1.1544       (Spot rate at inception, USD per EUR)
F0           = 1.0935       (1-year forward rate, USD per EUR – desk-quoted; flag CIP gap)
R_USD        = 0.0375       (USD interest rate, annual simple, Fed Funds upper bound)
R_EUR        = 0.0200       (EUR interest rate, annual simple, ECB Deposit Facility)
T_DAYS       = 365          (Days to settlement, Apr 3 2026 → Apr 3 2027)
K_PUT        = 1.1544       (Put option strike, ATM = S0)
PREM_PUT     = 0.019        (Put premium per EUR, USD)
K_CALL       = 1.2000       (Call option strike, OTM collar leg)
PREM_CALL    = 0.010        (Call premium per EUR, USD – collar: sell this call)
F0_CIP       = S0 * (1 + R_USD) / (1 + R_EUR)   [Compute and display for parity check]

# NAMED RANGES
Define all ten variables above as named ranges in the workbook (Formulas > Name Manager).
Named ranges must exactly match the symbols listed above: FC_AMT, S0, F0, R_USD, R_EUR,
T_DAYS, K_PUT, PREM_PUT, K_CALL, PREM_CALL.

All downstream formulas must reference named ranges, not hardcoded values.

# COLOR CODING
Yellow fill   → All editable input cells (Section A)
Blue fill     → Assumption cells (rates, premiums, strikes sourced externally)
Green fill    → Formula output cells
Gray fill     → Final summary output cells (Section F)
Black text    → All formula cells
Blue text     → All hardcoded numeric inputs

# WORKBOOK STRUCTURE

## Sheet 1: FX Hedge Model

### SECTION A — INPUTS
10-row table with columns: Parameter | Symbol | Value | Units | Source / Notes
List all 10 named ranges. Mark Value column cells Yellow (editable inputs).
Add a computed row: CIP-Implied F0 = S0*(1+R_USD)/(1+R_EUR) in Green.

### SECTION B — FORWARD CONTRACT HEDGE
Two-row block:
  Row 1: Agreed forward rate today = F0
  Row 2 (Output, Green): USD Proceeds = FC_AMT * F0 = $21,870,000

### SECTION C — MONEY MARKET HEDGE
Four-step chain:
  Step 1: EUR to borrow = FC_AMT / (1 + R_EUR * T_DAYS/365)   → €19,607,843
  Step 2: Convert at spot = Step1 * S0                         → $22,635,294
  Step 3: Invest USD for T_DAYS = Step2 * (1 + R_USD*T_DAYS/365) → $23,484,118
  Step 4 (Output, Green): USD Proceeds = Step 3
  Parity Check row: = MM_Proceeds - Forward_Proceeds
    Flag with ⚠ if abs(difference) > 10,000. Add note: "CIP reconciliation required."

### SECTION D — OPTION HEDGES
Rows:
  Total Put Premium (USD) = PREM_PUT * FC_AMT               → $380,000
  Total Call Premium (USD) = PREM_CALL * FC_AMT             → $200,000
  Net Collar Cost (USD) = Put_Premium - Call_Premium         → $180,000
  Put Net Proceeds at S0 = MAX(S0, K_PUT)*FC_AMT - Put_Premium_Total  → $22,708,000
  Collar Floor Proceeds = K_PUT*FC_AMT - Net_Collar_Cost     → $22,908,000
  Collar Cap Proceeds = K_CALL*FC_AMT - Net_Collar_Cost      → $23,820,000

### SECTION E — SENSITIVITY TABLE
11 rows. S_T Multiplier from 0.95 to 1.05 in steps of 0.01.
Columns: S_T_Mult | S_T (=S_T_Mult*S0) | Unhedged | Forward | MM Hedge | Put Net | Collar Net

Formulas:
  Unhedged        = S_T * FC_AMT
  Forward         = F0 * FC_AMT   [constant across all rows]
  MM Hedge        = FC_AMT/(1+R_EUR*T_DAYS/365)*S0*(1+R_USD*T_DAYS/365)  [constant]
  Put Net         = MAX(S_T, K_PUT)*FC_AMT - PREM_PUT*FC_AMT
  Collar Net      = MIN(MAX(S_T, K_PUT), K_CALL)*FC_AMT - (PREM_PUT - PREM_CALL)*FC_AMT

Highlight the S_T = S0 row (multiplier = 1.00) in light blue fill.
Add a line chart: X-axis = S_T, Y-axis = USD Proceeds, one series per strategy (5 lines).
Include vertical reference lines (or data labels) at S_T = S0 and S_T = F0.

### SECTION F — SUMMARY OUTPUT (Gray fill)
6-row table: Strategy | USD Proceeds at S0 | vs Unhedged USD | vs Unhedged % | Key Tradeoff
Strategies: Unhedged | Forward | Money Market | Put Option | Collar
Include a CFO Recommendation row (manually completed by analyst).

## Sheet 2: Notes & Assumptions
Document all data sources, rate conventions, simplifications, and the CIP discrepancy.
Include model version, author, and analysis date.

# MODEL LOGIC RULES
- All formulas must use named ranges, not hardcoded numbers.
- Simple interest only: Rate * (T_DAYS / 365). No compounding.
- Option style: European. No Black-Scholes. Premiums are point estimates.
- Transaction costs: excluded (mid-market rates).
- Bid-ask: excluded.
- Credit risk: not modeled.
- The forward rate F0 = 1.0935 is desk-quoted. Display CIP-implied F0 alongside it
  and flag any gap > 0.05 with a warning cell.

# VERIFICATION CHECKS
1. Forward Proceeds: FC_AMT * F0 = $21,870,000 exactly.
2. MM Step 1 × S0 × (1 + R_USD) = MM Step 3 (chain must close).
3. Parity Check: MM_Proceeds - Forward_Proceeds = difference; label ⚠ if non-trivial.
4. Put floor check: At S_T = K_PUT, Put Net = K_PUT*FC_AMT - PREM_PUT*FC_AMT = $22,708,000.
5. Collar cap check: At S_T = 1.21, Collar Net = K_CALL*FC_AMT - Net_Collar_Cost = $23,820,000.
6. All Section E formulas must update automatically if any Section A input changes.

# FORMATTING REQUIREMENTS
- Font: Arial 10pt throughout.
- Column widths: auto-fit all columns; minimum 12 for numeric columns.
- Number format: $#,##0 for all USD amounts; 0.0000 for rates; 0% for percentages.
- Negative numbers: parentheses (not minus sign).
- Section headers: Bold, 12pt, dark blue fill (#1F3864), white text.
- All inputs in Section A: Yellow fill (#FFFF00).
- Output rows: Green fill (#E2EFDA).
- Summary section (F): Gray fill (#D9D9D9).
- Sensitivity table base row (S_T = S0): Light blue fill (#DEEAF1).

# EXPORT
Save as: furusho-matthew-stage4-model.xlsx
Deliver with zero formula errors. Verify using recalc before final save.
```

---

## Extra Credit: Areas for Further Study & Improvement

### 1. AI Skills & Automation

The structured prompt in Section F demonstrates a critical modern skill: converting domain knowledge into machine-readable instructions that an LLM can execute reproducibly. The next frontier is closing the loop. AI tools like Claude with Code Interpreter access could be configured to pull live EUR/USD rates, forward points, and ECB/Fed rate decisions via market data APIs (Bloomberg, Refinitiv, or open-source alternatives like FRED), and automatically repopulate the Section A inputs before regenerating the full model. Combined with a Monte Carlo extension — simulating thousands of EUR/USD paths using historical or implied volatility — the model could output not just scenario proceeds but probability distributions, VaR estimates, and expected shortfall under each hedge strategy. This would transform a static CFO presentation tool into a live risk dashboard that treasury can refresh with a single prompt.

### 2. Multi-File Reasoning & Model Governance

The three-stage architecture of this project (spec → model → prompt) naturally lends itself to AI-assisted multi-file reasoning. An AI given access to all three files — the Stage 3 spec, the Stage 2 Excel model, and this Stage 4 prompt — could perform automated consistency checks: verifying that named ranges in the spreadsheet match the spec, that sensitivity table logic follows the calculation flow in Section 4.1–4.4, and that the AI prompt in Section F would reproduce the same numbers as the manually built model. This kind of automated cross-file auditing is directly analogous to what financial statement auditors do when tracing from supporting schedules to the primary statements — and it is a capability that firms like Deloitte, KPMG, and major corporate treasury functions are beginning to operationalize using enterprise AI platforms. Version-controlled multi-file packages committed to GitHub represent the enabling infrastructure for this workflow.

### 3. GitHub & Version Control

Committing each stage of this project to GitHub creates a fully auditable, reproducible model lineage. Stage 1 (exposure memo), Stage 2 (Excel model), Stage 3 (technical spec), and Stage 4 (final analysis + AI prompt) each represent a discrete, timestamped artifact that can be reviewed, rolled back, or branched for scenario testing. This workflow mirrors the hedge documentation requirements under ASC 815 and IFRS 9: both standards require that hedge designation documentation exist at or before the hedging relationship is established and that it be preserved for the life of the hedge. A GitHub repository with signed commits provides tamper-evident version history, making it suitable as part of an audit package. For this project specifically, the Stage 3 spec could serve as the hedge designation memorandum; the Stage 2 and 4 models as the quantitative support; and the GitHub commit history as the evidence of preparation date and authorship — all three of which auditors and regulators require.

---

*End of Stage 4 Final Analysis — Matthew Furusho | Aerospace Division Treasury | April 3, 2026*
