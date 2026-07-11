# 🪟 Pandas Series — EP 15: Window Functions & Analytical Operations

Part of my **Pandas Learning Series** — the episode that changes how you think about analyzing rows. Window functions don't ask "what is the total?" They ask "what about each row, using the rows around it?" That's a completely different question — and it's how real analysts, financial engineers, and data scientists think. 📊

---

## 📒 About This Notebook

Standard aggregation collapses your data. Window functions **preserve every row** while adding analytical context.

Instead of:
> "What is total sales?" → one number

Ask:
> "What was the average of the last 3 days?"
> "How much did sales grow from yesterday?"
> "What's the running total so far?"
> "Who ranks highest in each group?"

These are all window operations.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Date":     pd.date_range("2025-01-01", periods=10),
    "Sales":    [100, 120, 150, 130, 160, 180, 170, 210, 220, 200],
    "Employee": ["A","A","A","A","A","B","B","B","B","B"]
})
```

---

## 🧠 What's Covered

### 1. 🔁 shift() — The Most Used Window Function

Moves values without changing the index. The current row can "look" at previous or next rows.

```python
df["Yesterday"] = df["Sales"].shift(1)    # previous row
df["Tomorrow"]  = df["Sales"].shift(-1)   # next row
```

> First row (shift(1)) → NaN — no previous row exists.

---

### 2. 📉 diff() — Day-Over-Day Change

```python
df["Daily_Change"] = df["Sales"].diff()
# 100 → NaN   120 → +20   150 → +30   130 → -20
```

**Formula:** Current − Previous

> First row always NaN. Negatives mean decrease.

---

### 3. 📈 pct_change() — Percentage Growth

```python
df["Growth"]   = df["Sales"].pct_change()       # as decimal
df["Growth_%"] = df["Sales"].pct_change() * 100 # as percentage
```

**Formula:** (Current − Previous) / Previous

> 120 → 100 = +20% growth. 130 → 150 = −13.3% drop.

---

### 4. ➕ cumsum() — Running Total

```python
df["Running_Sales"] = df["Sales"].cumsum()
# [100, 220, 370, 500, 660, 840...]
```

---

### 5. ⬆️ cummax() — Highest Value So Far

```python
df["Highest"] = df["Sales"].cummax()
# [100, 120, 150, 150, 160, 180...]
# Never goes down — records the peak at each row
```

---

### 6. ⬇️ cummin() — Lowest Value Encountered

```python
df["Lowest"] = df["Sales"].cummin()
# [100, 100, 100, 100, 100, 100...]
# Never goes up — records the floor at each row
```

---

### 7. ✖️ cumprod() — Running Product

```python
s = pd.Series([2, 3, 4])
s.cumprod()
# [2, 6, 24]
```

---

### 8. 🏆 rank() — Rank Rows

```python
df["Rank"] = df["Sales"].rank(ascending=False)
```

**Three ranking methods:**

| Method | Behaviour |
|---|---|
| `"average"` | Ties get the average of their positions |
| `"dense"` | No gaps in rank numbers |
| `"first"` | First occurrence wins |

```python
df["Rank_Avg"]   = df["Sales"].rank(method="average")
df["Rank_Dense"] = df["Sales"].rank(method="dense")
df["Rank_First"] = df["Sales"].rank(method="first")
```

---

### 9. 🪟 rolling() — The King of Window Functions

```python
df["Rolling_Mean"] = df["Sales"].rolling(window=3).mean()
df["Rolling_Sum"]  = df["Sales"].rolling(3).sum()
df["Rolling_Min"]  = df["Sales"].rolling(3).min()
df["Rolling_Max"]  = df["Sales"].rolling(3).max()
df["Rolling_Std"]  = df["Sales"].rolling(3).std()
```

**How it works:**
- Takes current row + previous (n-1) rows
- Calculates the function across that window
- Slides forward with each row

> First `n-1` rows → NaN (not enough history yet). This is the **Moving Average** used in finance, forecasting, and trend analysis.

---

### 10. 📈 expanding() — Everything So Far

```python
df["Expanding_Mean"] = df["Sales"].expanding().mean()
```

**rolling() vs expanding():**

| | rolling(n) | expanding() |
|---|---|---|
| Window size | Fixed (last n rows) | Grows with every row |
| First n rows | NaN | Calculated from row 1 |

---

### 11. ⚖️ ewm() — Exponentially Weighted Moving Average

```python
df["EWMA"] = df["Sales"].ewm(alpha=0.3).mean()
```

> Recent values get more weight than older values. `alpha=0.3` means 30% weight on the most recent observation. Used heavily in financial time series.

---

### 12. 👥 Group-Wise Window Functions

Instead of a global running total — compute **per employee**:

```python
df["Employee_Running_Sales"] = (
    df
    .groupby("Employee")["Sales"]
    .cumsum()
)
```

> Employee A gets their own running total. Employee B gets theirs. Separate windows per group.

---

## 📋 Quick Reference

| Function | What it computes |
|---|---|
| `shift(1)` | Previous row value |
| `shift(-1)` | Next row value |
| `diff()` | Current − Previous |
| `pct_change()` | % growth from previous |
| `cumsum()` | Running total |
| `cummax()` | Highest value so far |
| `cummin()` | Lowest value so far |
| `cumprod()` | Running product |
| `rank()` | Row ranking |
| `rolling(n)` | Fixed window of last n rows |
| `expanding()` | All rows up to current |
| `ewm(alpha)` | Recency-weighted average |
| `groupby().cumsum()` | Per-group running total |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook "Window_Functions___Analytical_Operations.ipynb"
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
| 11 | Time Series & DateTime |
| 12 | Performance Optimization |
| 13 | Advanced I/O |
| 14 | Method Chaining & Functional Pandas |
| **15** | **Window Functions & Analytical Operations ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
