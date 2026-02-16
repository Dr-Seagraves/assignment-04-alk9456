# Assignment 04 Interpretation Memo

**Student Name:** Alec Ko
**Date:** 02/15/26
**Assignment:** REIT Annual Returns and Predictors (Simple Linear Regression)

---

## 1. Regression Overview

You estimated **three** simple OLS regressions of REIT *annual* returns on different predictors:

| Model | Y Variable | X Variable | Interpretation Focus |
|-------|------------|------------|----------------------|
| 1 | ret (annual) | div12m_me | Dividend yield |
| 2 | ret (annual) | prime_rate | Interest rate sensitivity |
| 3 | ret (annual) | ffo_at_reit | FFO to assets (fundamental performance) |

For each model, summarize the key results in the sections below.

---Higher dividend yields and prime rates are associated with lower REIT returns
FFO/assets ratio shows a positive but insignificant relationship with returns
Prime rate has the strongest explanatory power (highest R²) among the three predictors

## 2. Coefficient Comparison (All Three Regressions)

**Model 1: ret ~ div12m_me**
- Intercept (β₀): [.1082] (SE: [.0060], p-value: [.0000])
- Slope (β₁): [-.0687] (SE: [.0325], p-value: [.0346])
- R²: [.0018] | N: [2527]

**Model 2: ret ~ prime_rate**
- Intercept (β₀): [.1998] (SE: [.0158], p-value: [.0000])
- Slope (β₁): [-.0194] (SE: [.0030], p-value: [.0000])
- R²: [.0164] | N: [2527]

**Model 3: ret ~ ffo_at_reit**
- Intercept (β₀): [.0973] (SE: [.0092], p-value: [.3093])
- Slope (β₁): [.5770] (SE: [.5675], p-value: [.3093])
- R²: [.0004] | N: [2518]

*Note: Model 3 may have fewer observations if ffo_at_reit has missing values; statsmodels drops those rows.*

---

## 3. Slope Interpretation (Economic Units)

**Dividend Yield (div12m_me):**
- A 1 percentage point increase in dividend yield (12-month dividends / market equity) is associated with a -0.0687 percentage point change in annual return.
- The p-value (0.0346) is less than the 5% significance level, so the slope is considered statistically significant.

**Prime Loan Rate (prime_rate):**
- A 1 percentage point increase in the year-end prime rate is associated with a -0.0194 percentage point change in annual return.
- Higher rates are associated with lower returns, and the relationship is statistically significant (p < 0.001).

**FFO to Assets (ffo_at_reit):**
- A 1 unit increase in FFO/Assets (fundamental performance) is associated with a 0.5770 percentage point change in annual return.
- The slope is positive but not statistically significant (p = 0.3093).

---

## 4. Statistical Significance

For each slope, at the 5% significance level:
- **div12m_me:** Significant — the slope is negative and statistically significant (p = 0.0346)
- **prime_rate:** Significant — the slope is negative and statistically significant (p < 0.001)
- **ffo_at_reit:** Not significant — the slope is positive but not statistically significant (p = 0.3093).

**Which predictor has the strongest statistical evidence of a relationship with annual returns?** The prime_rate has the strongest statistical evidence, with the lowest p-value and highest t-statistic among the three predictors.

---

## 5. Model Fit (R-squared)

Compare R² across the three models:
- The prime_rate predictor explains the most variation in annual returns with an R² of 0.0164. The R² values are generally very low across all three models (ranging from 0.0004 to 0.0164), indicating that these individual predictors explain very little of the total variation in REIT annual returns. This suggests that other unmeasured factors are the primary drivers of REIT returns, such as market-wide economic conditions, sector-specific factors, or firm-specific characteristics not captured by these three variables.

---

## 6. Omitted Variables

By using only one predictor at a time, we might be omitting:
- **Market risk (beta):** REITs with higher systematic risk may have different returns, and beta might be correlated with dividend yields or interest rates
- **Firm size (market capitalization):** Larger REITs may behave differently than smaller ones, potentially correlated with FFO/assets ratios
- **Economic conditions (GDP growth, unemployment):** Broader macroeconomic factors that affect all REITs but vary by time period
- **REIT sector/subtype:** Different property types (office, retail, residential) may have different sensitivities to interest rates and fundamentals

**Potential bias:** If omitted variables are correlated with both the X variable and ret, our slope estimates may be biased. For example, if higher beta firms tend to have lower dividend yields and also lower returns, this could bias the dividend yield coefficient toward zero (attenuation bias). Similarly, time-varying economic conditions could affect both interest rates and REIT returns, potentially confounding the prime rate relationship.

---

## 7. Summary and Next Steps

**Key Takeaway:**
[2-3 sentences summarizing which predictor(s) show the strongest relationship with REIT annual returns and whether the evidence is consistent with economic theory] Among the three predictors examined, the prime loan rate shows the strongest statistical relationship with REIT annual returns.Highher interest rates are associated with lower returns. This is consistent with economic theory,  higher borrowing costs can reduce REIT by making real estate investments less appealing.  

**What we would do next:**


---

## Reproducibility Checklist
- [x] Script runs end-to-end without errors
- [x] Regression output saved to `Results/regression_div12m_me.txt`, `regression_prime_rate.txt`, `regression_ffo_at_reit.txt`
- [x] Scatter plots saved to `Results/scatter_div12m_me.png`, `scatter_prime_rate.png`, `scatter_ffo_at_reit.png`
- [x] Report accurately reflects regression results
- [x] All interpretations are in economic units (not just statistical jargon)
