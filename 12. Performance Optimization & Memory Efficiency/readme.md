# ⚡ Pandas Series — EP 12: Performance Optimization & Memory Efficiency

Part of my **Pandas Learning Series** — the episode that separates beginners from professionals. Anyone can write Pandas code that works. This episode is about writing code that's **fast, memory-efficient, production-ready, and scalable**. 🔥

---

## 📒 About This Notebook

Most beginners only care about making code work.

**Professionals ask different questions:**
- How much RAM does this use?
- How much time does this take?
- Will this work on 50 million rows?

This notebook answers all three.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "ID":         np.arange(100000),
    "Department": np.random.choice(["HR","IT","Finance"], 100000),
    "Salary":     np.random.randint(40000, 150000, 100000)
})
```
100,000 rows — large enough to feel the performance difference.

---

## 🧠 What's Covered

### 1. 📏 Measuring Memory Usage

> **First rule:** You cannot optimize what you don't measure.

```python
df.memory_usage()              # per column (bytes)
df.memory_usage().sum()        # total bytes
df.memory_usage().sum() / 1024**2   # in MB

df.info(memory_usage="deep")   # actual string sizes included
```

> ⚠️ `object` dtype stores pointers to Python objects. The actual strings live elsewhere in RAM. Use `memory_usage="deep"` to see true usage.

---

### 2. 🔽 astype() — Downcast Your Types

```python
# Professional Rule: Use the smallest datatype that safely holds your values

df["Salary"].astype("int32")     # saves vs int64
df["Age"].astype("int16")        # for small integers
df["Score"].astype("float32")    # saves vs float64
```

---

### 3. 🏷️ category dtype — The Biggest Memory Win

For columns with repeated string values:

```python
df["Department"] = df["Department"].astype("category")
```

**Before:** Every row stores a full string → `"HR"`, `"HR"`, `"IT"`, `"Finance"`...

**After:** Stores integers internally:
```
Categories: 0→Finance  1→HR  2→IT
Row data:   1 1 1 2 2 0 1 2...
```

> Massive memory reduction. Use this any time you have a column with repeated values.

---

### 4. ⚡ Vectorization — Always First Choice

```python
# ❌ BAD — loop: extremely slow
for i in range(len(df)):
    df.loc[i, "Bonus"] = df.loc[i, "Salary"] * 0.1

# ❌ BAD — apply(): also slow
df["Bonus"] = df["Salary"].apply(lambda x: x * 0.1)

# ✅ GOOD — vectorized: fast
df["Bonus"] = df["Salary"] * 0.1
```

> **Rule:** Vectorization almost always wins. Reach for `apply()` only when no vectorized option exists.

---

### 5. 🔁 iterrows() vs itertuples()

When loops are genuinely unavoidable:

```python
# ❌ BAD — iterrows(): converts each row to a Series
for index, row in df.iterrows():
    print(row["Salary"])

# ✅ GOOD — itertuples(): returns namedtuples, way faster
for row in df.itertuples():
    print(row.Salary)
```

> **Professional Rule:** Never use `iterrows()` unless absolutely necessary.

---

### 6. 🔍 query() — Cleaner Filtering

```python
# Standard
df[(df["Salary"] > 80000) & (df["Department"] == "IT")]

# With query() — cleaner, sometimes faster, less memory
df.query("Salary > 80000 and Department == 'IT'")
```

> Industry teams often prefer `query()` for complex conditions.

---

### 7. 🧮 eval() — Compute Expressions Efficiently

```python
# Standard
df["Tax"] = df["Salary"] * 0.2 + df["Bonus"] * 0.1

# With eval() — uses less temporary memory
df.eval("Tax = Salary*0.2 + Bonus*0.1", inplace=True)
```

> More useful on huge datasets where temporary arrays eat RAM.

---

### 8. 📦 Chunk Processing — For Files That Don't Fit in RAM

```python
# Suppose: 5 GB CSV, 8 GB RAM — you can't load it all at once
for chunk in pd.read_csv("big_file.csv", chunksize=10000):
    # process each chunk
    result = chunk.groupby("Department")["Salary"].sum()
```

> **This is how ETL pipelines work.**

---

### 9. 📖 Efficient CSV Reading

```python
# ❌ BAD — reads everything
pd.read_csv("data.csv")

# ✅ GOOD — only read what you need
pd.read_csv(
    "data.csv",
    usecols=["Salary", "Department"],
    dtype={"Salary": "int32", "Department": "category"}
)
```

> Specify `dtype` at read time — saves memory immediately before any processing starts.

---

### 10. 📋 copy() — Avoid SettingWithCopyWarning

```python
# ❌ BAD — causes SettingWithCopyWarning
high_salary = df[df["Salary"] > 80000]
high_salary["Bonus"] = 10000   # might not modify df

# ✅ GOOD — explicit copy, works safely
high_salary = df[df["Salary"] > 80000].copy()
high_salary["Bonus"] = 10000   # safe ✅
```

> **Professional Rule:** If you're creating a separate DataFrame to modify — always `.copy()`.

---

## ⚡ Professional Rules Summary

| Rule | Why |
|---|---|
| Measure memory first | Can't optimize blind |
| `category` for repeated strings | Biggest single memory win |
| Never `iterrows()` | `itertuples()` is far faster |
| Always `.copy()` | Prevents silent bugs and warnings |
| Vectorize first | Loops and `apply()` are last resort |
| `usecols` + `dtype` at read | Save memory before processing starts |
| `chunksize` for big files | Handle files larger than RAM |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Performace_Optimization_and_Memory_Efficiency.ipynb
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
| **12** | **Performance Optimization & Memory Efficiency ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
