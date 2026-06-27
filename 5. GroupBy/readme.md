# 🗂️ Pandas Series — EP 05: GroupBy Mastery

Part of my **Pandas Learning Series** — arguably the most important episode yet. Many people know Pandas. Far fewer truly understand `groupby()`. Yet most business questions in the real world are GroupBy problems in disguise. 💼

---

## 📒 About This Notebook

If you've ever been asked "what's the average salary by department?" or "how many orders per month?" — congratulations, you've been asked a GroupBy question. This notebook covers the complete GroupBy toolkit, from basic grouping through named aggregations, multi-column grouping, and sorting results.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Name":       ["Ali","Sara","Ahmed","Ayesha","Bilal","Usman"],
    "Department": ["HR","IT","IT","Finance","HR","Finance"],
    "Age":        [22, 25, 30, 28, 35, 40],
    "Salary":     [50000, 70000, 90000, 80000, 120000, 100000]
})
```

---

## ⚙️ The Core Philosophy — Split → Apply → Combine

```
Split   → Divide the DataFrame into groups based on a column
Apply   → Run a function on each group
Combine → Bring the results back together
```

---

## 🧠 What's Covered

### 1. Basic GroupBy
```python
group = df.groupby("Department")
group.groups               # dict of group → row indices
group.groups.keys()        # group names
list(group.groups.keys())  # as list
```
> Just creating groups — no computation yet. It's preparation.

### 2–8. Core Aggregations
```python
df.groupby("Department")["Salary"].mean()    # avg per group
df.groupby("Department")["Salary"].sum()     # total per group
df.groupby("Department")["Salary"].max()     # highest per group
df.groupby("Department")["Salary"].min()     # lowest per group
df.groupby("Department")["Salary"].median()  # median per group
df.groupby("Department")["Salary"].std()     # spread per group

df.groupby("Department")["Name"].count()  # ignores NaN
df.groupby("Department")["Name"].size()   # counts everything
```
> **Key difference:** `count()` skips NaN. `size()` counts every row.

### 9. Multiple Aggregations with agg()
```python
df.groupby("Department")["Salary"].agg(
    ["sum", "mean", "median", "max", "min", "count", "std"]
)
```

### 10. Named Aggregations — Professional Output
```python
df.groupby("Department").agg(
    AverageSalary = ("Salary", "mean"),
    HighestSalary = ("Salary", "max"),
    LowestSalary  = ("Salary", "min"),
    EmployeeCount = ("Name",   "size")
)
```
> Cleaner column names. Easier to read. Ready to export.

### 11. Grouping by Multiple Columns
```python
df.groupby(["Department", "Gender"])["Salary"].mean()
```
Creates a **Multi-Index** — one level for each grouping column.

### 12. as_index=False — Flat Output
```python
df.groupby("Department", as_index=False)["Salary"].mean()
```
Department becomes a regular column instead of the index. Useful before saving to CSV.

### 13. Sorting Group Results
```python
df.groupby("Department")["Salary"].mean().sort_values(ascending=False)
```

---

## 💼 Real Business Questions = GroupBy Problems

| Business Question | GroupBy Code |
|---|---|
| Average salary per department | `groupby("Department")["Salary"].mean()` |
| Total sales per city | `groupby("City")["Sales"].sum()` |
| Max spending per customer type | `groupby("Type")["Spend"].max()` |
| Number of orders per month | `groupby("Month")["OrderID"].count()` |
| Average marks per class | `groupby("Class")["Marks"].mean()` |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook GroupBy.ipynb
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
| **05** | **GroupBy Mastery ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
