# Seasonal Agriculture Performance Analysis

A data analytics project examining how agricultural performance — yield, profit, resource usage, and environmental conditions — varies across the **Kharif**, **Rabi**, and **Zaid** seasons in India. The analysis covers 4,000 farm records across 8 states, 8 crops, and 4 irrigation methods, using data cleaning, exploratory data analysis, correlation analysis, and one-way ANOVA testing to derive evidence-based, data-driven recommendations for seasonal agricultural planning.

> Built as part of the **VOIS AICTE Batch 2026–2027 Major Project** (Data Analytics), under the VOIS x Edunet Foundation program.

---

## Table of Contents

- [Problem Statement](#problem-statement)
- [Objective](#objective)
- [Dataset](#dataset)
- [Tech Stack](#tech-stack)
- [Repository Structure](#repository-structure)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
- [How to Run](#how-to-run)
- [Future Scope](#future-scope)
- [Author](#author)
- [Acknowledgements](#acknowledgements)

---

## Problem Statement

Agricultural activities are influenced by seasonal variations in environmental conditions, farming practices, resource availability, and market conditions. As a result, agricultural performance may differ from one season to another. However, raw agricultural data does not clearly explain how performance changes across seasons or what patterns can be observed under different seasonal conditions.

This project analyzes a seasonal agriculture dataset to investigate seasonal differences in agricultural performance by identifying meaningful patterns, trends, relationships, and variations within the available data.

## Objective

- Explore and understand the dataset
- Clean and prepare the data for analysis
- Examine how agricultural performance varies across seasons
- Identify important seasonal patterns and trends
- Investigate relationships between seasonal conditions and agricultural outcomes
- Compare relevant groups (crops, states, irrigation methods) within different seasons
- Identify significant differences or unusual patterns
- Apply appropriate statistical and visualization techniques
- Interpret findings based on evidence from the dataset
- Develop meaningful, data-driven conclusions and recommendations

## Dataset

**File:** `seasonal_agriculture_performance_dataset.csv`

| Attribute | Detail |
|---|---|
| Records | 4,000 farm records |
| States | 8 (Andhra Pradesh, Maharashtra, Telangana, Karnataka, Gujarat, Tamil Nadu, Punjab, Madhya Pradesh) |
| Districts | 10 |
| Crops | 8 (Wheat, Maize, Pulses, Rice, Cotton, Chilli, Groundnut, Sugarcane) |
| Seasons | 3 (Kharif, Rabi, Zaid) |
| Irrigation methods | 4 (Drip, Flood, Rainfed, Sprinkler) |

The dataset spans three categories of information:

- **Environmental conditions** — Rainfall, Temperature, Humidity, Sunlight Hours, Soil pH, Soil Moisture
- **Farming inputs** — Fertilizer, Pesticide, Seed Quality Score, Irrigation Method, Water Used
- **Economic & agronomic outcomes** — Yield, Production, Market Price, Total Cost, Revenue, Profit, Water Efficiency, Disease/Pest Risk

Three columns (`Rainfall_mm`, `Soil_Moisture_pct`, `Yield_Tonnes_Ha`) contained missing values, which were cleaned as part of the analysis (see [Methodology](#methodology)).

## Tech Stack

- **Python 3**
- **Pandas, NumPy** — data cleaning and manipulation
- **Matplotlib, Seaborn** — data visualization
- **SciPy (`stats`)** — one-way ANOVA statistical testing
- **Jupyter Notebook** — documentation and analysis environment

## Repository Structure

```
├── Seasonal_Agriculture_Performance_Analysis.ipynb   # Fully executed analysis notebook
├── seasonal_agriculture_performance_dataset.csv      # Source dataset
└── README.md                                         # Project documentation (this file)
```

## Methodology

The notebook (`Seasonal_Agriculture_Performance_Analysis.ipynb`) is organized into the following stages:

1. **Setup and Data Loading** — import libraries, load the dataset, define a consistent season color scheme used across every chart
2. **Understanding the Dataset** — data types, missing values, duplicates, summary statistics
3. **Data Cleaning** — missing values in `Rainfall_mm`, `Soil_Moisture_pct`, and `Yield_Tonnes_Ha` are filled using the **season-wise median** (not the overall median), since these variables genuinely differ by season and an overall median would bias the comparison the project is meant to investigate
4. **Dataset Overview** — record counts by season and crop
5. **Yield & Profit by Season** — boxplots and summary statistics for the two core performance indicators
6. **Environmental Conditions by Season** — rainfall, temperature, humidity
7. **Resource Usage by Season** — fertilizer, pesticide, water used
8. **Economic Outcomes by Season** — revenue, cost, profit
9. **Correlation Analysis** — a correlation heatmap across environmental, input, and performance metrics
10. **Irrigation Efficiency Across Seasons** — water efficiency by irrigation method, faceted by season
11. **Crop × Season Profit Analysis** — a heatmap identifying which crops are profitable in which seasons
12. **Disease/Pest Risk by Season**
13. **State × Season Yield Analysis** — a heatmap checking whether seasonal patterns are consistent across states
14. **Statistical Testing** — one-way ANOVA on Yield and Profit across seasons, to check whether observed differences are statistically significant or could be random variation
15. **Key Findings** — evidence-based conclusions
16. **Recommendations** — actionable, data-driven suggestions

## Key Findings

1. **Yield trends down across seasons, but the difference is not statistically strong.** Average yield falls from 5.63 t/ha (Kharif) → 5.04 t/ha (Rabi) → 4.64 t/ha (Zaid), but a one-way ANOVA gives **p ≈ 0.21** — the within-season variation is large enough that this trend cannot be confidently generalized from yield alone.
2. **Profit differs sharply and significantly across seasons (ANOVA p < 0.001).** Average profit falls from ₹1.79 lakh (Kharif) to ₹0.88 lakh (Rabi) to a **net average loss of ≈ ₹25,000 in Zaid**.
3. **The share of loss-making farms rises steadily each season:** 42.2% (Kharif) → 51.1% (Rabi) → 64.5% (Zaid).
4. **The profit decline is driven by falling revenue, not falling price.** Market price stays nearly flat (≈ ₹44,200–44,900/tonne) across seasons, while revenue drops from ₹7.1 lakh (Kharif) to ₹5.2 lakh (Zaid) as production volume falls. Average cost stays roughly flat (₹5.1–5.4 lakh), so costs do not shrink to match lower output — this is what pushes many Zaid farms into a loss.
5. **Kharif has the highest rainfall (852 mm) and humidity (72%)** but also the **highest disease/pest risk (54.5%)**, versus Zaid's lowest risk (38.2%) — a trade-off between favorable growing conditions and pest pressure.
6. **Crop choice matters more than season timing.** Sugarcane and Chilli stay strongly profitable in *every* season, while Wheat, Rice, and Maize run losses in *every* season in this dataset.
7. **Fertilizer, pesticide, and water usage are nearly flat across seasons** (~185 kg/ha fertilizer, ~5 L/ha pesticide), even though yield and profit are not — input usage does not appear to be adjusted seasonally.
8. **Rainfall, Fertilizer, and Seed Quality each show close to zero linear correlation with Yield individually** (all |r| < 0.03) — yield is likely shaped by a combination of factors rather than any single input acting alone.
9. **Season affects each state differently.** For example, Punjab peaks sharply in Rabi (8.61 t/ha) while Maharashtra dips in Zaid (2.27 t/ha) — seasonal patterns are not uniform across regions.

## Recommendations

- **Treat Zaid season as a financial risk zone.** With ~65% of Zaid farms losing money, prioritize cost-control measures (input planning, price negotiation, storage/timing of sale) specifically for Zaid.
- **Prioritize crop selection alongside season planning.** Since Sugarcane and Chilli remain profitable across all seasons while Wheat, Rice, and Maize do not, seasonal planning should be paired with crop-level profitability review.
- **Investigate the cost side of Zaid farming specifically**, since yield per hectare does not collapse in Zaid but profit does — the gap points to costs not scaling down with lower output.
- **Re-evaluate fertilizer/pesticide dosing by season and crop** instead of applying a near-uniform amount.
- **Use multivariate modeling for future yield prediction**, since no single environmental or input factor correlates strongly with yield in isolation.

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/SagarSharma131006/VI_Internship_Major_Project.git
   cd VI_Internship_Major_Project
   ```
2. Install the required dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scipy jupyter
   ```
3. Launch Jupyter Notebook:
   ```bash
   jupyter notebook Seasonal_Agriculture_Performance_Analysis.ipynb
   ```
4. Run all cells (`Cell → Run All`) to reproduce the complete analysis, including all charts and the ANOVA test.

## Future Scope

- Build a multivariate/ML model (e.g. Random Forest) to predict Yield and Profit, since individual factors show weak linear correlation on their own
- Extend the dataset to more states, crops, and multiple years to study seasonal trends over time
- Integrate live weather API data for real-time seasonal risk alerts
- Build a farmer-facing dashboard recommending the most profitable crop per season and region
- Study the cost-structure drivers behind Zaid season losses in more depth

## Author

**Sagar Sharma**
B.Tech CSE (AI & ML), Panipat Institute of Engineering and Technology
AICTE Student ID: `STU688dcbd0133971754123216`

- Email: sagarsharma131006@gmail.com
- LinkedIn: [linkedin.com/in/sagar-sharma-148b1a3a4](https://www.linkedin.com/in/sagar-sharma-148b1a3a4/)
- GitHub: [SagarSharma131006](https://github.com/SagarSharma131006)

## Acknowledgements

This project was completed as part of the **VOIS AICTE Batch 2026–2027 Major Project**, under the Vodafone Idea Foundation (VOIS) and Edunet Foundation collaboration, following completion of the **Data Visualization** course.
