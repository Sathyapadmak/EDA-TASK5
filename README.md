# Healthcare Data — Exploratory Data Analysis (EDA)

## 📌 Overview

This project performs an **Exploratory Data Analysis (EDA)** on a healthcare dataset (`healthcare_data_for_task.csv`). The goal is to understand the structure of the data, clean it, engineer a few useful features, and generate summary statistics and visualizations that reveal patterns in patient admissions, billing, and medical conditions.

The dataset includes patient-level records with fields such as:

- `Patient_ID` — unique identifier for each patient
- `Age` — patient age
- `Gender` — patient gender
- `Medical_Condition` — diagnosed condition
- `Medical_Code` — associated medical code (may contain missing values)
- `Admission_Type` — type of hospital admission (e.g., Emergency, Elective, Urgent)
- `Date_of_Admission` / `Discharge_Date` — admission and discharge timestamps
- `Billing_Amount` — cost billed for the patient's treatment

This analysis was built using **Python**, with **Pandas** for data handling and **Matplotlib / Seaborn** for visualization.

---

## 🛠️ Tech Stack / Libraries

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`

---

## 🚀 Steps Performed

### 1. Import Libraries
Loaded `pandas`, `numpy`, `matplotlib.pyplot`, and `seaborn` for data analysis and visualization.

### 2. Load the Dataset
Read the raw CSV file into a Pandas DataFrame using `pd.read_csv()`.

### 3. Initial Data Inspection
- Viewed the first few rows with `df.head()` to understand the structure.
- Checked the shape of the dataset (`df.shape`) to know the number of rows and columns.
- Used `df.info()` to inspect data types and non-null counts.
- Used `df.describe()` to get summary statistics (mean, std, min, max, etc.) for numeric columns.
- Listed all column names with `df.columns`.

### 4. Column-Level Exploration
Inspected key columns individually, such as `Age` and `Patient_ID`, to get a feel for the data.

### 5. Missing Value Check
Used `df.isnull().sum()` to identify columns with missing/null values.

### 6. Data Cleaning
- Filled missing values in `Medical_Code` with the placeholder `"Unknown"` instead of dropping rows, to preserve data.
- Standardized the `Admission_Type` column by stripping extra whitespace and converting text to Title Case (e.g., `" emergency "` → `"Emergency"`), which avoids duplicate categories caused by inconsistent formatting.

### 7. Category Validation
- Checked unique values in `Admission_Type` using `.unique()`.
- Counted the frequency of each admission type using `.value_counts()`.

### 8. Date Conversion
Converted `Date_of_Admission` and `Discharge_Date` from plain strings/objects into proper `datetime` format using `pd.to_datetime()`, enabling date-based operations.

### 9. Date Feature Extraction
Extracted the `year`, `month`, and `day` components from `Date_of_Admission` for potential time-based trend analysis.

### 10. Post-Cleaning Verification
Re-ran `df.info()` to confirm the updated data types (especially the datetime conversions) were applied correctly.

### 11. Feature Engineering — Length of Stay
Created a new column `Stay_Days`, calculated as the difference in days between `Discharge_Date` and `Date_of_Admission`, giving the length of each patient's hospital stay.

### 12. Billing Analysis
Used `df['Billing_Amount'].describe()` to summarize billing statistics — mean, minimum, maximum, and spread of treatment costs.

### 13. Grouped Analysis
Calculated the **average age per medical condition** using `groupby('Medical_Condition')['Age'].mean()`, to see which conditions affect which age groups the most.

### 14. Cross-tabulation
Built a cross-tab between `Medical_Condition` and `Gender` using `pd.crosstab()` to compare condition frequency across genders.

### 15. Visualization
Plotted a **bar chart** of `Admission_Type` counts using `value_counts().plot(kind='bar')`, labeled with axis titles, to visually compare the volume of Emergency, Elective, and Urgent admissions.

---

## 📊 Final Output — Admission Type Distribution

The final step of the notebook generates a bar chart showing the count of patients by `Admission_Type`. This is the key visual takeaway of the EDA — it highlights which admission category is most common in the dataset.

*(See the chart rendered in the notebook / chat output. Save the chart image, e.g. `admission_type_chart.png`, in this repo and reference it below if you'd like it embedded here:)*

```markdown
![Admission Type Distribution](admission_type_chart.png)
```

---

## ▶️ How to Run

```bash
pip install pandas numpy matplotlib seaborn
jupyter notebook EDA_TASK5.ipynb
```

Make sure `healthcare_data_for_task.csv` is placed in the correct path referenced in the notebook before running.

---

## 📁 Repository Structure

```
├── EDA_TASK5.ipynb          # Main analysis notebook
├── healthcare_data_for_task.csv   # Source dataset (not included — add your own)
└── README.md                 # Project documentation
```

---

## 📝 Notes

- Missing values in `Medical_Code` were imputed rather than dropped, to retain sample size.
- Text fields were standardized to avoid duplicate categories from inconsistent casing/whitespace.
- Dates were properly converted to enable time-based feature engineering (`Stay_Days`).
