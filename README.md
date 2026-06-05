# Flipkart Demand Prediction

## Overview

This project predicts demand values for delivery locations using historical demand data. The solution processes large-scale datasets efficiently and generates a submission file in the format required by the competition.

The implementation uses a lookup-based prediction strategy combined with fallback mechanisms to ensure complete coverage for all test records.

---

## Features

* Efficient processing of large CSV datasets using chunked loading.
* Historical demand lookup based on:

  * Geohash
  * Day
  * Timestamp
* Automatic handling of missing matches.
* Geohash-level demand aggregation for fallback predictions.
* Global demand mean fallback for unseen locations.
* Generates competition-ready submission files.
* Includes validation checks to ensure output correctness.

---

## Project Structure

```text
Flipkart-main/
│
├── dataset/
│   ├── train.csv
│   └── test.csv
│
├── newidea.py
├── submission_from_notebook.csv
└── README.md
```

---

## Technologies Used

* Python
* Pandas
* Pathlib

---

## Methodology

### 1. Data Loading

The training and test datasets are loaded using Pandas.

### 2. Historical Demand Lookup

A lookup table is created using:

```python
["geohash", "day", "timestamp"]
```

The system searches for matching historical records and retrieves the corresponding demand values.

### 3. Missing Value Handling

If a direct match is unavailable:

1. Use the average demand for the same geohash.
2. If the geohash is unseen, use the overall mean demand from the training dataset.

This guarantees predictions for every test record.

### 4. Submission Generation

The final output contains:

```csv
Index,demand
0,0.0907
1,0.0898
2,0.0070
...
```

---

## Validation

The script verifies:

* Correct number of rows.
* Correct column names.
* No missing predictions.

Example:

```python
assert len(submission) == 41778
assert list(submission.columns) == ["Index", "demand"]
assert submission["demand"].isna().sum() == 0
```

---

## How to Run

Install dependencies:

```bash
pip install pandas
```

Run:

```bash
python newidea.py
```

The generated submission file will be:

```text
submission_from_notebook.csv
```

---

## Future Improvements

* Machine Learning-based demand forecasting.
* Time-series feature engineering.
* Geospatial clustering.
* XGBoost and LightGBM models.
* Automated hyperparameter tuning.
* Ensemble forecasting methods.

