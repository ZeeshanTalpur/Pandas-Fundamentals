# ⛓️ Pandas Series — EP 14: Method Chaining & Functional Pandas

Part of my **Pandas Learning Series** — the episode that shows the biggest difference between a beginner and a senior data scientist. Not what they know. How they write it. 🔥

---

## 📒 About This Notebook

Beginners write code that works. Professionals write code that works, reads cleanly, and scales.

This notebook is about **Method Chaining** — the pattern of chaining Pandas operations into a single, readable, linear pipeline instead of creating a new variable at every step.

---

## 🔴 vs ✅ — The Core Difference

**Beginner way:**
```python
df1 = df[df["Salary"] > 50000]
df2 = df1.drop_duplicates()
df3 = df2.sort_values("Salary")
df4 = df3.reset_index(drop=True)
df5 = df4.assign(Bonus=df4["Salary"] * 0.1)
```
It works. But imagine 50 steps. Unreadable.

**Professional way:**
```python
(
    df
    .query("Salary > 50000")
    .drop_duplicates()
    .sort_values("Salary")
    .reset_index(drop=True)
    .assign(Bonus=lambda x: x["Salary"] * 0.1)
)
```
One clean pipeline. That's method chaining.

---

## 🧠 The Pipeline Mental Model

```
Raw Data → Filter → Clean → Create Columns → Sort → Aggregate → Output
```

Every Pandas operation returns a DataFrame. That means the next operation can immediately continue — no intermediate variables needed.

---

## 🧠 What's Covered

### 1. Method Chaining Basics

```python
(
    df
    .drop_duplicates()
    .sort_values("Salary")
    .reset_index(drop=True)
)
```

> **Always wrap with outer parentheses** — allows clean multi-line formatting without backslashes.

---

### 2. assign() — Create Columns Inside the Chain

```python
# Standard
df["Bonus"] = df["Salary"] * 0.1

# Inside a chain
df.assign(
    Bonus=lambda x: x["Salary"] * 0.1,
    Tax=lambda x: x["Bonus"] * 0.2
)
```

> Inside `assign()`, `lambda x` means **current DataFrame after all previous operations**. This lets you reference newly created columns in the same `assign()` call.

---

### 3. query() — Readable Filtering

```python
(
    df
    .query("Salary > 60000 and Department == 'IT'")
)
```

> Cleaner than boolean masking. Reads like a sentence. Fits naturally inside chains.

---

### 4. pipe() — Custom Functions in the Chain

```python
def add_bonus(df):
    df["Bonus"] = df["Salary"] * 0.1
    return df

(
    df
    .pipe(add_bonus)
)
```

> `pipe()` lets you plug any custom function into a chain — as long as it takes a DataFrame and returns a DataFrame.

---

### 5. sort_values() in a Chain

```python
(
    df
    .query("Salary > 50000")
    .sort_values("Salary", ascending=False)
)
```

---

### 6. rename() in a Chain

```python
(
    df
    .rename(columns={"Salary": "Income"})
)
```

---

### 7. Combining Everything — Full Pipeline

```python
def add_bonus(df):
    df["Bonus"] = df["Salary"] * 0.1
    return df

def add_tax(df):
    df["Tax"] = df["Salary"] * 0.05
    return df

(
    df
    .drop_duplicates()
    .query("Salary > 60000")
    .pipe(add_bonus)
    .pipe(add_tax)
    .sort_values("Salary", ascending=False)
    .reset_index(drop=True)
)
```

---

### 8. Reusable Pipelines — Write Once, Use Anywhere

```python
def clean_employee_data(df):
    return (
        df
        .drop_duplicates()
        .dropna()
        .query("Salary > 0")
        .assign(Bonus=lambda x: x["Salary"] * 0.1)
        .reset_index(drop=True)
    )

clean_df = clean_employee_data(df)
```

> Instead of copying the same cleaning steps across every notebook — wrap them in a function and call it once.

---

## ⚡ 5 Professional Rules

| Rule | Why |
|---|---|
| Prefer one pipeline over many temp DataFrames | Readable, debuggable, maintainable |
| Use `assign()` inside the chain | Keeps column creation inline |
| Use `pipe()` for custom logic | Any function can plug into a chain |
| Each step on its own line | One operation = one line |
| Wrap the whole chain in outer `( )` | Clean multi-line formatting |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Method_Chaining_And_Functional_Pandas.ipynb
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
| **14** | **Method Chaining & Functional Pandas ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
