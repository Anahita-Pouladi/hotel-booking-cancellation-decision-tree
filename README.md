# Hotel Booking Cancellation Prediction with Explainable Machine Learning

## Project Links

- **GitHub Repository:** [hotel-booking-cancellation-decision-tree](https://github.com/Anahita-Pouladi/hotel-booking-cancellation-decision-tree)
- **Kaggle Notebook:** [Hotel Booking Cancellation Prediction | Decision Tree](https://www.kaggle.com/code/anahitapouladi/hotel-booking-cancellation-decision-tree)

-------------------------------------------------------------------------

## Project Overview

Hotel booking cancellations create operational challenges for
hospitality businesses by affecting inventory planning, revenue
forecasting, and customer management decisions.

This project develops a machine learning pipeline to predict whether a
hotel reservation will be cancelled using only information available at
the time of booking.

The objective is not only to maximize predictive performance, but also
to build a reliable and interpretable workflow with careful attention
to:

-   Data quality validation
-   Leakage prevention
-   Feature engineering
-   Model generalization
-   Explainability

------------------------------------------------------------------------

## Problem Statement

Can historical reservation information be used to identify cancellation
risk before the final reservation outcome is known?

This project frames cancellation prediction as a binary classification
problem:

-   Target: `is_canceled`
-   Class 0: Reservation not cancelled
-   Class 1: Reservation cancelled

The model is designed as a pre-arrival risk prediction system, meaning
features that become available after cancellation decisions are
excluded.

------------------------------------------------------------------------

## Dataset

The project uses the Hotel Booking Demand dataset.

Dataset characteristics:

-   Rows: 119,390
-   Original Features: 32
-   Prediction Target: Booking cancellation

The dataset contains reservation details such as:

-   Lead time
-   Customer type
-   Deposit information
-   Stay duration
-   Previous booking behavior
-   Special requests
-   Market and distribution information


------------------------------------------------------------------------

## Dataset Attribution and License

This project uses the **Hotel Booking Demand** dataset published on Kaggle by **Jesse Mostipak**.

- **Dataset:** Hotel Booking Demand
- **Source:** [Kaggle — Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)
- **Dataset license:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- **Original research:** *Hotel Booking Demand Datasets* by Nuno Antonio, Ana Almeida, and Luis Nunes, published in *Data in Brief* (2019)

The raw dataset is **not included in this repository**. It must be obtained from its original source and remains subject to the **CC BY 4.0** license.

The repository's **MIT License applies only to the project code and documentation created for this portfolio project**; it does not replace or modify the dataset's original license.

------------------------------------------------------------------------

## Project Workflow

### Data Validation

The dataset was inspected through:

-   Shape and schema validation
-   Data type analysis
-   Descriptive statistics
-   Duplicate investigation
-   Missing value analysis

### Data Quality Handling

#### Duplicate Analysis

The dataset contains:

-   31,994 exact duplicate rows

These records were not automatically removed because the dataset does
not provide a reliable unique booking identifier.

Duplicate handling was treated as a data-quality consideration rather
than an automatic preprocessing step.

#### Missing Values

Main missing-value patterns:

  Feature     Missing Percentage
  --------- --------------------
  company                  \~94%
  agent                    \~14%
  country                   \<1%

Handling decisions:

-   `company` was removed due to extremely high missingness and limited
    predictive reliability.
-   `agent` was retained and treated as a categorical feature.
-   Remaining missing values were handled inside the preprocessing
    pipeline.

------------------------------------------------------------------------

## Leakage Prevention

A key objective of this project was preventing information leakage.

Removed features:

### Outcome Leakage

-   `reservation_status`
-   `reservation_status_date`

### Timing Leakage

-   `assigned_room_type`

This ensures that the model only uses information available before
cancellation occurs.

------------------------------------------------------------------------

## Feature Engineering

Additional features were created:

-   Total nights
-   Total guests

Additional validation checks were performed for:

-   Zero guest records
-   Zero night stays

------------------------------------------------------------------------

## Modeling Approach

### Baseline Model

A Decision Tree classifier was trained first without complexity
constraints.

  Metric         Score
  ----------- --------
  Accuracy      0.8606
  Precision     0.8144
  Recall        0.8078
  F1 Score      0.8111

The baseline model achieved strong test performance but showed
significant overfitting.

------------------------------------------------------------------------

## Hyperparameter Optimization

GridSearchCV was applied using a reduced search space with F1 score as
the optimization objective.

Best parameters:

``` text
criterion = gini
max_depth = 12
min_samples_leaf = 5
min_samples_split = 25
class_weight = None
ccp_alpha = 0.0
```

`ccp_alpha` was kept explicit for transparency, but pruning was not
actively explored because only the default value was evaluated.

------------------------------------------------------------------------

## Tuned Model Performance

  Metric         Score
  ----------- --------
  Accuracy      0.8582
  Precision     0.8298
  Recall        0.7766
  F1 Score      0.8023

The tuned model slightly reduced test F1 but significantly improved
generalization.

------------------------------------------------------------------------

## Generalization Analysis

### Baseline Decision Tree

  Metric              Value
  ---------------- --------
  Train F1           0.9944
  Test F1            0.8111
  Train-Test Gap     0.1833

### Tuned Decision Tree

  Metric              Value
  ---------------- --------
  Train F1           0.8158
  Test F1            0.8023
  Train-Test Gap     0.0135

The tuned model substantially reduced overfitting and produced a more
stable model.

------------------------------------------------------------------------

## Feature Importance

Top predictive features:

  Feature                       Importance
  --------------------------- ------------
  deposit_type_Non Refund           0.3856
  agent_9                           0.1064
  total_of_special_requests         0.0837
  lead_time                         0.0716
  country_PRT                       0.0664

Feature importance values represent model-specific patterns and should
not be interpreted as causal relationships.

------------------------------------------------------------------------

## Key Findings

-   Deposit type is the strongest decision-tree feature in this dataset.
-   Longer booking lead times provide useful cancellation signals.
-   Customer behavior features such as special requests contribute
    additional predictive information.
-   Model simplicity and generalization are more important than
    maximizing training performance.

------------------------------------------------------------------------

## Limitations

-   Duplicate records remain an unresolved data-quality question.
-   Decision Tree models may not capture complex nonlinear interactions
    as effectively as ensemble methods.
-   Feature importance reflects model behavior, not causal impact.

------------------------------------------------------------------------

## Future Improvements

Possible future directions:

-   Compare with ensemble models such as Random Forest and Gradient
    Boosting.
-   Perform stability analysis across different data splits.
-   Explore calibrated probability predictions.
-   Investigate business-oriented threshold optimization.

------------------------------------------------------------------------

## Technologies

-   Python
-   Pandas
-   NumPy
-   Scikit-learn
-   Matplotlib
-   Seaborn
-   Jupyter Notebook

------------------------------------------------------------------------

## Project Structure

``` text
.
├── notebooks/
│   └── Hotel_Booking_Cancellation_Prediction_Decision_Tree.ipynb
├── README.md
├── requirements.txt
└── data/
```
