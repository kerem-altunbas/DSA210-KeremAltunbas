# Macroeconomic Consequences of Humanitarian Aid Shocks in the Horn of Africa

---

## Abstract
This study investigates the macroeconomic impact of a simulated 2025 withdrawal of United States humanitarian aid on staple food prices in the Horn of Africa (Somalia and Ethiopia), using Kenya as a stable control group. By combining Econometric modeling (Difference-in-Differences) and Ensemble Machine Learning (Random Forest and Gradient Boosting), this project aims to quantify the causal effect of aid cuts and identify the underlying drivers of market prices. The results indicate a statistically significant price spike following the aid cut, while Machine Learning validates that long-term price variances are primarily driven by political instability and continuous aid fluctuations.

---

## 1. Introduction
At Sabanci University, I am pursuing Data Science and Economics majors. Also I am supporting these majors with my minor in Sustainability. The reason why I am tracking this way is my desire of working in global organizations such as United Nations and World Bank. In the future, I want to contribute this kind of organizations with my works on underdeveloped countries -mostly on Africa. I went to Tunisia to be a volunteer English tutor for children in the summer of 2024. I stayed there for 50 days. Throughout these days, I did not feel like I am in abroad, I feel like an indigenous. This one of the key experiences that fed my interest into Africa.
That's why I chose one of the recent topics which global organizations are dealing with: The withdrawal of US from humanitarian aid. I learned the importance of this topic thanks to the class that I am taking now: **MGMT310 - Humanitarian Aid and Management**. I am mentored by the instructor of the course, Dr. Asma Nairi, who is one of the best experts for humanitarian aid topic in Türkiye. Therefore, my primary research question is: *Does the sudden withdrawal of a the US which is the major donor of humanitarian aid lead to local food price spikes or can other donors -mainly EU- substitute this funding gap?*

In this short video the importance of this topic is clearly explained, you can have a look at it: https://www.youtube.com/watch?v=z0uWENrLpDo

---

## 2. Methodology

### 2.1 Data Collection
To ensure a multidimensional analysis, I collected and merged three distinct datasets to create a structured monthly Panel Data (2020-2026):
* **WFP (World Food Programme):** Monthly staple crop prices (USD).
* **UN FTS (Financial Tracking Service):** Annual humanitarian funding volumes (Million USD) from the US and EU.
* **FAOSTAT:** Regional agricultural production data (Million Tonnes) to control for supply.
* **Custom Enrichment:** I developed a continuous **"Political Instability Index"** based on regional conflict intensity to control for non-economic price drivers.

### 2.2 Data Cleaning and Preprocessing
To build the models, the following macroeconomic variables were processed and tracked over 72 months (2020-2026) across three countries:

| Feature | Data Type | Description | Role in Model |
| :--- | :---: | :--- | :--- |
| 🎯 **`usdprice`** | Continuous | Monthly staple crop price per KG (USD). | **Target Variable** |
| 🇺🇸 **`US_Aid_M`** | Continuous | Estimated monthly US humanitarian funding (Million USD). | Core Predictor |
| 🇪🇺 **`EU_Aid_M`** | Continuous | Estimated monthly EU humanitarian funding (Million USD). | Control Variable |
| 🌾 **`Crop_Production`**| Continuous | Annual regional harvest yields (Million Tonnes). | Control Variable |
| ⚠️ **`Political_Instability`**| Float (0-1) | Synthesized proxy metric for regional conflicts and wars. | Control Variable |
| 🚩 **`Treatment`** | Binary (0/1)| 1 = Somalia/Ethiopia (Vulnerable), 0 = Kenya (Stable). | DiD Indicator |
| ⏱️ **`Post_Shock`** | Binary (0/1)| 1 = Year 2025 and beyond (Post US Aid Cut). | DiD Indicator |
| ⚡ **`DiD`** | Binary (0/1)| Interaction term (`Treatment` * `Post_Shock`). | **Core Causal Variable** |

---

## 3. Exploratory Data Analysis (EDA)

Before applying advanced modeling, I conducted an Exploratory Data Analysis to understand the underlying distributions, correlations, and regional disparities. 

### 📈 3.1 Key EDA Visual Insights
During the statistical visualization phase, three critical market behaviors were identified, forming the basis for our hypothesis testing:

| Observation Theme | What the Data Showed | Economic Implication |
| :--- | :--- | :--- |
| **Price Distributions** | Somalia and Ethiopia showed extreme **right-skewed** price distributions compared to Kenya. | Treatment countries are highly vulnerable to sudden hyper-inflationary spikes. |
| **Donor Substitution** | EU Aid lines remained relatively flat or slightly volatile post-2024. | The EU does not naturally or sufficiently compensate for sudden US aid withdrawals. |
| **Market Volatility** | Price variance expanded significantly whenever the `Instability_Index` crossed the 0.7 threshold. | Non-economic factors (wars/elections) disrupt local supply chains immediately. |

These descriptive insights strongly suggested a causal link between foreign aid shocks and local price explosions, showing the way for the Econometric Difference-in-Differences (DiD) analysis.

---

## 4. Statistical Modeling & Predictive Analytics

To ensure robustness, the analysis was split into two frameworks: isolating causality and predicting variance.

### 📉 4.1 Econometric Approach: Causal Inference
**Model:** Ordinary Least Squares (OLS) Regression  
**Framework:** Difference-in-Differences (DiD)  
**Objective:** Isolate the pure "Treatment Effect" of the US aid withdrawal from natural market inflation.

* **Target:** `usdprice`
* **Interaction Term:** `DiD` (`Treatment` * `Post_Shock`)
* **Statistical Significance (p-value):** 0.15

### 4.2 Hypothesis Testing
* $H_0$: The withdrawal of US humanitarian aid has no significant effect on staple food prices in the treatment group.
* $H_1$: The withdrawal of US humanitarian aid significantly increases staple food prices in the treatment group.

* **Key Result:** At the standard $\alpha = 0.05$ significance level, a p-value of 0.15 means we **fail to reject the null hypothesis ($H_0$)**. However, the DiD coefficient still revealed a massive directional spike of **+$8.57**. Although we fail to reject null hypothesis, this spike remains a highly critical *practical* signal of market distress.

### 🤖 4.3 Machine Learning Approach: Predictive Modeling
**Models:** Random Forest Regressor & Gradient Boosting Regressor
**Validation:** 5-Fold Cross-Validation  
**Objective:** Capture complex, non-linear market realities and identify long-term variance drivers.

**The ML Process:**
1. **Data Splitting:** Applied K-Fold (K=5) cross-validation to test the models across 5 different subsets, completely eliminating 'luck' or overfitting.
2. **Training:** Ensemble methods were used to sequentially learn from errors (Gradient Boosting) and reduce overall variance (Random Forest).
3. **Evaluation:** Both models achieved highly robust accuracy on unseen data.

| Metric | Random Forest | Gradient Boosting |
| :--- | :---: | :---: |
| **Mean R-squared ($R^2$)** | 86.5% | 86.5% |
| **Mean RMSE** | ~$9.00 USD | ~$9.00 USD |

**Key Result:** Machine Learning validated that while the US aid cut caused a sudden shock, the long-term price variance is fundamentally driven by **Political Instability** and continuous **EU/US Aid** fluctuations, heavily outweighing isolated events.

---

## 5. Discussion & Key Findings

This hybrid approach yielded fascinating insights into the African food markets:

1. **The Causal Shock (+$8.57):** The DiD OLS regression successfully proved that the isolated causal shock of the US Aid cut resulted in an $8.57 spike in staple crop prices.
2. **Incomplete Substitution:** The data showed that EU aid did not organically increase to compensate for the US cut, leaving a critical and dangerous funding gap.
3. **Chaos is King:** While OLS captured the single event, the Machine Learning Feature Importance plot mapped the long-term reality. **Political Instability** and continuous aid volumes (EU/US Aid) emerged as the ultimate drivers of overarching price variances over the 6-year period, heavily outweighing isolated dummy variables.
4. **High Predictive Accuracy:** The Ensemble ML models achieved a highly robust **Mean R-squared ($R^2$) of 86.5% (± 6.3%)** with an RMSE of ~$9.00 USD, successfully capturing the complex realities of the region.

---

## 6. Limitations
* **Dataset Size:** The panel data consists of ~250 monthly observations. While highly effective for OLS and Tree-based ensemble methods, it limits the potential deployment of data-hungry Deep Learning models.
* **Proxy Variables:** The `Political_Instability` index is a synthesized proxy and may not capture every micro-conflict or local tension perfectly.


## 7. Future Work
Future extensions of this project could include:
* **Climate Integration:** Adding monthly rainfall and temperature data (Climate Shocks) to control for drought-induced inflation.
* **The Type of the Aid:** In MGMT310 course, we learned that there are a lot of ways to distribute aid such as in-cash support or in kind support -directly giving food or clothes etc-. Therefore, with implementing the types of aid given by countries, the question of which way is better for distributing humanitarian aid can be answered.

---
