# 📊 Pandas Series — EP 04: Exploratory Data Analysis (EDA)

Part of my **Pandas Learning Series** — this one is where data starts talking. EDA is the process of understanding a dataset before you ever touch a model. Done right, it tells you what's normal, what's unusual, and what questions to ask next. 🧠

---

## 📒 About This Notebook

EDA isn't a single function — it's a workflow. This notebook walks through the complete 7-step EDA process that professional analysts follow on every new dataset, covering descriptive statistics, categorical analysis, spread, frequency, correlation, and outlier detection.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Name":       ["Ali", "Sara", "Ahmed", "Ayesha", "Bilal"],
    "Age":        [22, 25, 30, 28, 35],
    "Salary":     [50000, 70000, 90000, 80000, 120000],
    "Department": ["HR", "IT", "IT", "Finance", "HR"],
})
```

---

## 🧭 The 7-Step EDA Workflow

```
1. Overview
2. Descriptive Statistics
3. Categorical Analysis
4. Numerical Analysis
5. Correlation Analysis
6. Outlier Detection
7. Business Insights
```

---

## 🧠 What's Covered

### 1. 📋 df.describe() — 8 Stats in One Call
```python
df.describe()               # numeric columns only
df.describe(include="all")  # includes categorical columns
```

**What every row means:**
| Row | Meaning |
|---|---|
| `count` | Non-missing values |
| `mean` | Average |
| `std` | Standard deviation (spread) |
| `min` | Smallest value |
| `25%` | Q1 — First Quartile |
| `50%` | Median — Q2 |
| `75%` | Q3 — Third Quartile |
| `max` | Largest value |

---

### 2. 📍 Mean, Median, Mode
```python
df["Salary"].mean()
df["Age"].median()
df["Department"].mode()          # returns Series (multiple modes possible)
df.mean(numeric_only=True)       # mean for all numeric columns
df.median(numeric_only=True)
```

---

### 3. 📈 Standard Deviation & Variance
```python
df["Salary"].std()    # spread
df["Salary"].var()    # spread² (variance = std²)
df.std(numeric_only=True)
```

**Interpretation:**
- Large std → huge differences in salary across employees
- Small std → employees earn similar amounts

---

### 4. 🏷️ Unique Values & Value Counts
```python
df["Department"].unique()                        # distinct values
df["Department"].nunique()                       # count of distinct values
df["Department"].value_counts()                  # frequency table
df["Department"].value_counts(normalize=True)    # proportions (0–1)
```
> `value_counts()` is one of the most powerful functions in EDA.

---

### 5. 📦 Quartiles
```python
df["Salary"].quantile(0.25)              # Q1
df["Salary"].quantile(0.5)               # Q2 (median)
df["Salary"].quantile(0.75)              # Q3
df["Salary"].quantile([0.25, 0.5, 0.75, 1])  # all at once
```

---

### 6. 🔗 Correlation Analysis
```python
df[["Age", "Salary"]].corr()
```

**Reading the correlation matrix:**
| Value | Meaning |
|---|---|
| `0.8–1.0` | Strong positive |
| `0.5–0.8` | Moderate positive |
| `0–0.5` | Weak positive |
| `-ve values` | Same idea, opposite direction |
| Diagonal | Always 1 (Age vs Age = perfect) — ignore |

---

### 7. 🚨 Outlier Detection (IQR Method)
```python
q1 = df["Salary"].quantile(0.25)
q3 = df["Salary"].quantile(0.75)
iqr = q3 - q1
lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr
outliers = df[(df["Salary"] < lower) | (df["Salary"] > upper)]
```

---

## 💪 Professional EDA Checklist — 6 Checks

Run these every time you get a new dataset:

```python
df.info()             # structure + types
df.describe()         # descriptive stats
df.isna().sum()       # missing values
df.nunique()          # distinct value counts
df.corr()             # correlation matrix
df.value_counts()     # category frequency
```

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Exploratory_Data_Analysis.ipynb
```

**Requirements:** Python 3.x · Pandas · Jupyter Notebook

```bash
pip install pandas jupyter
```

---

## 📚 Part of the Pandas Series

| # | Topic |
|---|---|
| 01 | Series & DataFrames |
| 02 | Indexing & Slicing |
| 03 | Data Cleaning Mastery |
| **04** | **Exploratory Data Analysis ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
