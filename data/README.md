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

- The raw dataset is excluded from this GitHub repository and should be downloaded from the original Kaggle source.
- The notebook expects the dataset to be available locally as `data/hotel_bookings.csv` or in one of the supported relative paths defined in the notebook.
- Do not rename the dataset unless you also update the data-loading code in the notebook.

## Data Quality Notes

The project documents several dataset-quality considerations, including:

- 31,994 exact duplicate rows
- High missingness in `company`
- Missing values in `agent`, `country`, and `children`
- No reliable unique booking identifier

These issues are handled and discussed in the main notebook and project documentation.


## License and Attribution

This project uses the **Hotel Booking Demand** dataset published on Kaggle by **Jesse Mostipak**.

- **Source:** [Kaggle — Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)
- **License:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- **Original research:** *Hotel Booking Demand Datasets* by Nuno Antonio, Ana Almeida, and Luis Nunes, published in *Data in Brief* (2019)

The raw dataset is **not included in this GitHub repository**. Download it from the original Kaggle source and place it in this directory as:

```text
hotel_bookings.csv
```

The repository's MIT License applies to the project code and documentation only. The dataset remains governed by its original **CC BY 4.0** license.

## Reproducibility

After placing `hotel_bookings.csv` in this directory, run the notebook from the repository root or from the `notebooks/` directory using the supported relative data paths.
