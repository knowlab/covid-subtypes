# Identifying COVID-19 Subtypes via a Multi-dimensional Space

## Technical details

### Table 1. Random Forest classifcation configurations: hyperparameters and sampling coefficients. The down/upsampling coefficients are relative to the number of individuals in the most numerous class.

| Clustering                                                                                | Hyperparameters                                                                               | Downsampling co-efficient | Upsampling co-efficient |
|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------|-------------------------|
| Baseline KModes Binary                                                                    | n estimators=40, max depth=None, max features=‘sqrt’, min samples split=10, criterion=‘ gini’ | 0.6                       | 0.8                     |
| Baseline KModes Multiclass                                                                | n estimators=60, max depth=10, max features=‘sqrt’, min samples split=10, criterion=‘ gini’   | 1                         | 0.8                     |
| Layered Axes KModes Layer 1                                                               | n estimators=30, max depth=10, max features=‘log2’, min samples split=2, criterion=‘ entropy’ | 1                         | 0.8                     |
| Layered Axes KModes Layer 2, Cluster 0                                                    | n estimators=20, max depth=None, max features=‘sqrt’, min samples split=10, criterion=‘ gini’ | 1                         | 0.8                     |
| Layered Axes KModes Layer 2, Cluster 1                                                    | n estimators=20, max depth=5, max features=‘sqrt’, min samples split=10, criterion=‘gini’     | 1                         | 0.8                     |
| n estimators=20, max depth=5, max features=‘sqrt’, min samples split=10, criterion=‘gini’ | n estimators=15, max depth=None, max features=‘log2’, min samples split=2, criterion=‘ gini’  | 1                         | 0.8                     |
| Prognosis Space DBScan                                                                    | n estimators=60, max depth=15, max features=‘log2’, min samples split=2, criterion=‘ entropy’ | 1                         | 0.8                     |
