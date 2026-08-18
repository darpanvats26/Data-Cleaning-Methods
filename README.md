# Day 11 – Cleaned Company Employee Dataset

## Project Overview

This project cleans a messy company employee dataset using Python and Pandas. The dataset was inspected for missing values, duplicate records, inconsistent categorical entries, and incorrect data types. Appropriate cleaning techniques were applied, followed by verification and export of the cleaned dataset.

## Dataset Summary

- **Original file:** `Day11_Messy_Company_Employee_Dataset.csv`
- **Original rows:** 157
- **Columns:** 12
- **Final rows:** 150
- **Rows removed:** 7 duplicate records
- **Final columns:** 12

### Columns

`Employee_ID`, `Employee_Name`, `Department`, `Job_Title`, `Age`, `Gender`, `Annual_Salary`, `Experience_Years`, `Joining_Date`, `City`, `Performance_Score`, `Work_Mode`

## Problems Identified

The original dataset contained:

- **32 missing values**
- **7 exact duplicate rows**
- Inconsistent capitalization in categorical fields, for example:
  - `ENGINEERING` / `engineering` → `Engineering`
  - `female` / `MALE` → `Female` / `Male`
  - `delhi` / `DELHI` → `Delhi`
  - `REMOTE` / `remote` → `Remote`
- `Joining_Date` was stored as an object/string instead of a date type.
- Numeric columns containing missing values required imputation.

## Cleaning Steps

### 1. Inspection

Pandas functions such as `head()`, `info()`, `describe()`, `isnull()`, `duplicated()`, and `value_counts()` were used to inspect the dataset and quantify data-quality issues.

### 2. Text Cleaning

Leading and trailing whitespace was removed using `str.strip()`. Categorical values in Department, Gender, City, and Work_Mode were standardized using consistent capitalization.

### 3. Data Type Correction

Numeric fields were converted with `pd.to_numeric(..., errors="coerce")`. The `Joining_Date` column was converted using `pd.to_datetime(..., errors="coerce")` and exported in `YYYY-MM-DD` format.

### 4. Missing Numerical Values

Missing values in `Age`, `Annual_Salary`, `Experience_Years`, and `Performance_Score` were filled using the **median** of each respective column. Median imputation was selected because it is less affected by extreme values than the mean.

### 5. Missing Categorical Values

Missing values in `Department`, `Gender`, `City`, and `Work_Mode` were filled using the **mode**, i.e. the most frequent valid category.

### 6. Duplicate Records

Exact duplicate records were identified using `duplicated()` and removed using `drop_duplicates()`. This reduced the dataset from 157 to 150 rows.

### 7. Verification

The dataset was checked after cleaning to confirm that the identified missing values and duplicate records had been resolved. The exported CSV was also re-read and verified.

## Before vs After

| Measure | Before Cleaning | After Cleaning |
|---|---:|---:|
| Rows | 157 | 150 |
| Columns | 12 | 12 |
| Missing Values | 32 | 0 |
| Duplicate Rows | 7 | 0 |

## Method Selection

Different methods were selected according to the type of data problem:

- **Median imputation** was used for numerical employee attributes.
- **Mode imputation** was used for categorical attributes.
- **Standardization** was used to make equivalent categorical values consistent.
- **`drop_duplicates()`** was used because the identified duplicate records were exact duplicates.
- **`pd.to_datetime()`** was used to correctly represent joining dates.
- `dropna()` was not used to discard incomplete employee records because the missing values could be reasonably imputed.
- Forward filling was not appropriate because employee records are independent observations; copying a previous employee's value could introduce incorrect information.

## Output Files

- `Cleaned_Company_Employee_Dataset_Day11.csv` — final cleaned dataset
- `Day11_Cleaning_Summary.txt` — brief cleaning summary

## Tools Used

- Python
- Pandas
- NumPy

## Final Result

The final dataset contains **150 rows and 12 columns**, with **0 missing values and 0 duplicate rows**. Categorical entries were standardized, numerical missing values were imputed appropriately, and the joining-date field was converted to a suitable date representation.

## Conclusion

The cleaning process improved the consistency and quality of the company employee dataset while preserving valid employee records. The resulting CSV is ready for further analysis.
