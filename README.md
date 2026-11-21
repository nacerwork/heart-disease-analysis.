## Heart Disease Dataset: Exploration, Clustering and Modelling

An end-to-end data science analysis of the Cleveland heart-disease dataset (`Heart.csv`: 303 patients, 13 clinical variables plus the `AHD` diagnosis label), built as a course assignment in Python.

## What I did

**1. Data cleaning**
- Dropped the unnamed index column, removed rows with missing values (4 in `Ca`, 2 in `Thal`), leaving 297 patients.
- Converted the target `AHD` from Yes/No to 1/0, `Ca` from float to int, and stripped whitespace in string columns.

**2. Exploration and association analysis**
- Descriptive statistics and a PairGrid of the continuous variables.
- Pearson, Spearman and distance-correlation heatmaps, with a recommended metric for each variable pair.
- A mixed-type association matrix (Spearman, correlation ratio, Cramér's V).
- Predictive Power Score (PPS) compared with conventional correlation to look at directional association.

**3. Target selection**
- Chose `MaxHR` (maximum heart rate during the exercise test) as the continuous target.
- Selected predictors with forward selection under repeated 5-fold cross-validation and checked VIF.

**4. Dimensionality reduction and clustering**
- 3D PCA (the first 3 components explain only about 41% of the variance).
- 3D UMAP followed by HDBSCAN, which found 5 compact patient clusters.
- Cluster profiles and an ANOVA showing `MaxHR` differs between clusters (F = 13.8, p ≈ 2e-10).
- The clusters turned out to be driven mainly by categorical variables (`ChestPain`, `Thal`).

**5. Modelling `MaxHR`**
- Compared a linear model with random-forest scenarios (R², RMSE, MAE, residual KDEs, predicted-vs-actual plots, cluster-coloured diagnostics).
- The linear model performed best (test R² ≈ 0.35). A random forest on the same variables overfit badly, and one on all features reached R² ≈ 0.28.

**6. Simpson's paradox check**
- Compared pooled and within-cluster correlations. No convincing paradox was found; the main effect was attenuation of relationships inside clusters.

## Key findings
- `MaxHR` is only moderately predictable from this clinical data (R² ≈ 0.3–0.35).
- The strongest drivers are the disease label, exercise angina, ST-slope, `Oldpeak` and age.
- Cluster membership helps interpret patient groups but does not improve predictions.

## Tools
Python, pandas, NumPy, SciPy, scikit-learn, seaborn/matplotlib, UMAP, HDBSCAN, ppscore

## Files
- `Heart_Analysis.ipynb`: full notebook
- `Heart_Analysis.html`: rendered version
