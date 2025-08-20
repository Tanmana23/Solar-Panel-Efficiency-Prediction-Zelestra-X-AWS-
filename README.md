# Solar Panel Efficiency Prediction

## Project Overview

This repository contains a machine learning solution for the Zelestra solar panel efficiency prediction challenge. The objective was to build a model that accurately predicts the energy efficiency of solar panels using a variety of real-world sensor data.

My approach integrates domain-specific knowledge of solar panel physics with advanced ensemble modeling techniques. This physics-informed methodology proved more effective than relying on purely algorithmic optimization and resulted in a top-ranking performance.

The final model achieved a **Root Mean Square Error (RMSE) of approximately 0.0998** on a held-out validation set and a custom competition score of **90.17%**.

## Technical Approach

The solution is built around a robust multi-stage pipeline focused on data integrity, feature relevance, and model generalization.

### Data Preprocessing
A rigorous data cleaning pipeline was implemented to handle anomalies common in sensor data. This included:
-   **Systematic Cleaning**: Addressed contaminated readings, including invalid strings (`"unknown"`, `"badval"`) and physically impossible values (e.g., negative irradiance).
-   **Hierarchical Imputation**: Utilized a multi-stage strategy that prioritized physics-based relationships and group-level statistics (`string_id`) before resorting to global medians.

### Feature Engineering
Over 40 new features were developed based on the physical principles governing solar panel performance. Key feature categories include:
-   **Electrical Physics**: `power`, `power_density`, and normalized efficiency ratios.
-   **Thermal Dynamics**: `temp_differential`, `thermal_stress`, and wind cooling effects.
-   **Degradation and Environmental Factors**: Panel age interactions, soiling impact, and maintenance effectiveness.

### Modeling and Validation
-   **Ensemble Strategy**: Employed an advanced ensemble of multiple CatBoost and LightGBM models. The final prediction is a weighted blend of these models, refined with conservative post-processing techniques like Gaussian smoothing and quantile-based calibration.
-   **Robust Validation**: A 4-fold `GroupKFold` cross-validation strategy, grouped by `string_id`, was used to ensure the model generalizes well to new, unseen panel installations and to prevent data leakage.

## Key Results and Insights

-   **Final Performance**: The model achieved an RMSE of **~0.0998** in cross-validation.
-   **Dominant Features**: Physics-informed features such as `power` (voltage × current), `temp_differential`, and `effective_irradiance` were consistently ranked as the most important predictors by the models.
-   **Core Insight**: The project underscores that for complex, domain-specific problems, a deep understanding of the underlying physical principles is critical for building a high-performance predictive model. The success of this approach highlights the value of feature engineering guided by domain expertise.
