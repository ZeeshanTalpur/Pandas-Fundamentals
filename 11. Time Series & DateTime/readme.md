# 📅 Pandas Series — EP 11: Time Series & DateTime Mastery

Part of my **Pandas Learning Series** — the episode that makes real-world datasets make sense. Almost every production dataset has a date or timestamp column. This notebook covers every DateTime tool in Pandas: converting, extracting, filtering, resampling, rolling windows, and growth calculations. ⏱️

---

## 📒 About This Notebook

Real-world data almost always contains:
- Order dates · Transaction timestamps · Login times
- Registration dates · Delivery dates · Sensor readings

And your job is often:
- Revenue per month · Users per week · Sales growth per quarter
- Rolling averages · Moving windows · Time-based filtering

This notebook teaches all of that.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Date":  ["2025-01-01", "2025-01-02", "2025-01-03", "2025-01-04", "2025-01-05"],
    "Sales": [100, 120, 110, 150, 130]
})
```

---

## 🧠 What's Covered

### 1. 🔄 Converting Strings to DateTime

Date columns load as plain strings (`object` dtype) — Pandas doesn't understand them as dates yet.

```python
df["Date"].dtype          # object → just a string

df["Date"] = pd.to_datetime(df["Date"])

df["Date"].dtype          # datetime64[ns] ✅
```

Now Python understands Year, Month, Day, Hour, Minute, Second.

---

### 2. 🔑 The .dt Accessor

Once a column is DateTime, `.dt` unlocks a full set of extraction tools:

```python
df["Date"].dt.year
df["Date"].dt.month
df["Date"].dt.day
df["Date"].dt.month_name()    # → "January"
df["Date"].dt.day_name()      # → "Monday"
```

---

### 3. 📆 Filtering By Dates

```python
df[df["Date"] > "2025-01-03"]     # after a specific date
```

---

### 4. 📌 Setting Date as Index

```python
df = df.set_index("Date")
df.loc["2025-01-03"]              # exact date
```

---

### 5. 🔍 Partial String Indexing

Once Date is the index, you can filter by partial strings:

```python
df.loc["2025-01"]     # all of January 2025
df.loc["2025"]        # all of 2025
```

---

### 6. 📆 date_range() — Generate Date Sequences

```python
pd.date_range(start="2025-01-02", periods=5)

# Monthly frequency
pd.date_range(start="2025-02", periods=6, freq="ME")
```

**Common Frequency Codes:**

| Code | Meaning |
|---|---|
| `D` | Daily |
| `W` | Weekly |
| `ME` | Month End |
| `MS` | Month Start |
| `Q` | Quarterly |
| `Y` | Year End |
| `H` | Hourly |
| `min` | Minutes |
| `S` | Seconds |

---

### 7. 📊 resample() — GroupBy for Time

```python
df.resample("ME").sum()     # monthly totals
df.resample("ME").mean()    # monthly averages
```

> **Intuition:** `groupby()` groups by categories. `resample()` groups by time periods.

---

### 8. 🔁 rolling() — Moving Average

```python
df["Rolling_3"] = df["Sales"].rolling(3).mean()
```

**Intuition:**
- Takes current day + previous 2 days = 3 days total
- Calculates average
- First 2 rows will be NaN (not enough history yet)
- This is called a **Moving Average** — the window slides forward with each day

---

### 9. 📈 expanding() — Running Cumulative

```python
df["Running_Avg"] = df["Sales"].expanding().mean()
```

| Method | Window |
|---|---|
| `rolling(n)` | Last n values only |
| `expanding()` | Everything so far (grows with each row) |

---

### 10. ↔️ shift(), diff(), pct_change()

```python
df["Yesterday"]  = df["Sales"].shift(1)          # previous day's value
df["Difference"] = df["Sales"].diff()             # day-over-day change
df["Growth"]     = df["Sales"].pct_change()       # percentage growth
```

> All three are extremely important in **finance and business analytics**.

---

## 📋 Key Intuitions

| Concept | Intuition |
|---|---|
| `pd.to_datetime()` | Convert strings → dates. Always do this first. |
| `.dt` accessor | Unlocks all date extraction |
| `resample()` | groupby() for time periods |
| `rolling(n)` | Last n values |
| `expanding()` | Everything up to current row |
| `shift(1)` | Yesterday's value |
| `diff()` | Change from previous row |
| `pct_change()` | % growth from previous row |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook "Time_Series___DateTime.ipynb"
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
| 03 | Data Cleaning Mastery |
| 04 | Exploratory Data Analysis |
| 05 | GroupBy Mastery |
| 06 | Transformations & Feature Engineering |
| 07 | Combining Data — SQL Joins |
| 08 | SQL Thinking with Pandas |
| 09 | MultiIndex Mastery |
| 10 | Advanced GroupBy |
| **11** | **Time Series & DateTime Mastery ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
