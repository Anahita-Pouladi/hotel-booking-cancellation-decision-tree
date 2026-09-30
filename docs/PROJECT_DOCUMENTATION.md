# Project Documentation

# Hotel Booking Cancellation Prediction with Explainable Machine Learning

## 1. Introduction

This document provides technical documentation for the project.

The goal is to build a machine learning classification pipeline that
predicts hotel booking cancellations using information available at the
booking stage.

Main objectives:

-   Build a reliable ML workflow
-   Prevent data leakage
-   Evaluate model generalization
-   Maintain model interpretability

------------------------------------------------------------------------

## 2. Problem Definition

Problem type:

Binary classification

Target:

`is_canceled`

Classes:

-   0: Reservation not cancelled
-   1: Reservation cancelled

The model is designed as a pre-arrival risk prediction system.

------------------------------------------------------------------------

## 3. Dataset

Dataset size:

-   Rows: 119,390
-   Features: 32 original columns

The dataset includes reservation information such as:

-   Lead time
-   Deposit type
-   Customer information
-   Stay duration
-   Booking behavior
-   Special requests

------------------------------------------------------------------------

## 4. Data Quality Processing

## Duplicate Records

The dataset contains 31,994 exact duplicate rows.

Duplicates were not automatically removed because no reliable unique
booking identifier exists.

------------------------------------------------------------------------

## Missing Values

`company` was removed because of extremely high missingness.

`agent` was retained and treated as a categorical feature.

Remaining missing values were handled inside the preprocessing pipeline.

------------------------------------------------------------------------

## 5. Leakage Prevention

Removed outcome leakage:

-   `reservation_status`
-   `reservation_status_date`

Removed timing-sensitive feature:

-   `assigned_room_type`

This ensures predictions are based only on information available before
cancellation.

------------------------------------------------------------------------

## 6. Feature Engineering

Created features:

-   Total nights
-   Total guests

Additional validation:

-   Zero guest records
-   Zero night stays

------------------------------------------------------------------------

## 7. Modeling

Baseline Decision Tree:

  Metric         Score
  ----------- --------
  Accuracy      0.8606
  Precision     0.8144
  Recall        0.8078
  F1 Score      0.8111

The baseline model showed strong performance but significant
overfitting.

------------------------------------------------------------------------

## 8. Hyperparameter Optimization

GridSearchCV optimized F1 score.

Best parameters:

    criterion = gini
    max_depth = 12
    min_samples_leaf = 5
    min_samples_split = 25
    class_weight = None
    ccp_alpha = 0.0

------------------------------------------------------------------------

## 9. Generalization Analysis

Baseline:

-   Train F1: 0.9944
-   Test F1: 0.8111
-   Gap: 0.1833

Tuned:

-   Train F1: 0.8158
-   Test F1: 0.8023
-   Gap: 0.0135

The tuned model reduced overfitting and improved stability.

------------------------------------------------------------------------

## 10. Explainability

Top model features:

1.  deposit_type_Non Refund
2.  agent_9
3.  total_of_special_requests
4.  lead_time
5.  country_PRT

Feature importance represents model behavior, not causal impact.

------------------------------------------------------------------------

## 11. Limitations

-   Duplicate handling remains a data-quality question.
-   Decision Trees may not capture all complex patterns.
-   Feature importance is not causal analysis.

------------------------------------------------------------------------

## 12. Future Improvements

Possible extensions:

-   Random Forest and Gradient Boosting comparison
-   Probability calibration
-   Threshold optimization
-   Stability analysis

------------------------------------------------------------------------

## 13. Repository Structure

    .
    ├── README.md
    ├── docs/
    │   └── PROJECT_DOCUMENTATION.md
    ├── notebooks/
    │   └── Hotel_Booking_Cancellation_Prediction_Decision_Tree.ipynb
    ├── requirements.txt
    └── data/
