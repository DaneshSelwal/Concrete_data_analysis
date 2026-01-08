# Concrete Data Analysis

## 📌 Overview
This repository focuses on **Concrete Strength Prediction** and analysis using various machine learning algorithms, optimization techniques, and uncertainty quantification methods. The goal is to derive reliable insights and build robust models to predict the compressive strength of concrete based on its composition.

The project explores:
* **Hyperparameter Tuning:** Advanced optimization using Optuna, Grid Search, and Bayesian Optimization.
* **Model Explainability:** Understanding feature importance with SHAP and LIME.
* **Uncertainty Analysis:** Quantifying prediction confidence using Conformal Prediction, Quantile Regression, and Probabilistic Distributions.

## 📂 Repository Structure & Navigation

### 1. Data
The dataset used for training and evaluation.
* **Location:** [`Data/`](Data/)
* **Files:**
    * [`train.csv`](Data/train.csv): Training dataset containing concrete mix features.
    * [`test.csv`](Data/test.csv): Test dataset for model evaluation.
* **Features:**
    * `C`: Cement
    * `mp`: Mineral Admixtures / Slag
    * `FA`: Fine Aggregate
    * `CA`: Coarse Aggregate
    * `F`: Fly Ash / Filler
    * `W_P`: Water-Powder Ratio
    * `Adm`: Admixture (Superplasticizer)
    * `str`: Compressive Strength (Target Variable)

### 2. Hyperparameter Tuning
Optimizing model performance using various search strategies to find the best configuration for algorithms like XGBoost, LightGBM, CatBoost, and Random Forest.

#### General Optimization
* **Notebook:** [`Hyperparameter_tuning.ipynb`](Hyperparameter_Tuning/Hyperparameter_tuning.ipynb)
* **Description:** Implements **Random Grid**, **GridSearchCV**, **Bayesian Optimization**, and **Hyperband**. Results (best models) are saved in the `output/` folder.

#### Advanced Optuna Optimization
Deep dive into Optuna samplers and pruners for efficient tuning.
* **Optuna Study 1:** [`Hyperparameter_tuning_Optuna_1.ipynb`](Hyperparameter%20tuning%20using%20Optuna/Optuna_1/Hyperparameter_tuning_Optuna_1.ipynb)
    * Focuses on testing different Optuna samplers and pruners.
* **Optuna Study 2:** [`Hyperparameter_tuning_Optuna_2.ipynb`](Hyperparameter%20tuning%20using%20Optuna/Optuna_2/Hyperparameter_tuning_Optuna_2.ipynb)
    * Extended optimization and comparison of results.
* **Autosampler:** [`Optuna_autosampler.ipynb`](Hyperparameter%20tuning%20using%20Optuna/Optuna_autosampler/Optuna_autosampler.ipynb)
    * Analysis of Optuna's autosampler capabilities.
* **PGBM Tuning:** [`PGBM.ipynb`](Hyperparameter%20tuning%20using%20Optuna/Optuna_PGBM/PGBM.ipynb)
    * Specific tuning for Probabilistic Gradient Boosting Machines.

### 3. Model Explanations
Interpreting the "Black Box" models to understand which features drive predictions.
* **Notebook:** [`Model_explainations.ipynb`](Model_Explainations/Model_explainations.ipynb)
* **Techniques:**
    * **SHAP (SHapley Additive exPlanations):** Global and local feature importance.
    * **LIME (Local Interpretable Model-agnostic Explanations):** Individual prediction explanation.

### 4. Uncertainty Analysis
Moving beyond point predictions to estimate the reliability and coverage of the models.

#### Probabilistic Distributions
* **Notebook:** [`Probabilistic__Distribution.ipynb`](Uncertainity_Analysis/Probabilistic%20_Distribution%20(IBUG)/Probabilistic__Distribution.ipynb)
* **Description:** Applies probabilistic distributions over **NGBoost** (Natural Gradient Boosting) and **PGBM** to achieve statistical coverage (aiming for ~95% confidence intervals).

#### Conformal Predictions
* **Notebook:** [`Conformal_Predictions(MAPIE,PUNCC).ipynb`](Uncertainity_Analysis/Conformal_Predictions/Conformal_Predictions(MAPIE,PUNCC).ipynb)
* **Description:** Uses **MAPIE** and **PUNCC** libraries to implement conformal prediction, ensuring that the ground truth lies within the predicted interval with a high probability (approx. 90%).

#### Quantile Regression
* **Notebook:** [`Quantile_Regression.ipynb`](Uncertainity_Analysis/Quantile_Regression/Quantile_Regression.ipynb)
* **Description:** Implements quantile regression to predict conditional quantiles (e.g., 5th and 95th percentiles) for interval estimation.

---

## 🚀 Getting Started

### Prerequisites
To run the notebooks in this repository, you will need the following Python libraries:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn optuna shap lime ngboost pgbm mapie puncc xgboost lightgbm catboost
