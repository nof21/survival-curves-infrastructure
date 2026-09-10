# survival-curves-infrastructure
> **Manuscript:** This repository contains the data and analysis code associated with the manuscript **“X”**, published in **XX**. DOI: **[DOI]**.

This repository contains the data-processing, survival-analysis, carbon-intensity, and infrastructure-replacement calculations used to examine the realised operational lifetimes of electricity-generation assets.

The analysis covers 11 generation technologies:
- Bioenergy
- Coal
- Geothermal
- Hydropower
- Natural gas
- Nuclear
- Oil
- Solar PV
- Solar thermal
- Offshore wind
- Onshore wind

The workflow combines asset-level information on commissioning, retirement, operating status, and installed capacity to quantify observed retirement ages, the age structure of operating fleets, deviations from assumed technical lifespans, implications for manufacturing-related carbon intensity, and cumulative replacement-capacity requirements.

## Main analysis

| Notebook | Analysis |
|---|---|
| `Old/main-figure-1.ipynb` | Kaplan-Meier survival analysis of retired electricity-generation assets |
| `Old/main-figure-2.ipynb` | Age structure and survival characteristics of the operating fleet |
| `Old/main-figure-3.ipynb` | Comparison of retired lifespans, active-fleet ages, and technical lifespan ranges |
| `Old/main-figure-4.ipynb` | Manufacturing and fuel-related carbon intensity, including the electricity generation required for manufacturing emissions to fall below a specified intensity threshold |
| `Old/main-figure-5.ipynb` | Cumulative replacement-capacity requirements for coal, natural gas, and nuclear reference cases |

## Supplementary analyses

| Notebook | Analysis |
|---|---|
| `si-figure-1.ipynb` | Global installed generation capacity in 2025 and illustrative 2050 capacity levels |
| `si-figure-2.ipynb` | Comparison of reconstructed installed capacity with reference capacity data and the corresponding percentage differences |
| `Old/si-figure-4-5.ipynb` | Annual commissioned and retired capacity, and deployment/retirement patterns by technology |
| `Old/si-figure-6.ipynb` | Kaplan-Meier survival curves for the complete analysis dataset |
| `si-figure-8.ipynb` | Material intensity by generation technology and material group |
| `si-figure-8.ipynb` | Manufacturing-related carbon intensity by generation technology and material group |

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
