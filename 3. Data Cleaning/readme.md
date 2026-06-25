# 🧹 Pandas Series — EP 03: Data Cleaning Mastery

Part of my **Pandas Learning Series** — the most important episode so far. Before any analysis, visualization, or machine learning, the data has to be clean. This notebook covers the complete data cleaning workflow that every Data Scientist runs on every new dataset. 💪

---

## 📒 About This Notebook

Real-world data is messy. Missing values, duplicates, wrong data types, inconsistent text formatting — it's all here. This notebook builds the full cleaning toolkit from scratch and wraps up with the 5-check muscle memory routine that should run automatically every time you load data.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Name":       ["Ali", "Sara", "Ahmed", "Ahmed", "  Bilal", "AYESHA"],
    "Age":        [22, np.nan, 30, 30, 35, 28],
    "Salary":     [50000, 70000, np.nan, np.nan, 120000, 80000],
    "Department": ["HR", "IT", "IT", "IT", "HR", "Finance"]
})
```

Issues baked in: 1 missing Age, 2 missing Salaries, 1 duplicate row, inconsistent name formatting, leading whitespace.

---

## 🧠 The 9-Step Data Cleaning Workflow

> This should become automatic every time you load a new dataset.

```
1. Inspect
2. Find Missing Values
3. Handle Missing Values
4. Find Duplicates
5. Remove Duplicates
6. Check Data Types
7. Fix Data Types
8. Clean Text Columns
9. Verify Results
```

---

## 🧠 What's Covered

### 1. 🔍 Detect Missing Values
```python
df.isna()          # True = missing, False = present
df.isna().sum()    # count per column
```

### 2. 🩹 Handling Missing Values

There is no universal solution — it depends on context.

**Method 1 — Drop rows** *(only when very few rows are missing)*
```python
df.dropna()
```

**Method 2 — Fill with constant** *(for categorical columns)*
```python
df.fillna("Unknown")
```

**Method 3 — Fill with mean** *(most common for numeric)*
```python
df["Age"] = df["Age"].fillna(df["Age"].mean())
```

**Method 4 — Fill with median** *(preferred when outliers exist)*
```python
df["Salary"] = df["Salary"].fillna(df["Salary"].median())
```

**Method 5 — Fill with mode** *(most frequent value, for categorical)*
```python
df["Department"].fillna(df["Department"].mode()[0])
```

**Method 6 — Forward Fill** *(common in time series)*
```python
df.ffill()
```

**Method 7 — Backward Fill**
```python
df.bfill()
```

---

### 3. 🔁 Detecting & Removing Duplicates
```python
df.duplicated()          # bool mask — True = duplicate
df.duplicated().sum()    # count duplicates
df.drop_duplicates()     # remove them
```

---

### 4. 🔠 Data Type Inspection & Conversion
```python
df.dtypes                                         # inspect all types
df["Age"] = df["Age"].astype(int)                 # convert type

# Common real-world problem: "Unknown" in a numeric column
age = pd.to_numeric(age, errors="coerce")         # converts invalid → NaN
```

---

### 5. 🏷️ Renaming Columns
```python
df.rename(columns={"cust_age": "Age", "cust_sal": "Salary"})
```

---

### 6. 🧽 Text Cleaning
```python
df["Name"].str.strip()    # remove leading/trailing spaces
df["Name"].str.lower()    # lowercase
df["Name"].str.upper()    # UPPERCASE
df["Name"].str.title()    # Title Case ← industry favourite

df["Department"].replace({"HR": "Human Resources", "IT": "Information Technology"})
```

---

### 7. ✅ Verification
```python
df.info()
df.isna().sum()
df.duplicated().sum()
df.dtypes
df.head()
```

---

## 💪 5 Checks — Muscle Memory

Run these **every single time** you load a new dataset:

```python
df.head()              # preview
df.info()              # types + non-null counts
df.isna().sum()        # missing values per column
df.duplicated().sum()  # duplicate rows
df.dtypes              # column data types
```

---

## 🏋️ Practice Problems

8 challenges solved in the notebook:

| # | Challenge |
|---|---|
| 1 | Create a DataFrame with missing ages, detect with `isna()` |
| 2 | Fill missing ages with mean |
| 3 | Fill missing salaries with median |
| 4 | Create and detect duplicate rows |
| 5 | Remove duplicates, verify removal |
| 6 | Clean names with `str.strip()` and `str.title()` |
| 7 | Convert a mixed column with "Unknown" to numeric using `pd.to_numeric()` |
| 8 | Rename `cust_age` and `cust_sal` to `Age` and `Salary` |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Data_Cleaning.ipynb
```

**Requirements:** Python 3.x · Pandas · NumPy · Jupyter Notebook

```bash
pip install pandas numpy jupyter
```

---

## 📚 Part of the Pandas Series

| # | Topic |
|---|---|
| 01 | Series & DataFrames |
| 02 | Indexing & Slicing |
| **03** | **Data Cleaning Mastery ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
