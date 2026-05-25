# Statistics-Project

Panel-data analysis of **EU wage dispersion** (Group 22), focusing on how minimum wages and macroeconomic conditions relate to wage inequality across the wage distribution.

## Project purpose

This repository contains the materials for a statistics/econometrics project titled **"EU Wage Dispersion"**. The analysis studies 21 EU countries with statutory minimum wages (2018–2023) and examines associations between:

- real minimum wage (PPP-adjusted)
- real GDP per capita (PPP-adjusted)
- unemployment rate

and wage-inequality measures:

- `d90d10` (overall dispersion)
- `d50d10` (lower-tail inequality)
- `d90d50` (upper-tail inequality)

## Repository contents

- `Group 22 R report.RData`  
  R workspace data file used in analysis (contains objects including `panel_final` and key variables such as `country`, `year`, `d90d10`, `d50d10`, `d90d50`, `real_min_wage_ppp`, `gdp_pc_real_ppp`, `unemployment_rate`).

- `R Scripts.rar`  
  Archive containing the project scripts:
  - `R Scripts/script_group_22 _models Script.Rmd`
  - `R Scripts/script_group_22_Poster Script.Rmd`

- `Statistics Project Report.pdf`  
  Final report artifact (poster-style PDF, title metadata: *EU Wage Dispersion*).

## Methods and workflow (from the R scripts)

The scripts implement this workflow:

1. Load panel data (`panel_final`) from `.RData`.
2. Create transformed regressors:
   - `log_min_wage = log(real_min_wage_ppp)`
   - `log_gdp_pc = log(gdp_pc_real_ppp)`
3. Filter finite/non-missing observations for estimation.
4. Build panel structure with `pdata.frame(index = c("country", "year"))`.
5. Estimate, for each dependent variable (`d90d10`, `d50d10`, `d90d50`):
   - pooled OLS (`model = "pooling"`)
   - fixed effects (`model = "within"`)
   - random effects (`model = "random"`)
6. Run diagnostics/inference:
   - Breusch–Pagan heteroskedasticity tests
   - cluster-robust standard errors (country level via `vcovHC(..., cluster = "group")`)
   - robust Hausman tests to choose FE vs RE
7. Produce summary tables (p-values) and country-level inequality plots.

## Main findings (as documented in project scripts/report text)

- For **D90/D10** and **D50/D10**, robust Hausman tests favor **fixed effects**.
- For **D90/D50**, robust Hausman tests favor **random effects**.
- Higher real GDP per capita and unemployment are associated with higher inequality in lower/middle-tail comparisons (D90/D10, D50/D10).
- Real minimum wage effects are generally small/negative and statistically weak in preferred specifications.
- Effects are weaker and less robust in the upper-tail comparison (D90/D50).

Selected model equations reported in the project materials:

- **D90/D10 (Robust FE):**  
  `D90/D10 = -0.286*log(min_wage) + 1.207*log(gdp_pc) + 0.064*unemployment_rate`
- **D50/D10 (Robust FE):**  
  `D50/D10 = -0.202*log(min_wage) + 0.684*log(gdp_pc) + 0.043*unemployment_rate`
- **D90/D50 (Robust RE):**  
  `D90/D50 = -0.033*log(min_wage) - 0.153*log(gdp_pc) - 0.013*unemployment_rate`

## Requirements

- R (recommended: recent version)
- R packages used by the scripts:
  - `plm`
  - `dplyr`
  - `lmtest`
  - `sandwich`
  - `knitr`
  - `ggplot2`
  - `scales`
  - `posterdown` (for poster-style HTML rendering in `script_group_22_Poster Script.Rmd`)

Install example:

```r
install.packages(c("plm", "dplyr", "lmtest", "sandwich", "knitr", "ggplot2", "scales", "posterdown"))
```

## How to reproduce

1. Clone/download the repository.
2. Extract scripts from the archive:

```bash
7z x "R Scripts.rar"
```

3. Open the extracted `.Rmd` files in RStudio (or render via `rmarkdown::render`).
4. Ensure the data file path matches script expectations.

> Note: scripts reference `load("data_group_22.RData")`, while this repository contains `Group 22 R report.RData`. To run as-is, either rename/copy the file or update `load(...)` paths in the `.Rmd` files.

Example rename:

```bash
cp "Group 22 R report.RData" "data_group_22.RData"
```

5. Render analyses:

```r
rmarkdown::render("R Scripts/script_group_22 _models Script.Rmd")
rmarkdown::render("R Scripts/script_group_22_Poster Script.Rmd")
```

## Data source and reference

- OECD Statistics Database (as cited in project files)
- Included academic reference in project script: Autor, Manning, & Smith (2016), *American Economic Journal: Applied Economics*.

---

If you only want to review conclusions without rerunning code, open `Statistics Project Report.pdf`.
