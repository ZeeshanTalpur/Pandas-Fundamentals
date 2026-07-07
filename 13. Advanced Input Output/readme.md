# 📁 Pandas Series — EP 13: Advanced Input/Output (I/O)

Part of my **Pandas Learning Series** — the episode that connects Pandas to the real world. Data doesn't live in your notebook. It lives in CSV files, Excel sheets, JSON APIs, Parquet files, SQL databases, and URLs. This notebook teaches you how to read and write all of them — the right way. 🔌

---

## 📒 About This Notebook

Every data pipeline starts with reading data and ends with saving it somewhere. This notebook covers every major I/O format Pandas supports, plus the smart reading parameters professionals use to keep things fast, clean, and memory-efficient from the first line.

---

## 🧠 What's Covered

---

### 1. 📄 CSV Files — The Most Common Format

```python
# Reading
df = pd.read_csv("customers.csv")

# Saving — ❌ creates extra index column
df.to_csv("output.csv")

# Saving — ✅ correct way
df.to_csv("output.csv", index=False)
```

> `read_csv()` is probably the single most-used Pandas function in industry.

---

### 2. 🎯 Selecting Specific Columns While Reading

```python
# ❌ Bad — loads everything
df = pd.read_csv("customers.csv")

# ✅ Good — only load what you need
df = pd.read_csv(
    "customers.csv",
    usecols=["First Name", "Last Name", "City"]
)
```

**Benefits:** Faster · Less RAM · Cleaner · Professional standard for large datasets.

---

### 3. 🔽 Specifying Data Types at Read Time

```python
df = pd.read_csv(
    "customers.csv",
    usecols=["Country"],
    dtype={"Country": "category"}
)
```

> Faster and more memory-efficient than loading first and converting after.

---

### 4. 🕳️ Handling Missing Values During Import

```python
df = pd.read_csv(
    "customers.csv",
    na_values=["NA", "Missing"]   # treat these as NaN
)
```

---

### 5. 📦 Reading Large CSVs in Chunks

```python
chunks = pd.read_csv("customers.csv", chunksize=10000)

for chunk in chunks:
    # process each chunk
    result = chunk.groupby("City")["Salary"].mean()
```

> This is exactly how ETL pipelines work. Use when the file is too large to load all at once.

---

### 6. 📊 Excel Files

```python
# Read entire file
df = pd.read_excel("output.xlsx")

# Read specific sheet
df = pd.read_excel("output.xlsx", sheet_name="Sheet1")

# Read ALL sheets — returns dict: {sheet_name: DataFrame}
df = pd.read_excel("output.xlsx", sheet_name=None)

# Save
df.to_excel("report.xlsx", index=False)
```

---

### 7. 🌐 JSON Files

```python
df = pd.read_json("data.json")
df.to_json("employees.json")
```

> Common in API response pipelines and web data workflows.

---

### 8. 🗜️ Parquet Files

```python
df = pd.read_parquet("employees.parquet")
df.to_parquet("employees.parquet")
```

**Why Parquet over CSV?**
- Smaller file size (compressed)
- Typed (dtypes preserved)
- Much faster to read
- Industry standard in big data (Spark, Hadoop, cloud warehouses)

---

### 9. 🗄️ SQL Databases

```python
# Read — simple query
df = pd.read_sql("SELECT * FROM employees", connection)

# Read — filtered query
query = """
SELECT Name, Salary
FROM employees
WHERE Salary > 70000
"""
df = pd.read_sql(query, connection)

# Save back to database
df.to_sql(
    "employees",
    connection,
    if_exists="replace",   # "replace" · "append" · "fail"
    index=False
)
```

> **Typical workflow:** Database → Pandas → Analysis → Dashboard / Machine Learning

---

### 10. 🔗 Reading from URLs

```python
df = pd.read_csv("https://example.com/data.csv")
```

> Pandas can read directly from URLs — no manual download needed. Works for CSV, Excel, JSON.

---

### 11. ⚙️ Common Parameters to Know Cold

```python
# Read first 100 rows only
pd.read_csv("data.csv", nrows=100)

# Skip first 5 rows
pd.read_csv("data.csv", skiprows=5)

# Semicolon-separated file
pd.read_csv("data.csv", sep=";")

# File has no header row
pd.read_csv("data.csv", header=None)

# Assign custom column names
pd.read_csv("data.csv", names=["ID", "Name", "Salary"])
```

---

## 📋 Format Guide — When to Use What

| Format | Use When |
|---|---|
| **CSV** | Daily data exchange, simple workflows |
| **Excel** | Business reports, stakeholder deliverables |
| **JSON** | API responses, web data |
| **Parquet** | Big data, cloud pipelines, production |
| **SQL** | Production databases, real-time data |
| **URL** | Open datasets, quick prototyping |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Advanced_Input_Output_IO_.ipynb
```

**Requirements:** Python 3.x · Pandas · openpyxl · Jupyter Notebook

```bash
pip install pandas openpyxl pyarrow jupyter
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
| 12 | Performance Optimization & Memory Efficiency |
| **13** | **Advanced Input/Output (I/O) ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
