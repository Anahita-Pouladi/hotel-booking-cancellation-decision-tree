# Dataset

This project uses the **Hotel Booking Demand** dataset for predicting hotel booking cancellations.

## Expected File

Place the raw dataset in this directory with the following filename:

```text
hotel_bookings.csv
```

Expected project structure:

```text
data/
├── README.md
└── hotel_bookings.csv
```

## Dataset Overview

The dataset contains:

- **119,390 rows**
- **32 original columns**
- Booking, customer, stay, deposit, market, and reservation-related information
- Target variable: `is_canceled`

## Important Notes

- The raw dataset may be excluded from the GitHub repository depending on file size and redistribution terms.
- The notebook expects the dataset to be available locally as `data/hotel_bookings.csv` or in one of the supported relative paths defined in the notebook.
- Do not rename the dataset unless you also update the data-loading code in the notebook.

## Data Quality Notes

The project documents several dataset-quality considerations, including:

- 31,994 exact duplicate rows
- High missingness in `company`
- Missing values in `agent`, `country`, and `children`
- No reliable unique booking identifier

These issues are handled and discussed in the main notebook and project documentation.

## Reproducibility

After placing `hotel_bookings.csv` in this directory, run the notebook from the repository root or from the `notebooks/` directory using the supported relative data paths.
