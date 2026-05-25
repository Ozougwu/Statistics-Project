# Statistics Project: EU Wage Dispersion

This repository contains a statistical analysis project on wage inequality across EU countries, with a focus on how real minimum wages, real GDP per capita, and unemployment are associated with wage dispersion.

## Project Summary

The analysis studies 21 EU countries with statutory minimum wages (2018–2023), using interdecile wage ratios:

- **D90/D10** (overall inequality)
- **D50/D10** (lower-tail inequality)
- **D90/D50** (upper-tail inequality)

Panel-data models are estimated with pooled OLS, fixed effects, and random effects; robust inference uses country-clustered standard errors and robust Hausman model selection.

## Repository Contents

- `Statistics Project Report.pdf` — final written project report.
- `Group 22 R report.RData` — dataset/workspace used for the analysis.
- `R Scripts.rar` — archived R Markdown scripts:
  - `R Scripts/script_group_22 _models Script.Rmd`
  - `R Scripts/script_group_22_Poster Script.Rmd`

## Methods Used

The scripts implement:

- Data preparation and log transforms:
  - `log(real_min_wage_ppp)`
  - `log(gdp_pc_real_ppp)`
- Panel regressions (`plm`) for each inequality measure.
- Diagnostics and inference:
  - Breusch–Pagan heteroskedasticity tests
  - Robust standard errors (`vcovHC`, clustered by country)
  - Robust Hausman tests (`phtest`)
- Poster/report-ready summary tables and visualizations.

## Reproducing the Analysis

1. Extract scripts from `R Scripts.rar`.
2. Open the `.Rmd` files in RStudio (or render with `rmarkdown`).
3. Install required R packages:
   - `plm`, `dplyr`, `lmtest`, `sandwich`, `knitr`, `ggplot2`, `scales`, `posterdown`
4. Ensure the data file is available to the scripts.
5. Knit/render:
   - `script_group_22 _models Script.Rmd`
   - `script_group_22_Poster Script.Rmd`

## Important Data Filename Note

The scripts currently load:

- `data_group_22.RData`

But this repository provides:

- `Group 22 R report.RData`

You may need to either rename the file or update the `load(...)` path in the scripts before rendering.

## Key Finding (from project materials)

The project reports stronger and more consistent associations of GDP per capita and unemployment with lower-tail wage inequality (D90/D10 and D50/D10), while effects for upper-tail inequality (D90/D50) are weaker.

## Authors

Group 22:
- Batoul Abdullah
- Rosalina Vieira
- Christian Ozougwu
