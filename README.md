# House Price Prediction

## Project Overview

This project builds a **house-price prediction model** using a linear
regression approach. The workflow in the accompanying Jupyter notebook
loads a Boston housing dataset, explores its features, trains and
evaluates a regression model, and saves the trained model with Python's
pickle functionality.

## Objectives

-   Load and organize the housing dataset.
-   Explore descriptive statistics, missing values, and feature
    correlations.
-   Split the data into training and testing sets.
-   Standardize the input features.
-   Train a linear regression model to predict house prices.
-   Evaluate predictions with regression metrics.
-   Save and reload the trained model.

## Dataset

The notebook reads data from `boston_dataset.csv`. It treats the **last
column** as the target (`Price`) and the preceding columns as input
features.

The 13 feature names used in the notebook are:

  Feature     Description
  ----------- ------------------------------------------------------
  `CRIM`      Per-capita crime rate by town
  `ZN`        Proportion of residential land zoned for large lots
  `INDUS`     Proportion of non-retail business acres
  `CHAS`      Charles River dummy variable
  `NOX`       Nitric oxide concentration
  `RM`        Average number of rooms per dwelling
  `AGE`       Proportion of owner-occupied units built before 1940
  `DIS`       Weighted distance to employment centres
  `RAD`       Index of accessibility to radial highways
  `TAX`       Property-tax rate
  `PTRATIO`   Pupil--teacher ratio by town
  `B`         Feature named `B` in the dataset
  `LSTAT`     Feature named `LSTAT` in the dataset

*Note:* These descriptions provide context for the feature names; the
notebook itself defines the names but does not document all feature
definitions. Confirm that the CSV columns match the expected order
before running the notebook.

## Workflow

### 1. Load and prepare the data

The notebook uses pandas to read `boston_dataset.csv`, assigns the final
column to the target variable, and places the other columns in the input
data. It then creates a DataFrame with the listed feature names and a
`Price` column.

### 2. Explore the data

The exploratory analysis includes:

-   `describe()` for summary statistics.
-   `isnull().sum()` to count missing values.
-   `corr()` to inspect pairwise correlations.

The notebook contains these checks but does not provide recorded results
in the source file.

### 3. Split into training and test sets

The data is split with `train_test_split` using:

-   **Test size:** 30%
-   **Random state:** 42

The fixed random state makes the split reproducible under the same data
and environment.

### 4. Standardize features

`StandardScaler` is fitted on the training features. The same fitted
scaler is then applied to the test features, avoiding fitting the scaler
separately on the test set.

### 5. Train the model

The notebook fits scikit-learn's `LinearRegression` model on the
standardized training features and training target. It also retrieves
the model coefficients and intercept and prints a regression equation.

Because the features are standardized, the coefficients correspond to
the standardized feature values rather than the original feature units.

### 6. Generate predictions and evaluate

The trained model predicts prices for the test set. The notebook
calculates these metrics:

  -----------------------------------------------------------------------
  Metric                              Purpose
  ----------------------------------- -----------------------------------
  Mean Absolute Error (MAE)           Average absolute difference between
                                      actual and predicted values

  Mean Squared Error (MSE)            Average squared prediction error

  Root Mean Squared Error (RMSE)      Square root of MSE, expressed in
                                      the target's units

  R² score                            Measures how much target variation
                                      is explained by the model relative
                                      to a mean-baseline model

  Adjusted R²                         Adjusts R² based on sample size and
                                      number of predictors
  -----------------------------------------------------------------------

The notebook does not include the resulting metric values in its saved
source, so model performance cannot be stated from the notebook code
alone.

### 7. Save and reload the model

The final section attempts to serialize the trained regression model to
`regmodel.pkl` and load it again. This supports reuse of the fitted
estimator without retraining, provided the save/load code executes
successfully.

For future predictions, the fitted `StandardScaler` should also be saved
and reused. New input rows must be transformed with that same scaler
before being passed to the regression model.

## Technologies

-   **Python**
-   **pandas** --- data loading and DataFrame operations
-   **NumPy** --- numerical operations
-   **Matplotlib** --- imported for plotting
-   **scikit-learn** --- data splitting, feature scaling, linear
    regression, and evaluation metrics
-   **pickle** --- model serialization

## How to Run

1.  Place `house_pricing_prediction.ipynb` and `boston_dataset.csv` in
    the appropriate working directory.

2.  Install the dependencies if they are not already available:

    ``` bash
    pip install pandas numpy matplotlib scikit-learn jupyter
    ```

3.  Start Jupyter:

    ``` bash
    jupyter notebook
    ```

4.  Open `house_pricing_prediction.ipynb` and run the cells in order.

## Implementation Notes

The notebook's model-saving cell contains `import Pickle` but later uses
the lowercase name `pickle`. Python module names are case-sensitive, so
this should normally be changed to:

``` python
import pickle
```

The data-loading step also assumes the target is the last CSV column and
that the remaining columns are in the expected feature order. Verify
these assumptions when using a different copy of the dataset.

To make the workflow more reproducible, consider saving both the scaler
and regression model together (for example, in a scikit-learn
`Pipeline`) and adding checks for missing values, unexpected columns,
and invalid input data.

## Limitations

-   The notebook does not include saved output values for the evaluation
    metrics.
-   It does not document a separate validation set or
    hyperparameter/model comparison.
-   Linear regression captures linear relationships and may not
    represent every relationship in housing data.
-   The source notebook alone does not establish how well the model
    generalizes to new data.
-   The dataset's provenance, licensing, and intended use are not
    documented in the notebook.

## Project Structure

``` text
.
├── house_pricing_prediction.ipynb
├── boston_dataset.csv
├── regmodel.pkl          # created when model serialization succeeds
└── README.md             # this project description
```

## Summary

This project demonstrates a basic end-to-end regression workflow:
loading housing data, exploring features, standardizing inputs, fitting
linear regression, evaluating predictions, and attempting to serialize
the model. The reported performance should be determined by running the
notebook successfully and reviewing its metric outputs.
