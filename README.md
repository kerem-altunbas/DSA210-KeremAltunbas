# DSA210 - Kerem Altunbaş - Term Project
# Macroeconomic Consequences of Humanitarian Aid Shocks in the Horn of Africa

## Project Overview
In this project, I am investigating the macroeconomic consequences of a simulated 2025 withdrawal of United States humanitarian aid on local staple food markets in the Horn of Africa. By combining data on food prices, humanitarian funding volumes, and agricultural production, I aim to quantify the causal effect of aid cuts and identify the underlying drivers of market prices. This project involves data collection, data cleaning, exploratory analysis, econometric modeling (Difference-in-Differences), and Machine Learning (Random Forest & Gradient Boosting) to determine the exact relationship between foreign aid and local food security.

In this short video the importance of this topic is clearly explained, you can have a look at it: https://www.youtube.com/watch?v=z0uWENrLpDo

## Objectives

### Understand Macroeconomic Influencers
Analyze how macroeconomic indicators, continuous aid volumes, and political instability dictate the long-term supply-demand balance in fragile economies like Somalia and Ethiopia.

### Isolate the Causal Shock
Pinpoint the exact isolated effect of the US aid withdrawal using a Treatment (Somalia/Ethiopia) and Control (Kenya) group dynamic.

### Apply Data Science in Humanitarian Context
Integrate methods from econometrics and predictive modeling to explore real-life global policy applications in a structured way.

## Motivation
Motivated by my volunteer experience in Tunisia and my career aspirations to work for the UN or World Bank, I wanted to bridge the gap between humanitarian aid and data science. This concept is deeply related with my coursework for **MGMT310 - Humanitarian Aid**.

## Data Exploration
- Visualize the extreme right-skewed price distributions of vulnerable countries.
- Explain trends in monthly humanitarian funding and local crop yields over time.
- Compare market volatility against the synthesized `Political_Instability` index.

## Hypothesis Testing
- **H₀:** The withdrawal of US humanitarian aid has no significant effect on staple food prices in the treatment group.
- **H₁:** The withdrawal of US humanitarian aid significantly increases staple food prices in the treatment group.

## Visualization
- Showing time-series changes in food prices vs. aid funding by line plots.
- Comparing price distributions across countries using boxplots.
- Feature Importance bar plots to interpret the long-term drivers of the Machine Learning models.

## Example Analysis
- Analyze whether the EU naturally substitutes the funding gap left by the US after 2024.
- A before/after shock analysis around the targeted year (2025) using DiD methodology to understand if local markets are affected significantly.
- Evaluate whether minor changes in crop production or major political instability have a stronger pull on local prices.

## Conclusion
By the end of this project, I aim to answer the following questions:
- Does the sudden withdrawal of a major donor -the US- lead to uncontrollable local food price spikes?
- Can other donors naturally substitute this funding gap?

The broader goal is not just a statistical output—but a clearer understanding of how global funding decisions affect physical survival and market dynamics in underdeveloped regions.

---

## 🚀 How to Reproduce the Analysis & Project Structure

**Project Structure:**
* `phase3_ML.ipynb`: The main and final Jupyter Notebook containing all data preprocessing, DiD modeling, and Ensemble Machine Learning analysis.
* `phase2.ipynb`: The intermediate phase notebook focusing on data collection, initial EDA, and early hypothesis testing.
* `FinalReport.md`: The comprehensive academic final report discussing methodology, insights, and future work.
* `Kerem_Altunbas_DSA210_Proposal.pdf`: The initial project proposal outlining the early research goals, dataset selections, and project scope.
* `requirements.txt`: The list of Python dependencies required to run the code.

**Instructions:**
1. Clone the repository:
2. Install dependencies: `pip install -r requirements.txt`
3. Launch Jupyter Notebook and run `phase3_ML.ipynb` sequentially.

---
## 🤖 AI Assistance Disclosure
In accordance with the DSA210 academic integrity guidelines, AI tools (LLMs) were utilized during this project for debugging Python code, refining academic English, and formatting Markdown structures. All data collection, modeling decisions, hypothesis formulations, and economic interpretations were performed independently.
