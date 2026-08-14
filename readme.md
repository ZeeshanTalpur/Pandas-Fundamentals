# 🐼 Pandas Fundamentals

A complete, from-scratch Pandas learning series — built notebook by notebook, documented thoroughly, and shared publicly as I learned. This repository covers everything from creating your first Series to writing production-grade data pipelines, window functions, and regex-powered string processing. 🚀

> **Stack:** Python · Pandas · NumPy · Jupyter Notebook
> **Duration:** 16 episodes — beginner to professional
> **Goal:** Master Pandas as a complete data manipulation and analysis tool, ready for real-world Data Science and ML workflows.

---

## 🗂️ Repository Structure

```
Pandas-Fundamentals/
│
├── 1.  Series and DataFrames
├── 2.  Indexing and Slicing
├── 3.  Data Cleaning
├── 4.  Exploratory Data Analysis
├── 5.  GroupBy
├── 6.  Transformation & Feature Engineering
├── 7.  Combining Data (SQL joins in Pandas)
├── 8.  SQL Thinking with Pandas
├── 9.  Multi Index
├── 10. Advanced GroupBy
├── 11. Time Series & DateTime
├── 12. Performance Optimization & Memory Efficiency
├── 13. Advanced Input Output
├── 14. Method Chaining and Functional Pandas
├── 15. Window Functions and Analytical Operations
└── 16. Advanced String Processing
```

Each folder contains a Jupyter notebook and its own dedicated README.

---

## 📚 Complete Episode Guide

### 🟢 Phase 1 — Foundations (Episodes 1–4)

| # | Topic | What You Learn |
|---|---|---|
| 1 | **Series & DataFrames** | The two core Pandas data structures, creation, attributes, basic operations |
| 2 | **Indexing & Slicing** | `.loc`, `.iloc`, boolean indexing, label vs position, fancy indexing |
| 3 | **Data Cleaning** | Missing values (7 methods), duplicates, dtype fixes, text cleaning, 5-check muscle memory |
| 4 | **Exploratory Data Analysis** | `describe()`, mean/median/mode, std/variance, `value_counts()`, quartiles, correlation, outlier detection |

---

### 🟡 Phase 2 — Core Manipulation (Episodes 5–8)

| # | Topic | What You Learn |
|---|---|---|
| 5 | **GroupBy Mastery** | Split-Apply-Combine, all core aggregations, named agg, multi-column grouping, `as_index`, sorting |
| 6 | **Transformation & Feature Engineering** | New columns, `map()`, `replace()`, `apply()`, `np.where()`, `cut()`, `qcut()`, `assign()` |
| 7 | **Combining Data — SQL Joins** | `pd.concat()`, `pd.merge()`, all 4 join types, `left_on`/`right_on`, `suffixes`, `indicator=True` |
| 8 | **SQL Thinking with Pandas** | 15 SQL operations translated to Pandas — SELECT, WHERE, GROUP BY, HAVING, JOIN, UNION, UPDATE, DELETE |

---

### 🔵 Phase 3 — Advanced (Episodes 9–12)

| # | Topic | What You Learn |
|---|---|---|
| 9 | **MultiIndex Mastery** | `set_index()`, `.loc` with tuples, GroupBy → MultiIndex, `stack()`/`unstack()`, `swaplevel()`, `xs()` |
| 10 | **Advanced GroupBy** | `transform()`, `filter()`, `apply()` — the three GroupBy superpowers beyond `agg()` |
| 11 | **Time Series & DateTime** | `to_datetime()`, `.dt` accessor, partial indexing, `date_range()`, `resample()`, `rolling()`, `expanding()`, `shift()` |
| 12 | **Performance Optimization** | Memory measurement, `astype()` downcasting, `category` dtype, vectorization, `itertuples()`, `query()`, `eval()`, `chunksize`, `.copy()` |

---

### 🔴 Phase 4 — Professional (Episodes 13–16)

| # | Topic | What You Learn |
|---|---|---|
| 13 | **Advanced I/O** | CSV (all params), Excel (multi-sheet), JSON, Parquet, SQL databases, URLs, `usecols`, `dtype`, `chunksize`, `nrows` |
| 14 | **Method Chaining & Functional Pandas** | Chaining philosophy, `assign()`, `query()`, `pipe()`, reusable pipeline functions, 5 professional rules |
| 15 | **Window Functions & Analytical Operations** | `shift()`, `diff()`, `pct_change()`, `cumsum()`, `cummax()`, `cummin()`, `rank()`, `rolling()`, `expanding()`, `ewm()`, groupwise windows |
| 16 | **Advanced String Processing** | 15 `.str` methods — `lower/upper/title`, `strip`, `replace`, `contains`, `split`, `extract`, `extractall`, `findall`, `match`, `fullmatch` |

---

## 🛠️ Complete Skills Index

### Data Structures
- Series creation, attributes, operations
- DataFrame creation from dict, list, CSV
- `.shape`, `.dtypes`, `.info()`, `.head()`, `.tail()`

### Selection & Filtering
- `.loc[]` (label-based), `.iloc[]` (position-based)
- Boolean masking, `&`, `|`, `~`
- `query()` string-based filtering
- Fancy indexing

### Data Cleaning
- `isna()`, `fillna()` (7 strategies), `dropna()`
- `ffill()`, `bfill()`
- `drop_duplicates()`
- `astype()` for type conversion
- `pd.to_numeric(errors="coerce")`
- `str.strip()`, `str.title()`, `str.replace()`

### Aggregation & Grouping
- `groupby()` — single and multi-column
- Core agg: `mean`, `sum`, `max`, `min`, `median`, `std`, `count`, `size`
- `agg([...])` — multiple at once
- Named aggregations
- `transform()`, `filter()`, `apply()`

### Feature Engineering
- `assign()` for new columns
- `map()` vs `replace()`
- `np.where()` for conditional labeling
- `pd.cut()` (equal width) and `pd.qcut()` (equal frequency)
- `apply()` with lambdas and named functions

### Combining Data
- `pd.concat()` — axis=0 (vertical), axis=1 (horizontal)
- `pd.merge()` — inner, left, right, outer joins
- `left_on`, `right_on`, `suffixes`, `indicator=True`

### SQL Equivalents
- SELECT → `df[[cols]]`
- WHERE → `df[condition]`
- GROUP BY → `.groupby()`
- HAVING → filter after groupby
- JOIN → `pd.merge()`
- UNION → `pd.concat()`
- CASE WHEN → `np.where()`
- UPDATE → `df["col"] = value`
- DELETE → `df = df[condition]`

### Hierarchical Indexing
- `set_index()` / `reset_index()`
- MultiIndex with `.loc[("L1", "L2")]`
- `stack()` / `unstack()`
- `swaplevel()` + `sort_index()`
- `xs()` cross-sections

### Time Series
- `pd.to_datetime()`, `.dt` accessor
- Partial string indexing
- `pd.date_range()` with frequency codes
- `resample()` — GroupBy for time
- `rolling(n)` — moving window
- `expanding()` — cumulative window
- `shift()`, `diff()`, `pct_change()`

### Window & Analytical Functions
- `cumsum()`, `cummax()`, `cummin()`, `cumprod()`
- `rank()` with `average`, `dense`, `first`
- `rolling()` — mean, sum, min, max, std
- `expanding()` — growing window
- `ewm(alpha)` — exponential weighting
- Group-wise windows via `groupby().cumsum()`

### Performance & Memory
- `memory_usage()`, `memory_usage(deep=True)`
- `astype("int32")`, `astype("float32")`, `astype("category")`
- Vectorization over loops and `apply()`
- `itertuples()` over `iterrows()`
- `query()` and `eval()`
- `pd.read_csv(usecols=..., dtype=..., chunksize=...)`
- `.copy()` to prevent `SettingWithCopyWarning`

### I/O
- CSV: `read_csv()`, `to_csv(index=False)`
- Excel: `read_excel()`, `to_excel()`, multi-sheet
- JSON: `read_json()`, `to_json()`
- Parquet: `read_parquet()`, `to_parquet()`
- SQL: `read_sql()`, `to_sql(if_exists=...)`
- URL: direct `read_csv("https://...")`

### String Processing (`.str` accessor)
- Case: `lower()`, `upper()`, `title()`
- Space: `strip()`, `lstrip()`, `rstrip()`
- Substitution: `replace()` (text + regex)
- Search: `contains()`, `startswith()`, `endswith()`
- Split: `split(expand=True)`
- Combine: `cat(sep=...)`
- Measure: `len()`, `slice()`
- Regex extract: `extract()`, `extractall()`, `findall()`
- Regex check: `match()`, `fullmatch()`

### Method Chaining
- Pipeline with outer `( )`
- `assign()` inside chains
- `pipe()` for custom functions
- `query()` for inline filtering
- Reusable pipeline functions

---

## 🚀 Getting Started

```bash
git clone https://github.com/ZeeshanTalpur/Pandas-Fundamentals.git
cd Pandas-Fundamentals
jupyter notebook
```

**Requirements:**

```bash
pip install pandas numpy openpyxl pyarrow jupyter
```

---

## 📖 How to Use This Repo

| You are... | Start here |
|---|---|
| Complete beginner | Folder `1. Series and DataFrames` — work through in order |
| Know Python basics | Folder `3. Data Cleaning` — the most important episode |
| Comfortable with basics | Folder `5. GroupBy` — where real analysis starts |
| Want applied SQL skills | Folder `8. SQL Thinking with Pandas` |
| Working with dates/time data | Folder `11. Time Series & DateTime` |
| Worried about performance | Folder `12. Performance Optimization` |
| Want professional code style | Folder `14. Method Chaining` |
| Cleaning messy text | Folder `16. Advanced String Processing` |

---

## 🗺️ What's Next

With Pandas complete, the journey continues into:

- 📊 **Data Visualization** — Matplotlib & Seaborn
- 🤖 **Machine Learning** — Scikit-learn
- 🏗️ **Data Engineering** — pipelines, ETL, SQL databases

---

## 🙋 About Me

I'm **Zeeshan**, a Software Engineering student at Mehran University of Engineering & Technology (MUET), Jamshoro — learning Data Science and AI in public, one notebook at a time. 🌱

Every episode in this repository was documented and shared publicly on LinkedIn and GitHub as I built it. This isn't a course. It's a learning log.

📎 [LinkedIn](https://linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

---

More learning, more building, more data coming up! ✨