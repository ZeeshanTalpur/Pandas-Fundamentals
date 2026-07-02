# ⚡ Pandas Series — EP 10: Advanced GroupBy

Part of my **Pandas Learning Series** — the episode where GroupBy stops being a summary tool and becomes a full analytics engine. Three functions. Infinite power. 🔥

---

## 📒 About This Notebook

If you can only use `groupby().mean()` — you're using 10% of GroupBy's power.

The real superpowers are:
- `transform()` — same-size output, aligned to the original DataFrame
- `filter()` — keep or drop entire groups
- `apply()` — run any custom logic on each group

Master these three and you can solve most group-wise business problems.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Name":       ["Ali", "Sara", "Ahmed", "Ayesha", "Bilal", "Usman"],
    "Department": ["HR", "HR", "IT", "IT", "Finance", "Finance"],
    "Salary":     [50000, 70000, 90000, 80000, 60000, 75000],
    "Experience": [2, 5, 8, 6, 3, 7]
})
```

---

## 🧠 What's Covered

---

### 1. ⚙️ transform() — Same-Size Output

The key difference from `agg()`:

```python
# agg() → SHRINKS (3 rows for 3 departments)
df.groupby("Department")["Salary"].mean()

# transform() → SAME SIZE (6 rows, aligned to original df)
df.groupby("Department")["Salary"].transform("mean")
```

`transform()` adds the group result back to every row that belongs to that group.

---

**Example 1: Department Average Salary (as new column)**
```python
df["Dept_Avg"] = df.groupby("Department")["Salary"].transform("mean")
```

---

**Example 2: Is This Employee Above or Below Department Average?**
```python
df["Status"] = np.where(
    df["Salary"] > df["Dept_Avg"],
    "Above Average",
    "Below Average"
)
```
> Industry use: HR dashboards, performance analysis, compensation benchmarking.

---

**Example 3: Group-wise Z-Score Normalization**
```python
df["Salary_z"] = df.groupby("Department")["Salary"].transform(
    lambda x: (x - x.mean()) / x.std()
)
```
> Standardize within each group — not across the whole dataset.

---

**Example 4: Rankings Within Groups**
```python
df["Rank"] = df.groupby("Department")["Salary"].rank(ascending=False)
```
> Rank 1 = highest earner in that department.

---

### 2. 🔍 filter() — Keep or Remove Entire Groups

`filter()` operates on entire groups — not individual rows.

```
Group → Test condition → Keep all rows? or Drop all rows?
```

**Example 1: Keep departments with average salary > 70,000**
```python
df.groupby("Department").filter(
    lambda x: x["Salary"].mean() > 70000
)
```

**Example 2: Keep large departments (≥ 3 employees)**
```python
df.groupby("Department").filter(
    lambda x: len(x) >= 3
)
```

**Industry use cases:**
- Remove tiny customer segments before analysis
- Remove rare/sparse categories
- Drop cities with insufficient data
- Keep only statistically valid groups

---

### 3. 🛠️ apply() — Custom Group Processing

```
agg()       → simple summaries (mean, sum, count)
transform() → same-size output, row-aligned
apply()     → ANYTHING
```

**Example 1: Salary Range per Department**
```python
def salary_range(group):
    return group.max() - group.min()

df.groupby("Department")["Salary"].apply(salary_range)
```

**Example 2: Top Earner in Every Department**
```python
def top_employee(group):
    return group.nlargest(1)

df.groupby("Department")["Salary"].apply(top_employee)
```

---

## 🧭 Decision Guide — Which One to Use?

| You want to... | Use |
|---|---|
| Add group result back to the original DataFrame | `transform()` |
| Keep or remove entire groups based on a condition | `filter()` |
| Run custom logic and return any kind of output | `apply()` |
| Simple summary (mean, sum, count) | `agg()` |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Advanced_GroupBy.ipynb
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
| **10** | **Advanced GroupBy ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
