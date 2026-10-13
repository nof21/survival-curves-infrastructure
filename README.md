# survival-curves-infrastructure
> **Manuscript:** This repository contains the data and analysis code associated with the manuscript **“Realised energy asset lifetimes reshape infrastructure turnover in the net zero transition”**, published in **XX**. DOI: **[DOI]**.

This repository contains the data-processing, survival-analysis, carbon-intensity, and infrastructure-replacement calculations used to examine the realised operational lifetimes of electricity-generation assets.

The analysis covers 10 generation technologies:
- Bioenergy
- Coal
- Geothermal
- Hydropower
- Natural gas
- Nuclear
- Oil
- Solar PV
- Offshore wind
- Onshore wind

The workflow combines asset-level information on commissioning, retirement, operating status, and installed capacity to quantify observed retirement ages, the age structure of operating fleets, deviations from assumed technical lifespans, implications for manufacturing-related carbon intensity, and cumulative replacement-capacity requirements.

## Main analysis

| Notebook | Analysis |
|---|---|
| `main-figure-1.ipynb` | Kaplan–Meier survival curves for the 10 generation technologies using the full survival sample, with operating assets treated as right-censored observations and retired assets as events. Reference survival levels of 80%, 50%, and 10% are reported where reached. |
| `main-figure-2.ipynb` | Comparison of technical lifespan ranges, observed retirement-age distributions, Kaplan–Meier lifespan estimates, and the age structure of the active fleet. |
| `main-figure-3.ipynb` | Carbon intensity as a function of assumed operating lifespan. The analysis combines manufacturing-related emissions with fuel-related emissions where applicable and compares technical, observed-retirement, and Kaplan–Meier lifespan assumptions. A second panel evaluates the operating time/electricity generation required for manufacturing emissions to fall below 25 gCO2e/kWh. |
| `main-figure-4.ipynb` | Cumulative replacement-capacity requirements for coal, natural gas, and nuclear reference cases across Global, China, EU, India, and US cases. Replacement options include Solar PV, Wind Onshore, Wind Offshore, and Nuclear where applicable. The default calculation uses continuous replacement cycles and compares requirements implied by Kaplan–Meier and observed-retirement lifetimes. |
| `main-table-1.ipynb` | Multi-horizon restricted mean survival time (RMST) analysis using the full censored survival sample. RMST is evaluated at 10, 20, 30, 40, 50, and 60 years where supported by observed follow-up. Solar Thermal is excluded, observations are not capacity weighted, and RMST is not extrapolated beyond observed follow-up. |

### Main-table outputs

`main-table-1.ipynb` exports:

```text
tables/si/rmst_multihorizon_summary.xlsx
figures/si/rmst_multihorizon.png
figures/si/rmst_multihorizon.pdf
```

## Supplementary analyses

| Notebook | Analysis |
|---|---|
| `si-figure-1.ipynb` | Comparison of global installed generation capacity in 2025 with illustrative 2050 capacity levels. Values are assembled from the external sources and scenario assumptions documented directly in the notebook. |
| `si-figure-2-3.ipynb` | **Figure S2:** reconstructed cumulative operating capacity compared with the reference `EIA Data World` series. **Figure S3:** percentage difference between the reconstructed dataset and the reference series. |
| `si-figure-4-5.ipynb` | **Figure S4:** annual commissioned and retired capacity by technology. **Figure S5:** capacity additions and retirements by technology and deployment year, with additions plotted as positive values and retirements as negative values. |
| `si-figure-6.ipynb` | Kaplan–Meier curves calculated using **retired assets only**, showing the observed retirement-age distribution conditional on assets having retired. This should not be interpreted as the full censored survival estimate. |
| `si-figure-7.ipynb` | Age-survival curves for the **currently operating fleet**. Curves represent the share of operating assets with age greater than or equal to a given value; reference ages are shown at the 80%, 50%, and 10% levels, together with corresponding installed-capacity information. |
| `si-figure-8.ipynb` | EIA-860-only Kaplan–Meier sensitivity analysis across the same 10 harmonised technologies, using the `EIA-860` worksheet rather than the full combined dataset. |
| `si-figure-9.ipynb` | Natural-gas survival sensitivity analysis using the `Gas - 85`, `Gas - 90`, and `Gas - 95` worksheets. |
| `si-figure-10.ipynb` | Oil survival sensitivity analysis using the `Oil - 85`, `Oil - 90`, and `Oil - 95` worksheets. |
| `si-figure-11.ipynb` | Material intensity by generation technology and material group. This input analysis retains 11 technologies, including Solar Thermal. |
| `si-figure-12.ipynb` | Manufacturing-related carbon intensity by generation technology and material group. This input analysis retains 11 technologies, including Solar Thermal. |

## Data

The harmonised analysis dataset is available at:

```text
data/combined_dataset.xlsx
```

Depending on the notebook, the dataset includes fields such as technology, commissioning year, retirement year, operating status, installed capacity, calculated lifespan, and survival-event indicator. The workbook also contains technology-level material and carbon-intensity inputs used by the corresponding figure notebooks.

### Primary asset-data sources

The harmonised dataset draws on publicly available electricity-generation asset databases, including:

- **U.S. Energy Information Administration (EIA), Form EIA-860**  
  https://www.eia.gov/electricity/data/eia860/

- **World Resources Institute (WRI), Global Power Plant Database**  
  https://datasets.wri.org/datasets/global-power-plant-database

- **Global Energy Monitor (GEM)** technology-specific power-plant datasets  
  https://globalenergymonitor.org/

Additional literature and statistical sources are used for technical lifespan assumptions, capacity factors, material intensities, material emission factors, fuel-related emissions, and technology-specific scenario values. Full source attribution is provided in the associated manuscript and Supplementary Information.

## Methodological overview

### Asset lifespans

For retired assets, realised operational lifespan is calculated from commissioning and retirement years:

```text
lifespan = retirement year - commissioning year
```

Records with invalid or non-positive operational durations should be treated consistently with the filtering criteria documented in the analysis notebooks and manuscript.

### Survival analysis

Technology-specific survival functions are estimated using the Kaplan-Meier estimator. The analysis distinguishes between the survival distributions of retired assets and the age structure of assets that remain operational.

Selected survival thresholds are used to characterise the distributions, including the median survival age.

### Technical versus realised lifespans

Observed retirement ages are compared with technical lifespan ranges compiled from the literature. This comparison is used to identify technologies for which realised operating durations differ materially from conventional engineering assumptions.

### Manufacturing carbon intensity

Manufacturing-related greenhouse gas emissions per unit of installed capacity are converted into electricity-normalised carbon intensity using technology-specific capacity factors and operating lifespans.

In general:

```text
manufacturing intensity
    = manufacturing footprint
    / lifetime electricity generation
```

Shorter realised lifespans increase manufacturing-related carbon intensity because embodied emissions are distributed over less lifetime electricity generation.

### Fuel-related emissions

For fuel-consuming technologies, fuel-related greenhouse-gas emissions are added to the manufacturing contribution. Fuel emission factors are expressed per unit of fuel-energy input and converted to electricity output using the relevant conversion efficiency.

### Replacement capacity

Cumulative replacement requirements account for:

1. differences in capacity factor between the reference and replacement technologies; and
2. repeated replacement cycles over the operating horizon of the reference technology.

The notebooks allow continuous replacement-cycle treatment and compare technical-lifespan assumptions with realised retirement lifespans.
