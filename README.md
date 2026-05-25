#  Decoupling Kenya's Economic Growth from Energy Intensity: A Framework Evaluating Grid Expansion vs. Resource Efficiency

## 🔗 Project Quick Links
* **Interactive Tableau Dashboard:** [👉 Click Here to View the Live Dashboard (https://public.tableau.com/app/profile/marion.kariuki6726/viz/KenyaEnergyTransitionPortfolio-Phase1/Dashboard1))
* <img width="1499" height="1199" alt="Dashboard 1 (1)" src="https://github.com/user-attachments/assets/d6412d9d-e6a1-4fda-8085-48ebc942049a" />

* **Cleaned Dataset:** `kenya_energy_baseline.csv` (Stored in this repository)
* **Data Pipeline Script:** `clean_energy_data.py`

---
 
## 🎯 1. Project Objective & Business Problem
In development economics and national infrastructure planning, measuring grid expansion is only half the battle. The true operational bottleneck is understanding whether grid access successfully displaces inefficient traditional fuels and improves national economic productivity. 

This project analyzes Kenya's macroeconomic energy shifts (2000–2021) to solve three core questions:
1. **The Infrastructure Gap:** How effectively has electrical grid access scaled over the last two decades?
2. **The Behavioral Inertia:** Is increased electricity access successfully reducing household reliance on combustible biomass (charcoal/wood)?
3. **The Economic Dividend:** Has the transition to a cleaner grid meaningfully optimized Kenya's national energy efficiency (Primary Energy Intensity)?

---

## 🛠️ 2. Data Engineering & Pipeline (Python)
The raw data was ingested directly from the UN Humanitarian Data Exchange (HDX) via the World Bank Data Bank. Because the source file was structured vertically in a clean "long format," a Python pipeline was engineered to cleanly isolate our target baseline tracking indicators without disrupting the historical chronology.

```python
import pandas as pd

# Ingest raw dataset directly from the UN HDX live server
url = "[https://data.humdata.org/dataset/98dea0b7-3d7d-4ac1-90d6-8b1f19b9b757/resource/57cb3e00-30cf-4218-ad91-86ccdaa19c4e/download/energy-and-mining_ken.csv](https://data.humdata.org/dataset/98dea0b7-3d7d-4ac1-90d6-8b1f19b9b757/resource/57cb3e00-30cf-4218-ad91-86ccdaa19c4e/download/energy-and-mining_ken.csv)"
df = pd.read_csv(url)

# Isolate baseline tracking indicators
my_baseline_indicators = [
    "Energy intensity level of primary energy (MJ/$2021 PPP GDP)",
    "Access to electricity (% of population)",
    "Combustible renewables and waste (% of total energy)"
]

# Pipeline execution: Filter, sort chronologically, and export clean data layer
filtered_baseline = df[df['Indicator Name'].isin(my_baseline_indicators)]
filtered_baseline = filtered_baseline.sort_values(by=['Indicator Name', 'Year'])
filtered_baseline.to_csv("kenya_energy_baseline.csv", index=False)
