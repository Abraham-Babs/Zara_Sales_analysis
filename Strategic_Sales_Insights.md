# Strategic Sales Insights: Commercial & Data Integrity Audit

**To:** Merchandising & Commercial Strategy Leadership  
**From:** Senior Retail Business Analyst  
**Subject:** Data Integrity Audit & Strategic Review of Zara Sales Model  

---

## 1. Executive Summary

We conducted a commercial and statistical audit of the Zara sales dataset to evaluate product performance drivers across price points, promotional activity, garment attributes, and supplier origin.

Our primary finding is that **the underlying dataset is synthetic and should not be used for commercial decision-making**. While it mimics real catalog text and product URLs, the numerical sales figures and retail attributes are generated artifacts.

Key takeaways for leadership:

1. **False Strategic Levers:** Factors previously thought to drive sales—such as near-shoring origin and product description keywords—have no statistically significant relationship with sales volume once proper controls are applied (p > 0.05).
2. **The Promotion Volume Trap:** Although promotions show a 1.59x (+58.9%) increase in unit volume, optimizing for volume without visibility into gross margins, discount depth, or return rates presents substantial margin risk.
3. **Synthetic Regularity:** Category-level regressions across shoes, jackets, sweaters, and jeans yield nearly identical price elasticity coefficients (-11% to -12%), which indicates a formulaic generation process rather than real consumer market behavior.

---

## 2. Data Integrity Audit: Four Critical Red Flags

Before investing capital based on an analytical model, the underlying data must pass a basic retail operational audit. Four structural issues were identified:

| Audit Check | Observed Dataset Behavior | Real Retail Operational Reality | Impact on Strategy |
| :--- | :--- | :--- | :--- |
| **Volume Distribution** | Artificially bounded between 518 and 1,940 units (mean: 1,097; normal-like curve). | Real SKU sales follow a Pareto distribution (top 20% of SKUs generate 80% of volume; heavy zero-sales tail). | Modeling results cannot be generalized to real store inventory or replenishment planning. |
| **Merchandising Terminology** | Placement is categorized as "Aisle", "End-cap", and "Front of Store". | Fast-fashion uses visual merchandising: collection walls, mannequins, and central tables. | Confirms supermarket grocery taxonomy was mapped onto an apparel catalog. |
| **Origin Variance** | Mean sales volume across 12 countries is essentially uniform (1,095 to 1,106). ANOVA: F = 1.60, p = 0.091. | Near-shoring (Spain, Portugal, Morocco) provides turnaround speed (2-3 weeks), not consumer purchasing preference. | The claimed "+3% lift from near-shoring" is random sampling variation, not a consumer trend. |
| **Unit Economics** | No Cost of Goods Sold (COGS), discount depth, or return rates. | Retail viability depends on net margin dollars, markdown timing, and return handling costs. | High-volume promotions cannot be confirmed as profitable without margin data. |

![Forensic Data Audit](assets/forensic_data_audit.png)

---

## 3. Econometric Findings (Negative Binomial GLM)

Using a Negative Binomial Generalized Linear Model with a log-link function, we evaluated the structural multipliers (Incident Rate Ratios, IRR):

### Verified Effects
* **Promotional Lift (IRR = 1.589, p < 0.001):** Promoted products move approximately 58.9% more units than unpromoted catalog items.
* **Women's Section Baseline (IRR = 1.106, p < 0.001):** Products in the Women's division maintain a 10.6% structural volume premium over Men's.
* **Price Elasticity (IRR = 0.887, p < 0.001):** Higher price tiers experience volume reductions of approximately 11.3% per log-dollar increase.

### Disproven Signals (Statistical Noise)
* **Description Keywords:** Keywords extracted from product descriptions (such as "technical" or "rib") showed no meaningful impact (IRR = 1.002 to 1.011, p > 0.80). Product copy does not dictate retail sales volume.
* **Near-Shoring Origin:** Sourcing from Spain, Portugal, Morocco, or Turkey showed an IRR of 1.001 (p = 0.932). Sourcing location has no direct consumer pull effect in this data.

![Strategic Sales Drivers](assets/strategic_sales_drivers.png)

---

## 4. The Promotion Fallacy: Volume vs. Profit

A common mistake in retail analytics is treating unit volume lift as an unmitigated success. In fast-fashion operations, unmeasured promotional volume often destroys profitability:

### Illustrative Economics
* **Full-Price Scenario:** An item sold at $50.00 with a 60% gross margin yields $30.00 in gross margin per unit.
* **Promotional Scenario (30% Discount):** The same item sold at $35.00 with a fixed $20.00 cost yields $15.00 in gross margin per unit (a 50% drop per unit).
* **Breakeven Requirement:** Unit volume must increase by 100% just to maintain the same total margin dollars. A 58.9% lift leaves the business with roughly 20% fewer gross profit dollars.
* **Return Logistics:** Apparel e-commerce return rates typically range from 20% to 35%. Promoted items frequently suffer higher return rates, incurring $8 to $15 per unit in return shipping, inspection, and repackaging costs.

![Promotional Lift](assets/eda_promotion_lift.png)

---

## 5. Recommendations for Commercial Strategy

### 1. Establish Pre-Model Data Quality Gates
Before approving any commercial forecasting model, analytics teams must verify:
* Skewness and distribution shape match retail power laws.
* Merchandising attributes reflect actual store and site taxonomy.
* Hypothesized supplier advantages are tested against basic ANOVA significance thresholds before presentation to leadership.

### 2. Transition from Static Snapshots to Point-of-Sale Time Series
To understand Zara's real competitive advantages, analytical infrastructure must incorporate:
* **Weekly Transaction Logs:** Measure sales velocity (units per store per week) rather than lifetime SKU totals.
* **Inventory Stockout Data:** Differentiate low demand from inventory stockouts.
* **Speed to Market:** Track cycle time from design sign-off to first store delivery.

### 3. Replace Volume Metrics with Margin KPIs
Shift commercial performance reviews away from raw units sold toward:
* **Gross Margin Return on Investment (GMROI).**
* **Full-Price Sell-Through Rate (targeting 85%+).**
* **Net Markdown Loss per Category.**
