
# 🏗️ Concrete Data Analysis & Strength Prediction

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Status](https://img.shields.io/badge/Status-Active-success)]()

A comprehensive machine learning repository dedicated to predicting the **Compressive Strength of Concrete**. This project goes beyond simple prediction by incorporating rigorous **Hyperparameter Tuning**, **Model Explainability** (XAI), and **Uncertainty Quantification** to ensure robust and reliable engineering applications.

---

## 📑 Table of Contents (Navigation)

1. [📌 Project Overview](#-project-overview)
2. [📂 Repository Structure](#-repository-structure)
3. [📊 Dataset Details](#-dataset-details)
4. [🛠️ Workflow & Methodology](#-workflow--methodology)
    - [Phase 1: Hyperparameter Tuning](#phase-1-hyperparameter-tuning)
    - [Phase 2: Model Explainability](#phase-2-model-explainability)
    - [Phase 3: Uncertainty Analysis](#phase-3-uncertainty-analysis)
5. [🚀 Installation & Usage](#-installation--usage)

---

## 📌 Project Overview

This repository implements a full data science pipeline for concrete strength analysis. It addresses the following key challenges:
- **Optimization**: Finding the absolute best model configurations using state-of-the-art frameworks like Optuna.
- **Transparency**: Using SHAP and LIME to unbox "black-box" models and understand feature impact.
- **Reliability**: Estimating prediction intervals using Conformal Prediction and Probabilistic Regression to gauge model confidence.

---

## 📂 Repository Structure

The repository is organized into four main modules. Click on the headings to navigate to the files.

### 1. 🗂️ [Data](./Data)
Contains the raw dataset split into training and testing sets.
- **[`train.csv`](./Data/train.csv)**: Historical data used for model training.
- **[`test.csv`](./Data/test.csv)**: Unseen data used for final evaluation.

### 2. 🎛️ Hyperparameter Tuning
We employ two distinct approaches for optimization:

#### A. [Standard Tuning Techniques](./Hyperparameter_Tuning)
- **[`Hyperparameter_tuning.ipynb`](./Hyperparameter_Tuning/Hyperparameter_tuning.ipynb)**
  - Implements **Grid Search**, **Random Search**, **Bayesian Optimization**, and **Hyperband**.
  - Compares convergence speed and final model performance across these methods.

#### B. [Advanced Optuna Integration](./Hyperparameter%20tuning%20using%20Optuna)
- **[`Optuna_1/`](./Hyperparameter%20tuning%20using%20Optuna/Optuna_1/Hyperparameter_tuning_Optuna_1.ipynb)**: Tests various Optuna Samplers (TPE, CmaEs) and Pruners (Hyperband, Median).
- **[`Optuna_2/`](./Hyperparameter%20tuning%20using%20Optuna/Optuna_2/Hyperparameter_tuning_Optuna_2.ipynb)**: Extended study focusing on maximizing the objective function for complex boosting models.
- **[`Optuna_autosampler/`](./Hyperparameter%20tuning%20using%20Optuna/Optuna_autosampler/Optuna_autosampler.ipynb)**: Investigates Optuna's automatic sampling capabilities.
- **[`Optuna_PGBM/`](./Hyperparameter%20tuning%20using%20Optuna/Optuna_PGBM/PGBM.ipynb)**: Specialized tuning for Probabilistic Gradient Boosting Machines.

### 3. 🧠 [Model Explainations](./Model_Explainations)
- **[`Model_explainations.ipynb`](./Model_Explainations/Model_explainations.ipynb)**
  - **SHAP**: Generates summary plots and dependence plots to show global feature importance.
  - **LIME**: Explains individual predictions to validate model behavior on specific concrete samples.

### 4. 📉 [Uncertainity Analysis](./Uncertainity_Analysis)
A critical component for engineering safety.

- **[Conformal Predictions](./Uncertainity_Analysis/Conformal_Predictions/Conformal_Predictions(MAPIE,PUNCC).ipynb)**
  - Uses **MAPIE** and **PUNCC** to generate rigorous prediction intervals (e.g., 90% confidence) with guaranteed coverage properties.
  
- **[Probabilistic Distribution (IBUG)](./Uncertainity_Analysis/Probabilistic%20_Distribution%20(IBUG)/Probabilistic__Distribution.ipynb)**
  - Implements **NGBoost** and **PGBM** to output full probability distributions (mean and variance) for each prediction, rather than single point estimates.
  
- **[Quantile Regression](./Uncertainity_Analysis/Quantile_Regression/Quantile_Regression.ipynb)**
  - Trains models to predict specific quantiles (5th and 95th percentiles) directly, providing a non-parametric way to estimate uncertainty.

---

## 📊 Dataset Details

The dataset comprises physical and chemical properties of concrete. The target variable is **Compressive Strength**.

| Feature | Description | Unit |
| :--- | :--- | :--- |
| **C** | Cement content | kg/m³ |
| **mp** | Mineral Admixtures / Slag | kg/m³ |
| **FA** | Fine Aggregate | kg/m³ |
| **CA** | Coarse Aggregate | kg/m³ |
| **F** | Fly Ash / Filler | kg/m³ |
| **W_P** | Water-to-Powder Ratio | Ratio |
| **Adm** | Admixture (Superplasticizer) | kg/m³ |
| **str** | **Compressive Strength (Target)** | MPa |

---

## 🛠️ Workflow & Methodology

### Phase 1: Hyperparameter Tuning
Before finalizing a model, we perform extensive tuning to minimize RMSE.
1. **Selection**: We select algorithms like XGBoost, LightGBM, and CatBoost.
2. **Optimization**:
   - We start with **Random Search** to narrow the search space.
   - We apply **Bayesian Optimization** and **Optuna** (TPE Sampler) to fine-tune learning rates, tree depths, and regularization parameters.
3. **Selection**: The configuration with the best Cross-Validation score is saved for training.

### Phase 2: Model Explainability
To ensure the model learns physics-compliant rules (e.g., more cement usually equals higher strength):
- We run **SHAP** analysis on the best performing model.
- We verify that features like `C` (Cement) and `Adm` (Admixture) have positive SHAP values.
- We use **LIME** to audit outliers where the model predicts unusually high or low strength.

### Phase 3: Uncertainty Analysis
We acknowledge that no model is perfect.
- **Method A (Conformal)**: We generate a prediction interval `[Lower, Upper]`. If the interval is too wide, the model is uncertain about that specific concrete mix.
- **Method B (Probabilistic)**: We model the output as a Normal distribution $\mathcal{N}(\mu, \sigma)$. A high $\sigma$ indicates high uncertainty (aleatoric uncertainty).

---
