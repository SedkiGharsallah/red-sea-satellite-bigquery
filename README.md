# Red Sea: 18 years of satellite ocean data with BigQuery

Analysis of **sea surface temperature (SST)** and **sea surface height (SSH)** in the Red Sea
from daily satellite observations (1998–2015, ~150 GB database), queried with **BigQuery (SQL)
on Google Cloud** from Google Colab, then analysed with Python and scikit-learn.

Course project, IMT Atlantique (Big Data & Cloud).

## What the notebook does

1. **SST / SSH relationship** — monthly distributions (boxplots) and a per-location
   correlation map between SST and SSH.
2. **Trends** — linear regression, then a regression with a yearly seasonal cycle
   (`a·t + b·sin(ωt) + c·cos(ωt) + d`), significance tests and 95% intervals,
   and an extrapolation to 2050.
3. **Atypical years** — each year is described by its 12 monthly SST standard deviations;
   K-means (k=2) separates regular and atypical years, visualised with PCA.
4. **Spatial zoning** — each location is described by its monthly SST and SSH profiles (24 features);
   K-means (k=3) splits the Red Sea into three regions, and PCA maps show the main spatial patterns.

## Key results

| | Result |
|---|---|
| SST trend | **+0.015 °C / year** (p ≈ 0.001), i.e. about +0.15 °C per decade |
| SSH trend | **+5.1 mm / year** (p < 10⁻⁵⁰), i.e. about +5 cm per decade |
| SSH extrapolation | about **+17 cm** between 2016 and 2050 (linear trend, to be read with caution) |
| Atypical years (K-means) | 4 years stand out: 1998, 2000, 2001 and 2015 |
| Spatial zoning | 3 coherent regions along the north–south axis of the Red Sea |

1998 and 2015 are both strong El Niño years, which may explain part of their atypical SST
variability; this link is a hypothesis and was not tested here.

## Stack

SQL (BigQuery) · Google Cloud Platform · Google Colab · Python · pandas · NumPy · SciPy ·
scikit-learn (linear regression, K-means, PCA) · Matplotlib · Basemap

## Reproducibility

The data comes from a private BigQuery dataset provided for the course, so the notebook
cannot be re-run without access to it (`YOUR_GCP_PROJECT` replaces the original project ID).
All outputs, figures and maps are saved in the notebook.

## Notes and limitations

- In the K-means section, the labels "regular" / "atypical" were swapped in the original run
  and have been corrected in the code and printed results; the legend of the saved PCA figure
  still shows the old labels.
- The 2050 extrapolations assume a constant linear trend and are only indicative.
- Missing values are filled with the column mean before standardisation; more careful
  gap-filling could change the clustering slightly.
