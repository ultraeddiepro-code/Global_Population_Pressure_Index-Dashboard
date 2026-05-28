# Global Population Pressure Index Dashboard

> An interactive Power BI dashboard analyzing **population pressure across countries** using demographic, economic, environmental, and food security indicators -- built with 11 cleaned datasets from World Bank, UN, IMF, FAO, UNDP, and OWID.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-Open%20Data-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange?style=for-the-badge)

---

## Overview

The **Global Population Pressure Index Dashboard** provides a comprehensive, multi-page view of how population growth interacts with resources, economy, water access, food security, and environmental sustainability across countries and regions.

The dashboard combines **11 cleaned datasets** to visualize population stress indicators and enable cross-country and cross-regional comparison over time (2000-2024).

---

## Objectives

- Measure and visualize **population pressure across countries and regions**
- Identify **high-risk regions** facing resource strain and food insecurity
- Enable **comparative analysis** between countries over time
- Support **data-driven insights** for planning and policy
- Build a clean, reproducible **data pipeline** from raw public data to Power BI

---

## Project Structure

```
Global_Population_Pressure_Index-Dashboard/
|
+-- data/
|   +-- raw/                        # Original downloaded datasets
|   +-- additional data/            # Supplementary datasets (World Bank, OWID, etc.)
|       +-- api en/                 # World Bank API CSV exports
|       +-- FAO_FS.csv
|       +-- global_hunger_index_2025.xlsx
|       +-- HDR25_Composite_indices_complete_time_series.csv
|       +-- owid-co2-data.csv
|       +-- world_bank_country_and_region.xlsx
|
+-- cleaned_data/                   # Cleaned & Power BI-ready CSVs
|   +-- dim_country_region.csv
|   +-- fact_population_un.csv
|   +-- fact_population_density.csv
|   +-- fact_land_area.csv
|   +-- fact_water_access.csv
|   +-- fact_economics_imf.csv
|   +-- fact_hdi.csv
|   +-- fact_co2_owid.csv
|   +-- fact_co2_wb.csv
|   +-- fact_food_security.csv
|   +-- fact_hunger_index.csv
|
+-- dashboard/                      # Power BI .pbix file
+-- notebooks/                      # Data cleaning & preprocessing scripts
+-- screenshots/                    # Dashboard screenshots
+-- docs/                           # Documentation
+-- README.md
+-- requirements.txt
```

---

## Dashboard Pages

| Page | Description |
|---|---|
| **1. Overview** | Global KPIs, population map, pressure index by region |
| **2. Economic Comparison** | GDP, GNI per capita, HDI, inflation across countries |
| **3. Resource Pressure & Relationships** | CO2, water access, food security, hunger index correlations |

---

## Key Metrics & Indicators

| Category | Indicators |
|---|---|
| Population | Total population, growth rate, density (people/km2) |
| Food Security | Undernourishment %, food insecurity %, protein supply, dietary energy adequacy |
| Hunger | Global Hunger Index score (2000, 2008, 2016, 2025) |
| Water Access | Rural, urban & total safe drinking water access (%) |
| CO2 & Energy | CO2 per capita, total GHG, coal/oil/gas emissions, energy per capita |
| Economics | GDP, GDP per capita, exports, imports volume, inflation |
| Human Development | HDI score, life expectancy, GNI per capita |
| Geography | Land area (km2), country region, income group classification |

---

## Data Model (Power BI)

The data model follows a **star schema** design:

```
dim_country_region  <----------------------------------------------+
       |                                                           |
       | (iso3 / country)                                          |
       v                                                           |
fact_population_un          fact_hdi                               |
fact_population_density     fact_co2_owid                          |
fact_land_area              fact_co2_wb     -----------------------+
fact_water_access           fact_food_security
fact_economics_imf          fact_hunger_index
```

All fact tables share `country` / `iso3` and `year` as join keys.

---

## Data Sources

All datasets are publicly available and free to download.

### Population & Demographics

| Dataset | Source | Link |
|---|---|---|
| World Population by Country (1960-2023) | United Nations / World Bank | [Download](https://data.worldbank.org/indicator/SP.POP.TOTL) |
| Population Growth Rate | World Bank | [Download](https://data.worldbank.org/indicator/SP.POP.GROW) |
| Population Density (people/km2) | World Bank | [Download](https://data.worldbank.org/indicator/EN.POP.DNST) |

### Food Security & Hunger

| Dataset | Source | Link |
|---|---|---|
| Suite of Food Security Indicators | FAO / World Bank Data360 | [Download](https://data360.worldbank.org/en/dataset/FAO_FS) |
| Global Hunger Index Scores (2000-2025) | Welthungerhilfe & Concern Worldwide | [Download](https://www.globalhungerindex.org/) |

### CO2 Emissions & Energy

| Dataset | Source | Link |
|---|---|---|
| CO2 & Greenhouse Gas Emissions (full dataset) | Our World in Data (OWID) | [Download](https://github.com/owid/co2-data) |
| CO2 Emissions per Capita (AR5 standard) | World Bank | [Download](https://data.worldbank.org/indicator/EN.GHG.CO2.PC.CE.AR5) |

### Water Access

| Dataset | Source | Link |
|---|---|---|
| Access to Safe Drinking Water (Rural & Urban) | WHO / UNICEF JMP via World Bank | [Download](https://data.worldbank.org/indicator/SH.H2O.SMDW.ZS) |

### Human Development

| Dataset | Source | Link |
|---|---|---|
| Human Development Index -- Complete Time Series | UNDP Human Development Reports | [Download](https://hdr.undp.org/data-center/documentation-and-downloads) |
| Statistical Annex HDI Table (2025 Report) | UNDP | [Download](https://hdr.undp.org/data-center/documentation-and-downloads) |

### Economics & Trade

| Dataset | Source | Link |
|---|---|---|
| GDP (constant 2015 USD) | World Bank / IMF | [Download](https://data.worldbank.org/indicator/NY.GDP.MKTP.KD) |
| GDP per Capita (constant 2015 USD) | World Bank / IMF | [Download](https://data.worldbank.org/indicator/NY.GDP.PCAP.KD) |
| Exports & Imports Volume | IMF World Economic Outlook | [Download](https://www.imf.org/en/Publications/WEO/weo-database/2024/October) |
| Inflation (Average Consumer Prices) | IMF | [Download](https://www.imf.org/en/Publications/WEO/weo-database/2024/October) |

### Geography & Country Metadata

| Dataset | Source | Link |
|---|---|---|
| Country Region & Income Group Classification | World Bank | [Download](https://datahelpdesk.worldbank.org/knowledgebase/articles/906519) |
| Total Land Area (km2) | World Bank | [Download](https://data.worldbank.org/indicator/AG.LND.TOTL.K2) |
| World Regions Classification | Our World in Data | [Download](https://ourworldindata.org/grapher/world-regions-according-to-the-world-bank) |

---

## Cleaned Files (used in Power BI)

| File | Rows | Description |
|---|---|---|
| `dim_country_region.csv` | 266 | Country -> ISO3 code, Region, Income Group lookup |
| `fact_population_un.csv` | -- | Population & growth rate by country and year |
| `fact_population_density.csv` | 6,217 | Population density (people/km2) by country and year |
| `fact_land_area.csv` | 6,217 | Total land area (km2) by country and year |
| `fact_water_access.csv` | -- | Rural, urban and total safe water access (%) |
| `fact_economics_imf.csv` | -- | GDP, GDP per capita, exports, imports, inflation |
| `fact_hdi.csv` | 3,452 | HDI score, life expectancy, GNI per capita (2000-2023) |
| `fact_co2_owid.csv` | 5,375 | CO2, GHG, energy per capita -- OWID (2000-2024) |
| `fact_co2_wb.csv` | 6,275 | CO2 per capita -- World Bank AR5 (2000-2024) |
| `fact_food_security.csv` | 29,967 | Undernourishment %, food insecurity %, protein supply |
| `fact_hunger_index.csv` | 493 | Global Hunger Index scores (2000, 2008, 2016, 2025) |

---

## Tools & Technologies

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Dashboard creation & visualization |
| **Python (pandas, openpyxl)** | Data cleaning & transformation |
| **World Bank / UN / IMF APIs** | Raw data sourcing |
| **GitHub** | Version control & project hosting |

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/6thAce/Global_Population_Pressure_Index-Dashboard.git
cd Global_Population_Pressure_Index-Dashboard
```

### 2. Install Python dependencies

```bash
pip install -r requirements.txt
```

### 3. Run data cleaning scripts

```bash
cd notebooks
python clean_all_data.py
```

### 4. Open the dashboard

Open `dashboard/Global_Population_Pressure_Index_Dashboard.pbix` in **Power BI Desktop** and refresh the data sources pointing to your `cleaned_data/` folder.

---

## Screenshots

> Coming soon -- dashboard screenshots will be added here once the project reaches v1.0.

---

## License & Attribution

All datasets are publicly available under their respective open data licenses:

- **World Bank** -- [CC BY 4.0](https://datacatalog.worldbank.org/public-licenses)
- **Our World in Data** -- [CC BY 4.0](https://ourworldindata.org/faqs#how-can-i-use-our-worlds-content)
- **UNDP HDR** -- [CC BY 3.0 IGO](https://hdr.undp.org/copyright-and-terms-use)
- **FAO** -- [CC BY-NC-SA 3.0 IGO](https://www.fao.org/contact-us/terms/en/)
- **IMF** -- [IMF Terms of Use](https://www.imf.org/external/terms.htm)
- **Global Hunger Index** -- [CC BY-NC-ND 4.0](https://www.globalhungerindex.org/)

> If you use this project or its data pipeline, please credit the original data providers listed above.

---

## Author

**6thAce** -- [GitHub Profile](https://github.com/6thAce)

> If you found this project useful, consider giving it a star!
