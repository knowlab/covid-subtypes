# Identifying COVID-19 Subtypes via a Multi-dimensional Space

## Technical details

### Table 1. Random Forest classifcation configurations: hyperparameters and sampling coefficients. The down/upsampling coefficients are relative to the number of individuals in the most numerous class.

| Clustering                                                                                | Hyperparameters                                                                               | Downsampling co-efficient | Upsampling co-efficient |
|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------|-------------------------|
| Baseline KModes Binary                                                                    | criterion='entropy', max_depth=10, min_samples_split=5, n_estimators=15               | 0.6                       | 0.8                     |
| Baseline KModes Multiclass                                                                | n estimators=60, max depth=10, max features=‘sqrt’, min samples split=10, criterion=‘ gini’   | 1                         | 0.8                     |
| Layered Axes KModes Layer 1                                                               | n estimators=30, max depth=10, max features=‘log2’, min samples split=2, criterion=‘ entropy’ | 1                         | 0.8                     |
| Layered Axes KModes Layer 2, Cluster 0                                                    | n estimators=20, max depth=None, max features=‘sqrt’, min samples split=10, criterion=‘ gini’   | 1                         | 0.8                     |
| Layered Axes KModes Layer 2, Cluster 1                                                    | n estimators=20, max depth=5, max features=‘sqrt’, min samples split=10, criterion=‘gini’    | 1                         | 0.8                     |
| Layered Axes Kmodes Layer 2, Cluster 2                                                    | n estimators=15, max depth=None, max features=‘log2’, min samples split=2, criterion=‘ gini’    | 1                         | 0.8                     |
| Layered Axes KModes Layer 2, Severe Patients                                              | criterion='entropy', max_depth=10, min_samples_split=5, max_features='sqrt',  n_estimators=5 | 1                  | 0.8                     |
| Prognosis Space DBScan                                                                    | n estimators=60, max depth=15, max features=‘log2’, min samples split=2, criterion=‘ entropy’ | 1                         | 0.8                     |
| Prognosis Space DBScan, Severe Patients                                                   | max_depth=15, min_samples_split=10, n_estimators=20, criterion='gini', max features = 'auto' | 1               | 0.8                     | 

### Prognosis Space Dimension Reduction Function 
The Dimension Reduction function we used takes the form: \
![](dim_red_function.png) \
* f_1 is computed by:
```
d_1 = 0
for chapter_presence, weight in zip([Nervous, Abnormal, Musculoskeletal, Circulatory, Digestive, Nutritional, Genitourinary, Respiratory, Blood/Immune], [0.5, 0.5, 0, 0.75, 0, 0, 0, 0.75, 0.5]):
  d_1 += chapter_presence*weight
```

* f_2 is computed by:
```
d_2 = 0
if (non-invasive oxygen) and (invasive oxygen):
  d_2 = 1.25
elif (invasive oxygen):
  d_2 = 1
elif (non-invasive oxygen):
  d_2 = 0.75
if (ECMO):
  d_2 += 0.5
```

* f_3 is computed by:
```
d_3 = 0
if (death):
  # this includes death and (death and icu)
  d_3 = 1.5
elif (icu):
  d_3 = 1
```

* f_4 is computed by:
```
d_4 = 0
if (los >= 14) and (los < 28):
  d_4 = 0.5
elif (los >= 28):
  d_4 = 0.75
```

The Prognosis Space approach, including the dimension reduction functions are implemented in [2c Prognosis Space DbScan](2c_Prognosis_Space_DbScan.ipynb).
