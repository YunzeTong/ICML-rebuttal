# Investigation on how our method could work with tree-based ensembles

We conducted an additional experiment employing three tree-based models to assess whether our sample weights improve models' robustness beyond neural networks. The results are listed as follow:

|                 | Adult         |               | Default       |               | Phishing      |               | Taxi (NYC)    |               |
| --------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
|                 | Worst         | Mean          | Worst         | Mean          | Worst         | Mean          | Worst         | Mean          |
| catboost        | 0.501 ± 0.009 | 0.754 ± 0.002 | 0.318 ± 0.004 | 0.647 ± 0.003 | 0.972 ± 0.001 | 0.976 ± 0.001 | 0.670 ± 0.002 | 0.813 ± 0.004 |
| catboost + JTT  | 0.489 ± 0.004 | 0.751 ± 0.001 | 0.314 ± 0.010 | 0.643 ± 0.001 | 0.959 ± 0.008 | 0.977 ± 0.005 | 0.673 ± 0.010 | 0.815 ± 0.007 |
| catboost + ours | 0.646 ± 0.003 | 0.793 ± 0.001 | 0.334 ± 0.003 | 0.652 ± 0.008 | 0.972 ± 0.002 | 0.981 ± 0.001 | 0.676 ± 0.010 | 0.812 ± 0.006 |
| LightGBM        | 0.503 ± 0.007 | 0.758 ± 0.003 | 0.320 ± 0.004 | 0.650 ± 0.002 | 0.961 ± 0.001 | 0.972 ± 0.001 | 0.684 ± 0.010 | 0.817 ± 0.003 |
| LightGBM + JTT  | 0.490 ± 0.010 | 0.753 ± 0.003 | 0.319 ± 0.009 | 0.650 ± 0.004 | 0.966 ± 0.003 | 0.981 ± 0.001 | 0.686 ± 0.016 | 0.819 ± 0.005 |
| LightGBM + ours | 0.603 ± 0.000 | 0.795 ± 0.001 | 0.349 ± 0.007 | 0.660 ± 0.005 | 0.966 ± 0.002 | 0.979 ± 0.001 | 0.698 ± 0.007 | 0.824 ± 0.008 |
| XGBoost         | 0.508 ± 0.017 | 0.751 ± 0.004 | 0.319 ± 0.010 | 0.638 ± 0.008 | 0.967 ± 0.004 | 0.971 ± 0.004 | 0.693 ± 0.031 | 0.817 ± 0.012 |
| XGBoost + JTT   | 0.494 ± 0.005 | 0.746 ± 0.001 | 0.320 ± 0.005 | 0.639 ± 0.003 | 0.963 ± 0.001 | 0.976 ± 0.001 | 0.693 ± 0.015 | 0.813 ± 0.002 |
| XGBoost + ours  | 0.649 ± 0.004 | 0.789 ± 0.002 | 0.342 ± 0.002 | 0.648 ± 0.007 | 0.966 ± 0.004 | 0.980 ± 0.003 | 0.691 ± 0.017 | 0.815 ± 0.005 |

The above table presents results on four datasets. For a comprehensive comparison, we also evaluated the JTT method using these tree-based models. Results indicate that our approach consistently enhances worst-group accuracy across base models, particularly for LightGBM. In contrast, JTT, a boundary-based method discussed in Section 1, improves robustness inconsistently, performing well only on certain datasets or base models. This finding supports our earlier observation of boundary-based methods—they rely solely on decision boundaries, which are disconnected from training distributions, leading to unstable robustness improvements. Conversely, our score-based strategy effectively captures distributional imbalance, generating reliable weights to enhance worst-group accuracy. These results further confirm our method's effectiveness with tree-based models.
