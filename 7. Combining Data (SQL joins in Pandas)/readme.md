# 🔗 Pandas Series — EP 07: Combining Data (SQL Joins in Pandas)

Part of my **Pandas Learning Series** — the episode where separate DataFrames finally talk to each other. Real datasets are almost never stored in one table. This notebook covers every tool Pandas gives you to combine, merge, and join data like a pro. 🧩

---

## 📒 About This Notebook

Multiple DataFrames → Combine them → Analyze everything together.

That's the big picture. This notebook walks through the three major combining tools in Pandas (`concat`, `merge`, `join`), all four SQL join types, and the advanced options professionals use on the job.

---

## 🧰 The Three Major Tools

| Tool | What it does |
|---|---|
| `pd.concat()` | Stack DataFrames vertically or horizontally |
| `pd.merge()` | SQL-style joins on a common column |
| `df.join()` | Join on indexes |

---

## 🧠 What's Covered

### 1. 📚 pd.concat() — Stacking Data

**Vertical Concatenation (axis=0)** — stack rows on top of each other:
```python
combined = pd.concat([df1, df2])
```

> ⚠️ Indexes repeat — fix with `ignore_index=True`:
```python
combined = pd.concat([df1, df2], ignore_index=True)
```

**Horizontal Concatenation (axis=1)** — stack columns side by side:
```python
df = pd.concat([names, ages, salaries], axis=1)
```

```
axis=0 → stack rows    → Vertical
axis=1 → stack columns → Horizontal
```

---

### 2. 🔀 pd.merge() — SQL Joins

Basic syntax:
```python
pd.merge(left_df, right_df, on="common_column")
```

#### Inner Join — Keep ONLY matching rows (default)
```python
merged = pd.merge(customers, orders, on="CustomerID")
```
CustomerID 3 exists in customers but not in orders → **dropped**.
CustomerID 4 exists in orders but not in customers → **dropped**.

#### Left Join — Keep all from left, NaN for no match on right
```python
left = pd.merge(customers, orders, on="CustomerID", how="left")
```

#### Right Join — Keep all from right, NaN for no match on left
```python
right = pd.merge(customers, orders, on="CustomerID", how="right")
```

#### Outer Join — Keep EVERYTHING
```python
outer = pd.merge(customers, orders, on="CustomerID", how="outer")
```

---

### 3. 🏷️ Different Column Names
When the key column has different names in each DataFrame:
```python
# customers has "CustomerID", orders has "CustID"
merged = pd.merge(
    customers,
    orders,
    left_on="CustomerID",
    right_on="CustID"
)
```

---

### 4. 🔑 Multiple Keys
Join on more than one column at once:
```python
pd.merge(df1, df2, on=["Department", "Gender"], how="outer")
```

---

### 5. ✏️ Suffixes
When both DataFrames share a column name beyond the key:
```python
pd.merge(
    df1, df2,
    on=["Department", "Gender"],
    how="outer",
    suffixes=("_left", "_right")
)
```
→ `Name_left`, `Name_right`, `Age_left`, `Age_right`

---

### 6. 🔍 indicator=True — Debug Your Joins
```python
pd.merge(
    customers, orders,
    left_on="CustomerID",
    right_on="CustID",
    how="outer",
    indicator=True
)
```
Adds a `_merge` column showing: `both` · `left_only` · `right_only`
Incredibly useful for understanding what matched and what didn't.

---

### 7. 🔗 df.join()
Works on indexes rather than columns. Professionals generally prefer `pd.merge()` because it's more explicit and flexible.

---

## 📊 Join Type Summary

| Join | What it keeps |
|---|---|
| `inner` | Only rows that match in BOTH DataFrames |
| `left` | All rows from left + matching from right (NaN if no match) |
| `right` | All rows from right + matching from left (NaN if no match) |
| `outer` | EVERYTHING — NaN wherever there's no match |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Combining_Data_SQL_joins_in_Pandas_.ipynb
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
| **07** | **Combining Data — SQL Joins in Pandas ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
