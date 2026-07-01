# 🌳 Pandas Series — EP 09: MultiIndex Mastery

Part of my **Pandas Learning Series** — the episode that takes indexing to the next level. MultiIndex is what happens when one level of grouping isn't enough. This notebook covers everything from creating hierarchical indexes to slicing through them with advanced tools like `xs()`. 🎯

---

## 📒 About This Notebook

Instead of a flat index, MultiIndex gives you a hierarchy — like an org chart for your data. This notebook walks through creating, accessing, stacking, unstacking, and cross-sectioning multi-level DataFrames.

---

## 🌳 The Hierarchy Concept

```
Company
├── HR
│   ├── Male
│   └── Female
└── IT
    ├── Male
    └── Female
```

Internally, the index becomes **tuples**:
```python
MultiIndex([
    ('HR', 'M'),
    ('HR', 'F'),
    ('IT', 'M'),
    ('IT', 'F')
])
```

That's a MultiIndex.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Name":       ["Ahmed", "Tooba", "Mushtaq", "Sania"],
    "Department": ["HR", "HR", "IT", "IT"],
    "Gender":     ["M", "F", "M", "F"],
    "Salary":     [50000, 70000, 80000, 90000]
})
```

---

## 🧠 What's Covered

### 1. set_index() — Create a MultiIndex
```python
# Single index
multi = df.set_index("Department")

# Multi-level index
multi = df.set_index(["Department", "Gender"])
# Level 1: Department
# Level 2: Gender
```

### 2. reset_index() — Flatten Back to Normal
```python
normal = multi.reset_index()
```
```
set_index()   → columns → indexes
reset_index() → indexes → columns
```

### 3. Accessing with .loc
```python
multi.loc["HR"]           # all HR employees
multi.loc[("HR", "M")]    # HR + Male only (pass as tuple)
```

### 4. GroupBy → MultiIndex (and how to handle it)

**GroupBy on multiple columns automatically creates a MultiIndex result:**
```python
result = df.groupby(["Department", "Gender"])["Salary"].mean()
```

**Two ways to fix it:**
```python
# Option 1: reset after groupby
result = result.reset_index()

# Option 2: prevent it from the start (professional preferred)
result = df.groupby(["Department", "Gender"], as_index=False)["Salary"].mean()
```

### 5. stack() — Columns → Index Level
```python
students = pd.DataFrame({
    "Math":    [90, 85],
    "Physics": [80, 95]
}, index=["Ali", "Sara"])

students.stack()
# Math and Physics become another index level
```

### 6. unstack() — Index Level → Columns (Reverse of stack)
```python
students.unstack()
```
```
stack()   ≈ set_index()   → columns become index
unstack() ≈ reset_index() → index becomes columns
```

### 7. MultiIndex Columns
Rows aren't the only things that can have multiple levels — columns can too.

```python
data = {
    ("Math", "Midterm"): [90, 85],
    ("Math", "Final"):   [95, 88],
    ("Physics", "Midterm"): [80, 92],
    ("Physics", "Final"):   [85, 96]
}
marks = pd.DataFrame(data, index=["Ali", "Sara"])

marks["Math"]                  # all Math scores
marks["Physics"]               # all Physics scores
marks[("Math", "Final")]       # Math Final only
```

### 8. swaplevel() — Reorder Hierarchy Levels
```python
multi.swaplevel()
# Department/Gender → Gender/Department
```

### 9. sort_index() — Always Sort After Swapping
```python
multi.swaplevel().sort_index()
```
> ⚠️ An unsorted MultiIndex can cause unexpected errors when slicing. Always `sort_index()` after `swaplevel()`.

### 10. xs() — Cross Sections (Advanced)
Cut through any level of the MultiIndex without specifying the other levels.

```python
# Give me all Male employees regardless of department
multi.xs("M", level="Gender")

# Give me all HR employees regardless of gender
multi.xs("HR", level="Department")
```
> `xs` = cross section = cut through any level directly.

---

## 💡 Key Rules Summary

| Operation | Direction | Method |
|---|---|---|
| Columns → Index | `set_index()` |
| Index → Columns | `reset_index()` |
| Columns → Index level | `stack()` |
| Index level → Columns | `unstack()` |
| Prevent MultiIndex from groupby | `as_index=False` |
| Reorder levels | `swaplevel()` |
| Sort after reordering | `sort_index()` |
| Cut through any level | `xs(val, level="name")` |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Multi_Index.ipynb
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
| **09** | **MultiIndex Mastery ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
