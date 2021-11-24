# Do not overfit! II 

The dataset provided is a 20000 <a href="https://www.codecogs.com/eqnedit.php?latex=\times" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\times" title="\times" /></a> 300 matrix, where both the predictor variables and the target variable are anonymized

|    | rows      | columns | dtypes | memory usage|
| -- | ----------- | ----------- | -- | -- |
| train.csv   | 250      | 301       | `float64` | 588.0 KB |
| test.csv   | 19750   | 300        | `float64` | 45.2 MB |

the target variable 

<a href="https://www.codecogs.com/eqnedit.php?latex=y_n&space;\in&space;[0,1]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_n&space;\in&space;[0,1]" title="y_n \in [0,1]" /></a>

only takes binary inputs which is what makes it a *classification task*.

# Summary

- Since there were too many variables to be visually inspected for outliers, automatic outlier identification techniques (IsolationForest, EllipticEnvelope, OneClassSVM) have been employed. EllipticEnvelope provided a best improvement on the score by removing the least number of rows.
- In order to address the issue of imbalanced distribution of classes, a range of oversampling techniques have been applied. Out of 4 techniques (SMOTE, BorderlineSMOTE, SVMSMOTE and ADASYN), ADESYN led to the best cross-validation results. None of the techniques affected the results on public leaderboard.
- I used a range of models that differ in complexity in order to put the hypothesis that the simpler models should perform better to test. While simpler models (Logistic Regression and GaussianNB) did outperform models such as Random Forest, the trend to overfit has been similar both with respect to simple and complex models.
- PyCaret was used to provide a perspective on how does our selection of models fare with respect to a larger range of models. It can be seen that models I selected outperformed most of the others models implemented by PyCaret.
- The least succesful part of our project is that of feature selection as Rasgo which we used for calculating feature importances and dropping the least important features produced different results on each run. We have attempted to circumvent this problem by taking a union of features which have been selected for removal over the course of several runs. This way, we have reduced our feature space in half.
- Out of all the attempts in our feature engineering part, only second-degree polynomials of the features that were found to be most important proved beneficial towards the score. Neither feature crosses nor polynomials of a higher degree led to any improvements. At this point we have reached the required score of `0.8` on public Kaggle leaderboard.
- Lasso gave the best score (`8.36`) and also helped us to reach the required score on private scoreboard. This is most likely due to the fact that Lasso implements `l1` regularization which brings the coefficients for the least important features to `0`, thus zeroing out their constribution in predictions. While this means that we were not succesful in identifying the list of features the removal of which would have lead to the highest score, this is surprising since we have also implemented `l1` regularization when using Logistic Regression.

# Technologies
- `scikit-learn`
- `numpy`
- `pycaret`
- `pyrasgo`
- `imblearn`
- `collections`
- `eli5`
- `scipy`
- `missingno`
- `seaborn`
- `matplotlib`
- `pandas`

# Licence

The project is licenced under [MIT Licence]()

# Contact

tvirbickas@gmail.com
