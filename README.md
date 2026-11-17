# Singapore HDB Resale Price Analysis

**R � Quarto � tidyverse � ggplot2 � Data validation � Exploratory analysis**

A Singapore Institute of Technology academic team project for **AAI1001: Data Engineering and Visualisation**, Group 15. The project investigates HDB resale price distributions across flat types and compares mature and non-mature estates.

The aim is to look beyond a headline average or median: how widely do prices vary, and what does the distribution reveal about different housing categories?

## My contribution

I am **Daryl Lai Weng Hong**. This repository originated under my previous GitHub account, [DRLLWH](https://github.com/DRLLWH/aai1001_proj); my current account is [StocialAbyss](https://github.com/StocialAbyss).

- The team's proposal assigns me **validation and metrics generation**, including median and interquartile-range measures.
- My recorded commits include adding the R analysis source in `aai.qmd`, updating the proposal, and contributing presentation material explaining the problem and the limitations of headline prices.
- This is shared team work. Committing an analysis file does not mean I independently authored every transformation, plot or forecasting component. The proposal assigns data visualisation and storytelling to Zulhilmi.

## Data and analytical workflow

The analysis source combines HDB resale transaction records with a town-level estate maturity lookup. It includes:

1. Parsing transaction dates, storey ranges and remaining lease information.
2. Calculating price per square metre and checking transaction counts by flat type.
3. Joining a normalised town key to the estate maturity lookup.
4. Checking missing values before analysis.
5. Comparing prices by flat type and estate maturity.

Data files are in `data/`. Consult the proposal for the original transaction-data reference. The maturity lookup is team-researched and should be treated separately from the official transaction source.

## Visualisations in the analysis source

| Visualisation | Analytical purpose |
| --- | --- |
| Transaction-count bar chart | Check sample representation across flat types before filtering. |
| Violin plots with boxplot overlays | Compare price distributions, medians and spread between estate categories. |
| Lease-versus-price-per-square-metre scatterplots | Explore the relationship between remaining lease and unit price within flat types. |
| Historical median prices and ARIMA forecast | Explore time-series patterns with prediction intervals; not a validated investment forecast. |

See [`aai.qmd`](aai.qmd) for the plotting code. This portfolio copy does not yet include newly rendered screenshots of those R charts.

**Attribution:** `images/visualisation.jpg` is a third-party Tableau visualisation used as design inspiration in the proposal. It is not a chart created by me or our team. Its original source is credited in the proposal.

## Files and reproduction

- `aai.qmd`: R data-preparation and plotting source.
- `AAI1001Grp15_ProjectProposal.qmd` / `.html`: project rationale, sources, proposed responsibilities and AI-use reflection.
- `revealjs_presentation_sample.qmd` / `.html`: presentation material; several sections remain placeholders.
- `aai1001_proj.Rproj`: R project file.

Open the R project and inspect `aai.qmd` in an R-capable editor, such as RStudio. Required R packages used by the analysis include `tidyverse`, `lubridate`, `forecast`, `readxl` and `scales`. Run from the repository root so the `data/` paths resolve. The current QMD declares a Jupyter R kernel; rendering also requires a matching execution environment or an intentional conversion to knitr.

These are source-based reproduction notes; a fresh end-to-end execution has not been verified for this portfolio copy.

## Scope and limitations

- The repository contains implemented R analysis code alongside proposal and unfinished presentation material. It should not be presented as a fully polished final submission.
- Observed differences between estate categories do not establish a causal effect of estate maturity.
- Filtering flat categories changes the population represented by the charts.
- The forecast source does not by itself establish out-of-sample forecasting performance.

## Team and provenance

Group 15: Ming Yang, Zi Xin, Desmond, Daryl and Zulhilmi. The proposal records responsibilities for ingestion, cleaning, joining, validation, metrics and visualisation. Original repository: [DRLLWH/aai1001_proj](https://github.com/DRLLWH/aai1001_proj).

The team's proposal discloses AI assistance with wording, R syntax, troubleshooting and visualisation suggestions, with team review of the outputs. That assistance is distinct from the subject matter of this analytical project.
