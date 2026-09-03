# CO₂ Emissions and Economic Growth in Vietnam

An analysis of Vietnam's CO₂ emissions in regional context, prepared for
**EVNGENCO3**, one of Vietnam's largest power generation corporations, as it
plans a shift toward cleaner production ahead of the country's 2050 net-zero
target.

**Author:** Tuan Phuc Tran (Lucas Tran)
**Course:** DATA1001, University of Sydney
**Tools:** R (tidyverse, ggplot2, countrycode, knitr, kableExtra)

---

## The question

How do Vietnam's emissions compare with the rest of the region, and how tightly
is emissions growth still bound to economic growth?

## Data

[Our World in Data — CO₂ and Greenhouse Gas Emissions](https://ourworldindata.org/co2-data):
annual records for more than 200 countries from 1750 to 2023.

Variables used: `country`, `year`, `co2`, `co2_per_capita`, `coal_co2`,
`oil_co2`, `gas_co2`, `energy_per_capita`, `gdp`, `population`.

The dataset is not included in this repository. Download `owid-co2-data.csv`
from the [OWID repository](https://github.com/owid/co2-data) and place it beside
the `.qmd` file before rendering.

## Method

1. Removed OWID aggregate rows (regions, income groups) so only countries remain.
2. Mapped ISO3 codes to continents with `countrycode` for regional comparison.
3. Dropped rows missing emissions or population figures.
4. Compared per-capita emissions across continents, marking Vietnam's position.
5. Traced Vietnam's total emissions over time with a LOESS smoother.
6. Tested the GDP–emissions relationship with a Pearson correlation.
7. Audited missing values by variable to establish how far the data can be trusted.

## Key findings

- **Vietnam sits below the Asian median** for emissions per person, but the
  spread within Asia is wide, reflecting very different levels of industrialisation.
- **Emissions have climbed steeply since 2000**, tracking rapid growth in
  electricity demand.
- **GDP and emissions move almost in lockstep** (r ≈ 0.97, p < 0.001). Economic
  growth has not been decoupled from carbon output.

## Recommendations

Waiting for emissions intensity to fall on its own is not a strategy. The
analysis supports prioritising renewable capacity, efficiency upgrades to
existing thermal units, and emission tracking that can measure whether either
is working.

## Limitations

- GDP and energy indicators are patchier for developing countries and for
  earlier years, so the analysis likely understates Vietnam's earlier energy
  shifts.
- The correlation assumes a consistent linear GDP–emissions relationship.
  Structural change in Vietnam's energy sector makes that assumption shakier
  over long horizons.
- The dataset is national. It carries no company-level figures, so nothing here
  describes EVNGENCO3's own emissions directly — only the context it operates in.
- Industrial output and generation mix are absent, which limits how far the
  drivers of emissions can be separated.

Integrating national data from Vietnam's Ministry of Industry and Trade, and
applying time-series models, would be the next step.

## Files

```
├── analysis.qmd     # Quarto source: code, charts and written analysis
├── analysis.html    # Rendered report
└── README.md
```

## Reproducing

Requires R and Quarto.

```r
install.packages(c("tidyverse", "ggplot2", "scales",
                   "countrycode", "knitr", "kableExtra"))
```

Place `owid-co2-data.csv` in the same folder, then render:

```bash
quarto render analysis.qmd
```

## References

International Energy Agency (2023). *CO₂ emissions by region and sector*.
https://www.iea.org/data-and-statistics

World Bank (2024). *CO₂ emissions (kt) — Vietnam*.
https://data.worldbank.org/indicator/EN.ATM.CO2E.KT?locations=VN

## AI usage

Generative AI tools were used for code debugging and formatting help only.
All analysis, interpretation and conclusions are my own. Full details are
recorded in the acknowledgements section of the report.
