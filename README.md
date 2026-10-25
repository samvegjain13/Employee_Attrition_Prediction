# Employee Attrition Analysis and Prediction

This project analyzes employee attrition in the included HR dataset and compares three classification models for identifying employees labeled as having left. The work is provided as a Jupyter notebook, with generated charts and a written summary.

## Project contents

- `analysis_1.ipynb` — data loading, preprocessing, exploratory analysis, model training and evaluation, charts, and HR recommendations.
- `WA_Fn-UseC_-HR-Employee-Attrition.csv` — dataset used by the notebook.
- `charts/` — five chart images produced by the analysis.
- `summary_1.docx` — a written summary of findings and recommendations.

## Dataset

The notebook identifies the data as the IBM HR Analytics employee attrition dataset. The included CSV contains 1,470 records and 35 columns, with `Attrition` as the target (`Yes` or `No`). The notebook reports 237 `Yes` records (16.1%) and 1,233 `No` records (83.9%).

The archive does not include a separate citation or download link for the dataset, so its original publication/source URL is not verified here.

## Analysis and methodology

The notebook covers:

1. Dataset inspection and class distribution.
2. Missing-value checks, removal of four columns (`EmployeeNumber`, `Over18`, `StandardHours`, and `EmployeeCount`), target encoding, one-hot encoding of categorical variables, and feature scaling.
3. Exploratory comparisons of attrition by department, job role, monthly income, work-life balance, and tenure.
4. Training and comparison of Logistic Regression, Random Forest, and Gradient Boosting classifiers.
5. Evaluation with precision, recall, F1-score, ROC-AUC, a classification report, and a confusion matrix.
6. Five visualizations and written HR recommendations.

The notebook uses an 80/20 train/test split with `random_state=42` and stratification by the target. It fits `StandardScaler` on the full feature matrix before making the split. This allows information from the eventual test set to influence preprocessing; the reported test metrics may therefore be optimistic. For a leakage-safe re-evaluation, split first and fit preprocessing only on the training data (ideally with a scikit-learn pipeline).

## Recorded results

The saved notebook output selects Logistic Regression as the best model by ROC-AUC:

| Model | Precision | Recall | F1-score | ROC-AUC |
| --- | ---: | ---: | ---: | ---: |
| Logistic Regression | 0.3412 | 0.6170 | 0.4394 | 0.7986 |
| Random Forest | 0.3750 | 0.0638 | 0.1091 | 0.7519 |
| Gradient Boosting | 0.5882 | 0.2128 | 0.3125 | 0.7941 |

These are the outputs saved in the notebook, not independently reproduced results. They are based on one train/test split and should be treated as an initial comparison rather than evidence of performance on future employees.

The exploratory analysis reports an overall attrition rate of 16.1%, a 20.6% rate in Sales, and a 39.8% rate for Sales Representatives. It also reports a mean monthly income difference of 2,046 between employees who left and those who stayed. The notebook formats income values with a rupee symbol, but the dataset's currency is not established in the included files; the difference is therefore stated without a currency in this README.

## Requirements

Imports in the notebook show use of:

- Python
- pandas
- NumPy
- Matplotlib
- seaborn
- scikit-learn

No dependency manifest or pinned package versions are included in the archive, so exact versions are unknown.

## Running the notebook

Open `analysis_1.ipynb` in Jupyter or Google Colab. Before running it, update the dataset-loading cell to use the CSV's location in your environment. The saved notebook currently reads from the Google Colab path `/content/WA_Fn-UseC_-HR-Employee-Attrition.csv`; it creates a `charts/` directory relative to the notebook when generating figures.

The archive does not specify tested Python or package versions, nor does it include a requirements file. Install compatible versions of the packages listed above in your chosen notebook environment.

## Limitations

- The target classes are imbalanced: 16.1% of records are labeled as attrition.
- The notebook scales features before the train/test split, creating potential data leakage in evaluation.
- Results are saved outputs from one split and are not independently verified here.
- The notebook includes demographic features and recommends fairness review before any HR use. Predictions should not be treated as certainty or used as the sole basis for employment decisions.
- The notebook proposes HR actions based on associations in this dataset; those associations do not establish cause and effect.

