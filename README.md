# Regression capstone - Predicting Daily Electricity Consumption in Norway

## Project Overview
This capstone investigates whether daily electricity consumption in Norway can be predicted using weather, seasonality, and lagged demand features.

**Problem Framing:**  
Accurate forecasting supports sustainable hydropower reservoir management, grid stability, and reduced reliance on imports.  

**Hypothesis vs Findings:**  
The initial hypothesis assumed that electricity consumption could be predicted primarily from weather and seasonality.  
Results disproved this: lagged demand features (yesterday’s and last week’s consumption) were far more important.  

---

## Key results
- Weather + Seasonality only → poor performance (negative R²).  
- Lags only → strong performance, test R² ≈ **0.92**.  
- Full model → Ridge Regression (α=1000) confirmed as the most robust model.  
- Random Forest consistently overfit, with weaker generalization.  

---

## Context and impact
- **Climate trends:** Recent years show **colder summers and milder winters**, weakening traditional seasonal patterns.  
- **Electrification:** Norway leads the world in EV adoption (over 80% of new cars sold are electric), contributing to high but relatively stable demand.  
- These structural changes explain why lag features dominate short-term prediction.  

---

## Workflow
1. **Data Preparation**  
   - [ENTSO-E Transparency Platform](https://transparency.entsoe.eu/): daily total load (2015–2025)  
   - [Norwegian Meteorological Institute](https://thredds.met.no/thredds/catalog/senorge/seNorge_2018/Archive/catalog.html): daily weather (temperature, precipitation)  

2. **EDA**  
   - Weak correlation between weather and consumption  
   - Seasonal decomposition shows yearly cycles, but less pronounced winter peaks  

3. **Modeling**  
   - Setup 1: Weather + Seasonality → failed (negative R²)  
   - Setup 2: Lags only → strong (R² ≈ 0.92)  
   - Setup 3: Full model → Ridge best balance  

4. **Optimization**  
   - Ridge regularization stabilized coefficients (α=1000)  
   - Random Forest tuning reduced overfitting but remained weaker than Ridge  

5. **Diagnostics**  
   - Residual plots confirmed unbiased errors and good generalization  

---

## Repository Structure
```text
.
├── datasets/              # raw and/or processed data (CSV, links in README)
├── notebook/              # regression_capstone.ipynb
├── report/                # technical report (PDF, up to 12 pages)
├── stakeholders/          # stakeholder summary (PDF, plain language)
└── README.md              # project overview (front page of repo)
```

---

## Final model
- **Model:** Ridge Regression  
- **Test R²:** 0.92  
- **Key drivers:** Lag features (yesterday, last week)  
- **Interpretation:** Persistence dominates short-term electricity demand, while weather and seasonality play a minor role.  

---

## How to run
1. Clone this repository  
2. Install requirements:  
   ```bash
   pip install -r requirements.txt
3. Open the notebook:
   ```bash
   jupyter notebook regression_capstone.ipynb

## Ethical Considerations
This project used only aggregated, public datasets (ENTSO-E, MET Norway), ensuring no personal data was involved. 

The modeling workflow is transparent and reproducible.  

Limitations include heavy reliance on lag features, which may underrepresent structural changes (e.g., policies, extreme climate events).  

Accurate forecasts can support sustainability, but responsible use requires continuous monitoring and clear communication of limitations.

## License
This project is for educational purposes under the BSc AI and Sustainable Technologies capstone program at Tomorrow University of Applied Sciences.