# wetland-nitrogen-analysis

Environmental Engineering course project testing the hypothesis that
placing wetlands in high-nitrogen surplus watersheds achieves greater
watershed-scale N removal per unit area than random or uniform
placement. Using current wetland density and modeled N removal across
US HUC-8 watersheds, I test this by checking whether existing wetland
placement is targeted at high-surplus watersheds or is closer to random
with respect to N surplus. If wetland density is uncorrelated with N
surplus, then current wetlands behave like random placement, and
high-surplus watersheds are leaving N removal potential unused.

## Data
-File: 'fig2_source_data.csv'
- Source: Cheng, F.Y., Van Meter, K.J., Byrnes, D.K. & Basu, N.B.
  "Maximizing US nitrate removal through wetland protection and
  restoration." *Nature* 588, 625-630 (2020).
  https://doi.org/10.1038/s41586-020-03042-5
- Obtained from: Source Data Fig. 2 (`fig2_source_data.csv`)
- Unit of observation: HUC-8 watershed (n = 2,098)
- Variables used: wetland density (`wetland_density`), N surplus
  (`n_surplus`), percent N removal (`pct_n_removal`), estimated N
  removal (`est_n_removal`)
- Categorical variable for coloring:  USGS hydrologic region (HUC-2,
  18 regions), derived from the first two digits of the HUC-8 code

## Contents
| `01_describe.ipynb` | Mean, median, SD; histograms
| `02_correlation.ipynb` | Pearson/Spearman, linear regression, scatter plots
| `03_pca_kmeans.ipynb` | PCA, PC weights, k-means, PC1 vs PC2 plot
| `figures/` | All generated figures (main and supplementary)
| `requirements.txt` | Python dependencies

## How to run
1. `git clone https://github.com/heatherbackman/README.md.git`
2. `pip install -r requirements.txt`
3. Run notebooks 01 → 02 → 03 from the repo root.

Tested with Python kernel 3.

## Key findings
- Wetland density and N surplus basically aren't correlated across the
  2,098 watersheds (Pearson r=-0.005, Spearman ρ=0.26). So wetlands
  aren't really located where the nitrogen is.
- PC1 and PC2 together explain 91.2% of the variance. K-means with k=3
  (picked using silhouette score) gave three groups: wetland-rich
  watersheds (406), wetland-poor with low N surplus (1,361), and a
  high-N-surplus group (331). Most of the high-surplus group is in the
  Midwest, and most of the wetland rich group is in the Southeast.
- My hypothesis was supported. The high-surplus watersheds don't have
  more wetlands than average and they remove less of their N (26% vs 43%
  in the wetland-rich group), so targeting restoration there makes sense.
  One caveat is that percent N removal and estimated N removal come from
  the paper's model, so these are modeled values and not measurements.
