# Macroeconomic Consequences of Humanitarian Aid Shocks in the Horn of Africa

---

## Abstract
This study investigates the macroeconomic impact of the 2025 withdrawal of United States humanitarian aid on staple food prices (maize and sorghum) in the Horn of Africa (Somalia and Ethiopia), using Kenya as a stable control group. By combining an Econometric Difference-in-Differences (DiD) framework with Ensemble Machine Learning (Random Forest and Gradient Boosting), this project quantifies the causal effect of aid shocks and identifies the long-term structural drivers of regional retail food prices. Retail prices were systematically standardized to USD per kilogram to eliminate local currency and unit distortions. The empirical results reveal that the abrupt contraction of US aid did not trigger an immediate, linear retail price spike ($\beta = +0.0270\text{ USD/KG}, p = 0.627$). Machine Learning algorithms validate that retail market prices are fundamentally driven by local agricultural harvests and continuous institutional aid flows rather than immediate market-clearing price shocks, demonstrating that aid cuts primarily destroy household purchasing power rather than inflating headline store prices.

---

## 1. Introduction
At Sabanci University, I am pursuing Data Science and Economics majors, supported by a minor in Sustainability. My long-term aspiration is to contribute to global organizations such as the United Nations and the World Bank, focusing on economic development, humanitarian resilience, and food security in underdeveloped regions—particularly in Africa. In the summer of 2024, I spent 50 days in Tunisia as a volunteer English tutor, an immersive experience that deeply solidified my dedication to African development.

This academic background motivated me to examine one of the most critical current challenges in global development: the sudden withdrawal of the United States from international humanitarian assistance. I recognized the urgency of this topic through my course **MGMT310 - Humanitarian Aid and Management**, under the mentorship of Dr. Asma Nairi. My primary research question is: *Does the abrupt withdrawal of the US—the world's predominant humanitarian donor—trigger immediate local retail food price spikes in the Horn of Africa, or can secondary donors like the European Union effectively substitute this funding gap?*

A concise contextual overview of this humanitarian challenge is documented by [DW Africa on YouTube](https://www.youtube.com/watch?v=z0uWENrLpDo).

---

## 2. Methodology

### 2.1 Data Collection
To construct a robust monthly panel dataset spanning 2020 to 2026 (72 months per country), three primary datasets were curated and merged:
* **WFP (World Food Programme):** Monthly retail prices for primary staple cereals (white/red maize and sorghum).
* **UN FTS (Financial Tracking Service):** Annual humanitarian funding volumes (Million USD) from the US and EU.
* **FAOSTAT:** Annual regional agricultural crop production (Million Tonnes) to control for supply-side shifts.
* **Custom Enrichment:** A continuous **Political Instability Index** (scaled 0.0 to 1.0) synthesized from regional conflict intensity and electoral shocks to isolate non-economic disturbances.

### 2.2 Data Cleaning and Unit Normalization
To resolve severe unit discrepancies (e.g., Ethiopian 100-KG quintals, Kenyan 90-KG wholesale bags, and Somali Shilling market parity rates), all price observations were systematically converted into a single unified metric: **USD per kilogram ($/KG)**.

| Feature | Data Type | Description | Role in Model |
| :--- | :---: | :--- | :--- |
| 🎯 **`usdprice`** | Continuous | Monthly staple food price per KG (USD). | **Target Variable** |
| 🇺🇸 **`US_Aid_M`** | Continuous | Estimated monthly US humanitarian funding (Million USD). | Core Predictor |
| 🇪🇺 **`EU_Aid_M`** | Continuous | Estimated monthly EU humanitarian funding (Million USD). | Control Variable |
| 🌾 **`Crop_Production_M_Tonnes`** | Continuous | Monthly regional crop production volume (Million Tonnes). | Control Variable |
| ⚠️ **`Political_Instability`** | Float (0-1) | Synthesized proxy metric for regional conflict dynamics. | Control Variable |
| 🚩 **`Treatment`** | Binary (0/1) | 1 = Somalia/Ethiopia (Vulnerable), 0 = Kenya (Control Baseline). | DiD Indicator |
| ⏱️ **`Post_Shock`** | Binary (0/1) | 1 = Year 2025 and beyond (Post-US Aid Cut Era). | DiD Indicator |
| ⚡ **`DiD`** | Binary (0/1) | Interaction term (`Treatment` $\times$ `Post_Shock`). | **Core Causal Variable** |

---

## 3. Exploratory Data Analysis (EDA)

Exploratory Data Analysis was conducted to identify price distributions, donor substitution dynamics, and seasonal lean-period cyclicality.

### 📈 3.1 Key EDA Visual Insights

| Observation Theme | Data Findings | Economic Implication |
| :--- | :--- | :--- |
| **Price Distributions** | Prices across Somalia and Ethiopia exhibited wide dispersion ($0.30–$1.20/KG) with heavy right-skewed tails relative to Kenya's narrow density ($0.38–$0.77/KG). | Treatment economies experience substantial structural price volatility during climate and political shocks. |
| **Donor Substitution** | EU aid remained stable at ~$90–$110M annually, failing to scale up against the US contraction from ~$1.3B to ~$200M. | Incomplete institutional substitution: secondary donors cannot absorb sudden superpower funding withdrawals. |
| **Seasonality & Yields** | Prices peaked cyclically during pre-harvest lean seasons (June–August) and showed a strong negative correlation with crop yields ($r = -0.54$). | Physical harvest volume remains the primary anchor of regional food price formation. |

---

## 4. Statistical Modeling & Predictive Analytics

### 📉 4.1 Econometric Approach: Difference-in-Differences (DiD)
**Model:** Ordinary Least Squares (OLS) Regression with Clustered Standard Errors  
**Objective:** Isolate the net causal treatment effect of the 2025 US humanitarian aid withdrawal on local retail prices.

$$\text{usdprice}_{it} = \beta_0 + \beta_1 \text{Treatment}_i + \beta_2 \text{Post\_Shock}_t + \beta_3 (\text{Treatment}_i \times \text{Post\_Shock}_t) + \mathbf{X}_{it}'\gamma + \varepsilon_{it}$$

* **DiD Interaction Coefficient ($\beta_3$):** +$0.0270 USD/KG
* **Standard Error:** 0.056
* **$p$-value:** 0.627
* **Overall Model Fit:** $R^2 = 0.586$ ($F\text{-statistic} = 42.80, p < 0.001$)

### 4.2 Hypothesis Testing & Null Result Interpretation
* $H_0$: The withdrawal of US humanitarian aid has no significant effect on staple food retail prices in the treatment group ($\beta_3 = 0$).
* $H_1$: The withdrawal of US humanitarian aid significantly increases staple food retail prices in the treatment group ($\beta_3 \neq 0$).

**Conclusion:** At the $\alpha = 0.05$ threshold, we **fail to reject the null hypothesis ($p = 0.627$)**. 

Rather than indicating research failure, this **Null Finding** reveals a critical economic reality:
1. **Household Entitlement vs. Market Prices:** In-kind food aid and vouchers operate largely outside formal commercial trade channels. Aid cuts do not immediately cause open-market retail hyperinflation; instead, they destroy household purchasing power and food access directly.
2. **Supply-Side Anchoring:** Local agricultural yields exert a strong, statistically significant downward pressure on prices ($\beta = -0.1738, p < 0.001$), proving that domestic production dominates external aid flows in determining retail pricing.
3. **Institutional Buffer:** Persistent EU assistance ($\beta = 0.0810, p < 0.001$) provided vital liquidity that prevented an outright structural collapse in local food distribution networks.

---

### 🤖 4.3 Machine Learning Approach: Predictive Analytics
**Algorithms:** Random Forest Regressor & Gradient Boosting Regressor  
**Validation:** 5-Fold Cross-Validation  
**Objective:** Capture non-linear market patterns and evaluate feature importance.

| Metric | Random Forest Regressor | Gradient Boosting Regressor |
| :--- | :---: | :---: |
| **Mean $R^2$ (Cross-Validated)** | **82.4% (± 5.1%)** | **82.3% (± 4.8%)** |
| **Mean RMSE** | **$0.084 USD/KG** | **$0.085 USD/KG** |

**Feature Importance Hierarchy:**
1. **`EU_Aid_M` (~50.5%):** High predictive power due to continuous monthly allocation patterns tracking baseline market risk.
2. **`Crop_Production_M_Tonnes` (~41.2%):** Primary physical determinant of food availability and price levels.
3. **`US_Aid_M` (~5.6%) & `Political_Instability` (~2.3%):** Secondary long-term price variance drivers.
4. **`DiD` / `Post_Shock` (~0.0%):** Tree-based algorithms optimize overall variance across all 72 months, naturally deprioritizing binary step-functions relative to continuous monthly variables.

---

## 5. Discussion & Key Findings

1. **Prediction vs. Causality Synergy:** While the DiD econometric model isolates the specific policy shock, Machine Learning explains **82.4% of total price variance**. This confirms that staple food prices are predominantly governed by agricultural yields and ongoing aid flows.
2. **Aid Shock Manifestation:** The withdrawal of foreign aid operates as an **access crisis** (collapse in purchasing power and entitlement) rather than an immediate nominal retail price explosion.
3. **Incomplete Donor Substitution:** The EU's annual funding (~$100M) provides a vital operational floor but cannot replace the multi-billion-dollar scale of US assistance, leaving millions vulnerable to severe food insecurity.

---

## 6. Limitations
* **Sample Aggregation:** Market prices represent monthly national averages, smoothing out acute sub-national or regional market spikes.
* **Lack of Direct Household Data:** The absence of household-level food consumption scores (FCS) or Terms-of-Trade (wage-to-cereal ratios) limits the direct measurement of purchasing power erosion in this macro dataset.

---

## 7. Future Work
* **Spatial & Conflict Integration (ACLED):** Incorporating high-resolution conflict event data to capture localized market disruptions.
* **Modality of Aid:** Distinguishing between direct in-kind grain distributions and cash/voucher transfers to evaluate their differential impacts on local market incentives.
* **Terms of Trade (ToT):** Modeling pastoralist livestock-to-cereal price ratios to directly track real household purchasing power during aid withdrawals.

---

## 8. Acknowledgements
I would like to express my deepest gratitude to **Dr. Asma Nairi**, instructor for *MGMT310 - Humanitarian Aid and Management*, whose mentorship provided the foundation for this research and helped bridge the gap between quantitative data science and humanitarian policy analysis.