# Flight Delay Data Engineering

## Project Overview

This project focuses on building data engineering pipelines for flight delay data using both **ETL** and **ELT** approaches.

The project combines flight delay data from a Kaggle CSV dataset and flight data collected from the **AviationStack API**. The data is cleaned, transformed, combined, and loaded into different storage systems for analysis.

## Project Objectives

- Collect flight data from multiple sources.
- Clean and validate flight delay data.
- Integrate data from Kaggle and AviationStack API.
- Build an ETL pipeline using Python.
- Build an ELT pipeline using Python, SQL, and Neon.
- Store processed data in SQLite.
- Create a final dataset suitable for analysis and dashboards.

## Data Sources

### Kaggle Dataset

The project uses a raw flight delay dataset stored in:

`Flight_Delays_raw.csv`

The data includes information such as:

- Flight date
- Airline
- Origin airport
- Destination airport
- Departure delay
- Arrival delay
- Cancellation
- Diversion

### AviationStack API

Flight data is also collected using the AviationStack API and saved as:

`api_flights.csv`

The API data is retrieved using Python and converted into a structured DataFrame before being saved as a CSV file.

## Data Cleaning

The `data_clean.py` script performs several preprocessing steps, including:

- Standardizing column names.
- Handling missing text values.
- Handling missing time and delay values.
- Filling missing numerical values using the median.
- Removing duplicate records.
- Filtering invalid delay values.
- Converting flight dates into a consistent date format.
- Validating missing values and duplicates.

The cleaned dataset is saved as:

`flight_delays_cleaned.csv`

## ETL Pipeline

The ETL pipeline follows three main stages:

### 1. Extract

Data is extracted from:

- The cleaned Kaggle flight delay dataset.
- AviationStack API.

### 2. Transform

The data is cleaned and transformed by:

- Standardizing column names.
- Removing duplicates.
- Converting dates and numerical values.
- Creating total delay.
- Creating delay status.
- Standardizing data from both sources.
- Combining the datasets.

The delay status is classified as:

- **Cancelled**
- **Diverted**
- **Delayed**
- **On Time**

### 3. Load

The transformed data is loaded into a **SQLite database** called:

`flights.db`

The final table is:

`flights`

## ELT Pipeline

The ELT pipeline follows a different approach by loading the raw data first and performing transformations inside the database.

### 1. Extract

Raw data is collected from the Kaggle dataset and AviationStack API.

### 2. Load

The raw datasets are loaded into **Neon PostgreSQL** staging tables:

- `stage_kaggle_raw`
- `stage_api_raw`

### 3. Transform

SQL is used to transform the raw data inside the database and create the final flight delay dataset.

The final table is:

`final_flight_delays`

The processed data can then be exported for dashboard and analysis purposes.

## Technologies

- Python
- Pandas
- SQL
- SQLite
- PostgreSQL / Neon
- AviationStack API
- Kaggle Dataset

## Project Files

| File | Description |
|---|---|
| `ETL.py` | Main ETL pipeline |
| `ELT.py` | ELT pipeline |
| `ELT.txt` | SQL transformations for the ELT pipeline |
| `api_data.py` | Collects flight data from AviationStack API |
| `data_clean.py` | Cleans and validates flight delay data |
| `Flight_Delays_raw.csv` | Raw flight delay dataset |
| `flight_delays_cleaned.csv` | Cleaned flight delay dataset |
| `api_flights.csv` | Flight data collected from the API |

## ETL vs ELT

| ETL | ELT |
|---|---|
| Transform before loading | Load before transforming |
| Uses Python for transformation | Uses SQL for database transformation |
| Loads processed data into SQLite | Loads raw data into Neon |
| Final table: `flights` | Final table: `final_flight_delays` |

## Project Workflow

![Flight Data Engineering Workflow](Flight%20Delay%20Data%20Engineering%20Workflow.png)

## Outcome

The project demonstrates how flight data from different sources can be collected, cleaned, integrated, and stored using both ETL and ELT data engineering approaches.

The resulting datasets are prepared for further analysis and dashboard development.
