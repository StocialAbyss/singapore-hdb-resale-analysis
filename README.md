# Singapore HDB Resale Price Analysis

**R | Quarto | tidyverse | ggplot2 | Exploratory data analysis**

An academic team project for **AAI1001: Data Engineering and Visualisation** at the Singapore Institute of Technology.

The project explores how HDB resale prices are distributed across flat types and how those distributions differ between mature and non-mature estates. It combines data preparation, validation and visualisation to explain more than a single headline price.

## What question does the project answer?

A median resale price summarises the middle transaction, but it does not show how tightly prices cluster, how far they spread, or whether distinct groups are being mixed together.

This project examines:

- How transaction volumes differ across flat types.
- How price distributions compare between mature and non-mature estates.
- How remaining lease relates to price per square metre.
- How monthly median prices change over time.

## 1. Start with the original visualisation

![Reference Tableau heatmap showing HDB resale price distributions by flat type](images/visualisation.jpg)

**Reference visualisation:** this heatmap comes from the [Singapore HDB Resale Tableau dashboard credited in the proposal](https://public.tableau.com/app/profile/fshih/viz/SingaporeHDBResale/HDBresale). It is the project's starting point for critique, not an output created by the project team.

The horizontal axis separates flat types, the vertical axis shows resale prices, and the colour intensity highlights concentrations of transactions. It provides a quick impression of common price ranges and unusually expensive transactions.

The redesign aims to make the statistical comparison clearer: show the median and interquartile range explicitly, and separate mature from non-mature estates rather than combining them in one distribution.

## 2. Prepare and combine the data

![Project workflow from resale transactions through cleaning, joining, aggregation, visualisation and analysis](images/workflowdataengineering.jpg)

The project combines the resale transaction CSV with a team-compiled estate maturity lookup.

| Step | What the code does | Why it matters |
| --- | --- | --- |
| Read the sources | Load transaction records and the maturity spreadsheet. | Bring transaction-level prices and estate categories together. |
| Parse dates | Convert transaction months into dates and extract year/month fields. | Support monthly grouping and trend analysis. |
| Transform fields | Extract storey-range information and convert remaining lease into numeric years. | Make text fields usable for numerical analysis. |
| Calculate unit price | Divide resale price by floor area. | Compare prices on a per-square-metre basis. |
| Inspect coverage | Count transactions by flat type before filtering. | Identify categories with limited representation. |
| Join the lookup | Standardise estate names in the lookup and join on town. | Add mature/non-mature classification to transactions. |
| Validate | Count missing values across the enriched dataset. | Identify gaps that could affect interpretation. |

The comparison plots focus on **3-room, 4-room, 5-room and executive flats**. Filtering changes the scope of the analysis; the results should be read as comparisons within those selected categories.

## 3. Explore the distributions and relationships

The following plots are implemented in [`aai.qmd`](aai.qmd). The repository currently contains their R source rather than saved result images.

### Transaction volume by flat type

A bar chart counts transactions in each flat category before filtering.

**How to read it:** taller bars indicate more recorded transactions. This is a data-coverage check, rather than a direct measure of demand: transaction counts also depend on the housing stock and the period covered.

### Resale price distributions by estate maturity

Violin plots compare mature and non-mature estates within each flat type, with boxplots overlaid. The source includes both side-by-side and split-violin versions.

**How to read it:**

- The width of a violin shows where prices are more concentrated.
- The box shows the middle 50% of transactions.
- The line inside the box marks the median.
- Points beyond the whiskers highlight statistical outliers.

This combines distribution shape with familiar statistical landmarks. It helps examine whether groups differ in their central price, spread or high-price tail without assuming that estate maturity causes those differences.

### Remaining lease versus price per square metre

A scatterplot places remaining lease on the horizontal axis and price per square metre on the vertical axis. Separate panels show different flat types, while colour identifies estate maturity.

Faint points reduce the effect of overlapping observations. Linear trend lines summarise the relationship within groups, allowing comparisons across flat types. They describe associations; location, transaction date and other factors may also influence price.

### Historical median prices and an ARIMA forecast

The code aggregates monthly median resale prices by estate maturity, then fits separate ARIMA models and forecasts the next 12 months.

Solid lines represent historical values, dashed lines represent forecasts, and shaded bands show 95% prediction intervals. These intervals communicate uncertainty. The source does not establish out-of-sample forecasting performance, so this is an exploratory extension of the analysis.

## 4. Read or run the project

| File | Purpose |
| --- | --- |
| [`aai.qmd`](aai.qmd) | Data preparation, checks and plotting code. |
| [Project proposal](AAI1001Grp15_ProjectProposal.qmd) | Motivation, sources, visualisation critique and design rationale. |
| `AAI1001Grp15_ProjectProposal.html` | Rendered proposal; download to view locally. |
| `revealjs_presentation_sample.qmd` | Presentation source, including unfinished sections. |
| `data/` | Resale transactions and estate maturity lookup. |
| `aai1001_proj.Rproj` | R project file. |

Use R with `tidyverse`, `lubridate`, `forecast`, `readxl` and `scales`. Run analysis chunks from the repository root so the relative data paths resolve. The QMD currently declares a Jupyter R kernel; Quarto rendering requires that environment, or an intentional change to an R/knitr configuration.

## Interpretation and scope

The project demonstrates how joining contextual data and choosing suitable charts can support a clearer comparison of housing prices. The maturity lookup is team-compiled, filtered categories limit coverage, and price differences should not be treated as causal effects. Proposal and presentation files remain alongside the implemented analysis source.

## Team and source

**Group 15:** Ming Yang, Zi Xin, Desmond, Daryl and Zulhilmi.

Original repository: [DRLLWH/aai1001_proj](https://github.com/DRLLWH/aai1001_proj). The proposal includes source attribution and a team AI-use reflection.
