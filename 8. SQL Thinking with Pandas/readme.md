# 🗄️ Pandas Series — EP 08: SQL Thinking with Pandas

Part of my **Pandas Learning Series** — the episode that bridges two worlds. SQL and Pandas are deeply connected. Every role in the data industry uses both. This notebook translates 15 core SQL operations directly into Pandas, side by side. 🔗

---

## 📒 About This Notebook

SQL operates on tables. Pandas operates on DataFrames. They think the same way.

If you know SQL, this notebook shows you exactly what each query looks like in Pandas. If you know Pandas, this notebook makes SQL intuitive instantly.

> **Data Scientists · Data Analysts · Data Engineers · ML Engineers** — all use both. Always.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Name":       ["Ali", "Sara", "Ahmed", "Ayesha", "Bilal"],
    "Age":        [22, 25, 30, 28, 35],
    "Salary":     [50000, 70000, 90000, 80000, 120000],
    "Department": ["HR", "IT", "IT", "Finance", "HR"]
})
```

---

## 🧠 15 SQL Operations → Pandas

### 1. SELECT
```sql
SELECT Name, Salary FROM Employees;
```
```python
df[["Name", "Salary"]]
```

---

### 2. WHERE (Single & Multiple Conditions)
```sql
SELECT * FROM Employees WHERE Salary > 80000;
SELECT * FROM Employees WHERE Department='IT' AND Salary > 70000;
```
```python
df[df["Salary"] > 80000]
df[(df["Department"] == "IT") & (df["Salary"] > 70000)]
```

---

### 3. ORDER BY
```sql
SELECT * FROM Employees ORDER BY Salary DESC;
ORDER BY Department ASC, Salary DESC;
```
```python
df.sort_values("Salary", ascending=False)
df.sort_values(["Department", "Salary"], ascending=[True, False])
```

---

### 4. LIMIT
```sql
SELECT * FROM Employees LIMIT 3;
SELECT * FROM Employees ORDER BY id DESC LIMIT 3;
```
```python
df.head(3)
df.tail(3)
```

---

### 5. DISTINCT
```sql
SELECT DISTINCT Department FROM Employees;
SELECT COUNT(DISTINCT Department) FROM Employees;
```
```python
df["Department"].unique()
df["Department"].nunique()
```

---

### 6. GROUP BY
```sql
SELECT Department, AVG(Salary), MAX(Salary), COUNT(*)
FROM Employees
GROUP BY Department;
```
```python
df.groupby("Department")["Salary"].agg(["mean", "max", "count"])
```

---

### 7. HAVING
```sql
SELECT Department, AVG(Salary)
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 85000;
```
```python
grouped = df.groupby("Department")["Salary"].mean()
grouped[grouped > 85000]
```
> `WHERE` filters before grouping. `HAVING` filters after. In Pandas, just filter the grouped result.

---

### 8. INNER JOIN
```sql
SELECT * FROM Customers INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```
```python
pd.merge(customers, orders, on="CustomerID")
```

---

### 9. LEFT JOIN
```sql
SELECT * FROM Customers LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```
```python
pd.merge(customers, orders, on="CustomerID", how="left")
```

---

### 10. UNION ALL
```sql
SELECT * FROM Employees2024 UNION ALL SELECT * FROM Employees2025;
```
```python
pd.concat([df1, df2], ignore_index=True)
```

---

### 11. CASE WHEN
```sql
CASE WHEN Salary > 100000 THEN 'Gold' ELSE 'Silver' END
```
```python
import numpy as np
df["Tier"] = np.where(df["Salary"] > 100000, "Gold", "Silver")
```

---

### 12. IS NULL / IS NOT NULL
```sql
WHERE Salary IS NULL;
WHERE Salary IS NOT NULL;
```
```python
df[df["Salary"].isna()]
df[df["Salary"].notna()]
```

---

### 13. UPDATE
```sql
UPDATE Employees SET Salary = Salary * 1.1;
UPDATE Employees SET Bonus = 10000 WHERE Salary > 80000;
```
```python
df["Salary"] *= 1.1
df.loc[df["Salary"] > 80000, "Bonus"] = 10000
```

---

### 14. DELETE
```sql
DELETE FROM Employees WHERE Salary < 60000;
```
```python
df = df[df["Salary"] >= 60000]
```

---

### 15. Full Query Translation
```sql
SELECT Name, Salary
FROM Employees
WHERE Department = 'IT'
ORDER BY Salary DESC
LIMIT 2;
```
```python
df[df["Department"] == "IT"][["Name", "Salary"]]\
  .sort_values("Salary", ascending=False)\
  .head(2)
```

---

## 📋 SQL → Pandas Cheatsheet

| SQL | Pandas |
|---|---|
| `SELECT col` | `df[["col"]]` |
| `WHERE condition` | `df[df[condition]]` |
| `ORDER BY col DESC` | `.sort_values("col", ascending=False)` |
| `LIMIT n` | `.head(n)` |
| `DISTINCT` | `.unique()` |
| `COUNT(DISTINCT)` | `.nunique()` |
| `GROUP BY` | `.groupby()` |
| `HAVING` | filter after `.groupby()` |
| `INNER JOIN` | `pd.merge(df1, df2, on="key")` |
| `LEFT JOIN` | `pd.merge(..., how="left")` |
| `UNION ALL` | `pd.concat([df1, df2], ignore_index=True)` |
| `CASE WHEN` | `np.where()` |
| `IS NULL` | `.isna()` |
| `IS NOT NULL` | `.notna()` |
| `UPDATE SET` | `df["col"] = new_value` |
| `DELETE WHERE` | `df = df[condition]` |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook SQL_Thinking_with_Pandas.ipynb
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
| **08** | **SQL Thinking with Pandas ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
