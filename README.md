# ICDS supervised learning labs

Practical Python and scikit-learn typing labs for the ICDS Introduction to Machine Learning course.

## Topic 4 · Regression

The regression notebook uses historical automobile data to predict city fuel efficiency (`mpg`) and guides learners through a complete workflow:

- Preparing and inspecting a regression dataset
- Establishing a mean baseline
- Simple linear regression
- Multiple linear regression
- Polynomial regression
- Decision-tree regression
- Random-forest regression
- Cross-validation and model comparison
- Introductory hyperparameter tuning
- Final held-out testing
- Prediction visualisation and residual analysis
- Interpreting metrics, coefficients, and modelling assumptions

## Repository contents

| File | Description |
|---|---|
| [`ICDS_Topic_4_Regression_Typing_Lab.ipynb`](./ICDS_Topic_4_Regression_Typing_Lab.ipynb) | Guided typing lab with prompts, hints, checkpoints, code cells, plots, and reflection questions |
| [`ICDS_Topic_4_5_Regression_Classification_Typing_Lab.ipynb`](./ICDS_Topic_4_5_Regression_Classification_Typing_Lab.ipynb) | Paired regression and classification lab using e-commerce delivery outcomes |

The notebook creates its teaching dataset (`auto_mpg.csv`) from an embedded copy when the setup cell is run. No separate dataset download is required.

## Topics 4–5 · Regression and classification

The comparison notebook uses the same completed orders and predictors for both tasks:

- **Regression:** estimate elapsed days from purchase to delivery.
- **Classification:** predict whether delivery was later than promised.

It guides learners through defining targets and features, splitting data, fitting preprocessing only on training data, comparing task-specific metrics, and timing model fits. Classification results include precision, recall, F1 and a confusion matrix because late deliveries are less common than on-time deliveries.

### Data setup

The notebook needs these two Olist CSV files in the `data/` folder:

- `olist_orders_dataset.csv`
- `olist_customers_dataset.csv`

Only the orders table and customer state are used. The raw CSV files are not included in Git. Download the [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) and copy those files into `data/`. See [`data/README.md`](./data/README.md) for details.

Launch Jupyter from the repository root and open the comparison notebook. In Google Colab, upload the notebook and the two CSV files, then put the files in a folder named `data` beside the notebook before running it. The notebook's cells marked `TYPE` are learner exercises and are intentionally incomplete.

The Olist records are historical and the lab includes delivered orders only. The notebook excludes actual delivery fields from its predictors because they are only known after the outcome. Cite the dataset when reusing the material and check its terms before redistributing the source files.

## Learning outcomes

By completing the lab, you should be able to:

1. Distinguish regression problems from classification problems.
2. Prepare predictors and a continuous target for modelling.
3. Train and generate predictions from several regression models.
4. Use pipelines to handle missing values and scaling safely.
5. Evaluate models using MAE, MSE, RMSE, and R².
6. Compare models using cross-validation.
7. Tune a model with a small grid search.
8. Use actual-versus-predicted and residual plots to diagnose errors.
9. Interpret results without confusing association with causation.

## How to use the notebook

### Option 1: Google Colab

1. Open [Google Colab](https://colab.research.google.com/).
2. Select **File → Upload notebook**.
3. Upload `ICDS_Topic_4_Regression_Typing_Lab.ipynb`.
4. Run the setup cell once, then work through the notebook from top to bottom.

### Option 2: Local Jupyter

Install the required packages:

```bash
python -m pip install numpy pandas matplotlib scikit-learn jupyter
```

Launch Jupyter:

```bash
jupyter notebook
```

Open the notebook and run the cells in order. Cells marked `TYPE` are intentionally incomplete: write the code, run it, and use the checkpoint cells to verify selected requirements.

## Modelling workflow

The lab reserves 20% of the records as a final test set. The remaining training data are used for five-fold cross-validation and model selection. The test set remains closed until the final evaluation.

The main target is:

- `mpg`: city fuel efficiency in miles per gallon

The primary numeric predictors are:

- `weight`
- `horsepower`
- `displacement`
- `cylinders`
- `acceleration`
- `model_year`

The optional extension introduces `origin` as a categorical predictor using one-hot encoding. `car_name` is excluded from the main modelling workflow.

## Evaluation metrics

- **MAE:** average absolute error in MPG; easy to interpret and a useful default when errors should count approximately equally.
- **MSE:** average squared error in MPG²; useful for optimisation and analysis, but less intuitive to communicate.
- **RMSE:** error in MPG with extra emphasis on large mistakes; useful when unusually large errors are especially costly.
- **R²:** compares the model with a mean-only baseline; useful as supporting context, but it is not an absolute error measure and can be negative.

For this lab, compare **MAE and RMSE together**, check performance against the baseline, and use R² as additional context. If MAE and RMSE disagree, inspect the largest residuals and consider whether large errors matter for the application.

## Modelling assumptions and limitations

For linear regression, inspect whether:

- Relationships are reasonably linear.
- Observations are independent.
- Residuals have a roughly constant spread.
- Residuals show no strong patterns or unusual outliers.
- Strong multicollinearity makes individual coefficients unstable.
- Missing values are handled using training data only.

Tree and forest models do not require the same linearity assumptions, but residual diagnostics and careful validation remain important.

This is a historical teaching dataset. It supports learning regression workflows, not reliable predictions for modern vehicles. Random train/test splitting may also be optimistic when records are related by manufacturer, model, or time period.

## Data provenance

The embedded data are based on the **Auto MPG** dataset from the UCI Machine Learning Repository:

- Quinlan, R. (1993), [Auto MPG](https://archive.ics.uci.edu/dataset/9/auto+mpg)
- DOI: [10.24432/C5859H](https://doi.org/10.24432/C5859H)
- Dataset licence: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

The notebook documents the preparation process and keeps the original missing horsepower values available for pipeline-based imputation.

## Reproducibility

The notebook uses fixed random seeds for the train/test split, cross-validation, tree, and forest models. Results may vary slightly across Python, NumPy, pandas, and scikit-learn versions.
