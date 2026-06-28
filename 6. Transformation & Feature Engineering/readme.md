# 🛠️ Pandas Series — EP 06: Transformations & Feature Engineering

Part of my **Pandas Learning Series** — the episode where data stops being passive and starts being shaped. Feature engineering is one of the highest-value skills in Data Science. This notebook covers every major tool for creating, transforming, and categorizing data in Pandas. ✨

---

## 📒 About This Notebook

Raw data rarely has everything you need. A salary number is less useful than a tier label. An age is less useful than an age group. This episode is about creating those features — transforming what you have into what your model or analysis actually needs.

---

## 💡 What Is Feature Engineering?

```
Name    Age   Salary
Ali     22    50000    →    Bronze
Sara    35    120000   →    Gold
```

These categories don't exist in the raw data. We create them. That's feature engineering.

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

## 🧠 What's Covered

### 1. 🆕 Creating New Columns (Vectorized)
```python
df["Bonus"] = df["Salary"] * 0.1
```
> Vectorized computation — no loops involved. This is the preferred way.

---

### 2. 🗺️ map() — Pure Mapping
```python
df["Department"] = df["Department"].map({"HR": "Human Resource"})
```
> ⚠️ **Gotcha:** Unmatched keys become **NaN**. IT, Finance → NaN if not in the dict.

**When to use:** Fast, clean mapping when all values have a match.

---

### 3. 🔄 replace() — Flexible Substitution
```python
df["Department"] = df["Department"].replace({"HR": "Human Resources"})
df["Department"] = df["Department"].replace({"IT": "Information Technology"})
```
> ✅ **Unmatched keys stay as-is.** IT and Finance are untouched until you map them.

**map() vs replace():**
| | map() | replace() |
|---|---|---|
| Unmatched keys | → NaN | → unchanged |
| Speed | Faster | Slightly slower |
| Flexibility | Less | More |

---

### 4. ⚙️ apply() — Custom Logic
```python
# Named function
def age_category(age):
    if age < 30:
        return "Young"
    return "Senior"

df["Category"] = df["Age"].apply(age_category)

# Lambda (compact)
df["Category"] = df["Age"].apply(lambda x: "Young" if x < 30 else "Senior")
```

> **When NOT to use apply():** If a vectorized operation exists, use it instead. `apply()` is slower. Use it only when no vectorized alternative exists.

---

### 5. 🔀 np.where() — Conditional Labeling

**Single condition:**
```python
df["HighIncome"] = np.where(df["Salary"] > 80000, "Yes", "No")
```

**Multiple conditions (nested):**
```python
df["Level"] = np.where(
    df["Salary"] > 100000, "Gold",
    np.where(
        df["Salary"] > 70000, "Silver",
        "Bronze"
    )
)
```

---

### 6. ✂️ cut() — Equal Width Binning
```python
bins   = [18, 25, 35, 50]
labels = ["Young Adult", "Adult", "Middle Age"]

df["AgeGroup"] = pd.cut(df["Age"], bins, labels=labels)
```

**Why businesses use this:**
> Instead of "Customer Age = 31" → "Customer Segment = Adult"

Much easier to analyze, visualize, and explain to stakeholders.

---

### 7. 📊 qcut() — Equal Frequency Binning
```python
df["SalaryLevel"] = pd.qcut(df["Salary"], q=3, labels=["Low", "Medium", "High"])
```

**cut() vs qcut():**
| | cut() | qcut() |
|---|---|---|
| Controls | Width of each bin | Number of entries per bin |
| Use when | You know the range | You want equal-sized groups |

**Industry uses:** Customer segmentation, risk levels, marketing tiers.

---

### 8. 🔗 assign() — Multiple Columns at Once
```python
df = df.assign(
    Bonus = df["Salary"] * 0.1,
    Tax   = df["Salary"] * 0.2
)
```
> Creates multiple columns in a single call. Powerful when combined with method chaining.

---

## ⚠️ Key Differences to Remember

| Tool | Unmatched keys | Best for |
|---|---|---|
| `map()` | → NaN | Pure value mapping, all keys known |
| `replace()` | → unchanged | Partial renaming, flexible |
| `apply()` | — | Custom logic with no vectorized equivalent |
| `np.where()` | — | Fast conditional labeling |
| `cut()` | — | Binning by range |
| `qcut()` | — | Binning by frequency |
| `assign()` | — | Multiple columns + method chaining |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Tranformations_and_Feature_Engineering.ipynb
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
| **06** | **Transformations & Feature Engineering ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
