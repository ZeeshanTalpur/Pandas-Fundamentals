# 🔍 Pandas Series — EP 02: Indexing & Slicing Mastery

Part of my **Pandas Learning Series** — where data stops being nameless rows and becomes something you can actually talk to. This episode is about accessing exactly what you need, exactly how you want it. 🎯

---

## 📒 About This Notebook

NumPy gives you positions. Pandas gives you labels, names, conditions, and positions — all at once. This notebook covers every selection method in Pandas, when to use each one, and the one key rule that trips up every NumPy user switching to Pandas.

---

## 🧠 The Big Idea

Every selection problem in Pandas is just two questions:
> **Which rows?** + **Which columns?** = done.

---

## 🧠 What's Covered

### Dataset Used
```python
df = pd.DataFrame({
    "Name":       ["Ali","Sara","Ahmed","Ayesha","Bilal"],
    "Age":        [22, 25, 30, 28, 35],
    "Salary":     [50000, 70000, 90000, 80000, 120000],
    "Department": ["HR","IT","IT","Finance","HR"]
})
df.index = [101, 102, 103, 104, 105]
```

---

### 1. 📋 Selecting Columns
```python
df["Salary"]              # single column → Series
df[["Name", "Salary"]]   # multiple columns → DataFrame
```

---

### 2. 🏷️ loc[ ] — Label Based
```python
df.loc[102]                        # single row by label
df.loc[[101, 104]]                 # multiple rows
df.loc[101:103]                    # range — UPPER LIMIT INCLUSIVE ✅
df.loc[102:105, ["Age","Salary"]]  # rows + columns together
```
> ⚠️ `loc` upper limit is **inclusive** — unlike NumPy.

---

### 3. 🔢 iloc[ ] — Position Based
```python
df.iloc[1]             # single row by position
df.iloc[[1, 4]]        # multiple rows
df.iloc[2:4]           # range — UPPER LIMIT EXCLUSIVE (like NumPy)
df.iloc[3, 1]          # single value
df.iloc[1:4, [0,2,3]]  # rows + columns by position
```
> ⚠️ `iloc` upper limit is **exclusive** — same as NumPy.

---

### 4. ⚡ Fast Scalar Access — at[ ] & iat[ ]
Faster than `loc` and `iloc` when accessing a single value.

```python
df.at[102, "Department"]   # label-based → faster than .loc
df.iat[1, 0]               # position-based → faster than .iloc
```

---

### 5. 🔎 Boolean Filtering
```python
df[df["Salary"] > 70000]

# AND
df[(df["Salary"] > 70000) & (df["Department"] == "IT")]

# OR
df[(df["Salary"] > 70000) | (df["Department"] == "IT")]

# NOT
df[~(df["Department"] == "IT")]
```
> Always wrap each condition in its own `( )`.

---

### 6. 🗣️ Query Method — SQL-Style Filtering
```python
df.query("Salary > 65000")
df.query("Salary > 70000 and Department == 'IT'")
```

---

### 7. 📶 Sorting
```python
df.sort_values("Salary")                    # ascending (default)
df.sort_values("Salary", ascending=False)  # descending
df.sort_values(["Salary", "Age"])          # multiple columns
```

---

### 8. ✅ Membership Testing & Unique Values
```python
df[df["Department"].isin(["HR", "IT"])]   # filter by list
df["Department"].unique()                  # distinct values
df["Department"].nunique()                 # count of distinct values
```

---

## ⚠️ The #1 Rule to Remember

| Method | Upper Limit | Based On |
|---|---|---|
| `loc` | **Inclusive** | Labels |
| `iloc` | **Exclusive** | Positions |
| `at` | Single value | Labels |
| `iat` | Single value | Positions |

This trips up every NumPy user switching to Pandas. Remember it.

---

## 🏋️ Practice Problems

8 challenges solved in the notebook:
1. Retrieve single and multiple columns from an employee DataFrame
2. Retrieve Name and Salary together
3. Access rows using `iloc[0]` and `iloc[2]`
4. Retrieve first 3 rows using `iloc`
5. Retrieve rows 1–4 and columns Name & Salary using `loc`
6. Filter employees with Salary > 60,000
7. Multi-condition filter: Salary > 60k AND Age > 22
8. Generate 100 synthetic customers with NumPy → filter above average salary, age < 25, top 2 highest salaries

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Indexing_and_Slicing.ipynb
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
| **02** | **Indexing & Slicing ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
