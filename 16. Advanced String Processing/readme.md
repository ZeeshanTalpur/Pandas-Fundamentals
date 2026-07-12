# 🧵 Pandas Series — EP 16: Advanced String Processing

Part of my **Pandas Learning Series** — the final episode. If Window Functions are the king of numerical analytics, String Processing is the king of data cleaning. Most real-world datasets aren't messy because of numbers — they're messy because of **text**. Before you build a model, you'll spend a lot of time here. 🧹

---

## 📒 About This Notebook

Names with extra spaces. Emails in mixed case. Department columns with inconsistent formatting. Employee codes you need to split apart.

Every `.str` method you need to clean all of that is in this notebook.

> **Key Rule:** All string operations in Pandas go through the `.str` accessor.

---

## 🗂️ Dataset Used

```python
df = pd.DataFrame({
    "Name":       [" ali ", "SARA", "ahMed", " John Doe "],
    "Email":      ["ali@gmail.com", "SARA@Yahoo.com", "ahmed123@gmail.com", "john@company.org"],
    "Department": ["IT Department", "HR Department", "Finance Department", "IT Department"],
    "Code":       ["EMP-001", "EMP-002", "EMP-003", "EMP-004"]
})
```

Issues baked in: leading/trailing spaces in names, mixed case in emails, department suffix clutter, regex extraction from codes.

---

## 🧠 What's Covered — 15 .str Methods

---

### 1. lower() — Everything Lowercase
```python
df["Name"].str.lower()
# " ali " → " ali "   "SARA" → "sara"   "ahMed" → "ahmed"
```

---

### 2. upper() — Everything Uppercase
```python
df["Name"].str.upper()
# " ali " → " ALI "   "SARA" → "SARA"
```

---

### 3. title() — Title Case (Industry Favourite)
```python
df["Name"].str.title()
# " ali " → " Ali "   "SARA" → "Sara"   "ahMed" → "Ahmed"
```
> Best for name columns before saving or displaying data.

---

### 4. strip() / lstrip() / rstrip() — Remove Spaces
```python
df["Name"].str.strip()   # removes both sides
df["Name"].str.lstrip()  # removes leading spaces only
df["Name"].str.rstrip()  # removes trailing spaces only
```
> `" ali "` → `"ali"`. Run this on every text column when loading data.

---

### 5. replace() — Text & Regex Substitution

**Text replacement:**
```python
df["Department"].str.replace("Department", "")
# "IT Department" → "IT "
```

**Regex replacement:**
```python
df["Department"].str.replace(r"\d", "", regex=True)
# removes every digit from the column
```

---

### 6. contains() — Find Text (Returns Boolean Mask)

```python
df["Email"].str.contains("gmail")            # case-sensitive
df["Email"].str.contains("gmail", case=False) # case-insensitive
df["Email"].str.contains(r"\d")              # contains digits? (regex)
```
> Use to filter rows: `df[df["Email"].str.contains("gmail")]`

---

### 7. startswith() / endswith()
```python
df["Code"].str.startswith("EMP")    # True for all EMP-XXX codes
df["Email"].str.endswith(".com")    # True for .com emails
```

---

### 8. split() — Break a String Apart

```python
df["Name"].str.split()               # returns list per cell
df["Name"].str.split(expand=True)    # expands into separate columns
```
> `"John Doe"` → `["John", "Doe"]` → two columns with `expand=True`.

---

### 9. cat() — Concatenate Strings Across Columns
```python
df["Name"].str.cat(df["Department"], sep="-")
# "Ali-IT Department"   "Sara-HR Department"
```

---

### 10. len() — String Length
```python
df["Email"].str.len()
# 13   14   18   16
```

---

### 11. slice() — Extract Characters by Position
```python
df["Code"].str.slice(2)     # from index 2 onwards
df["Code"].str[4:]          # equivalent syntax
# "EMP-001" → "P-001"
```

---

### 12. extract() — Regex Extraction (First Match)

```python
# Extract digits
df["Code"].str.extract(r"(\d+)")
# "EMP-001" → "001"

# Extract letters
df["Code"].str.extract(r"([A-Z]+)")
# "EMP-001" → "EMP"

# Extract email username (everything before @)
df["Email"].str.extract(r"(^.*)@")
# "ali@gmail.com" → "ali"
```
> Returns only the **first** match per cell.

---

### 13. extractall() — Extract ALL Matches
```python
s = pd.Series(["A12B45C89"])
s.str.extractall(r"(\d+)")
# Finds: "12", "45", "89" — all matches, not just the first
```
> Unlike `extract()`, returns every match across the whole string.

---

### 14. findall() — Find All Matches as List
```python
s.str.findall(r"(\d+)")
# ["12", "45", "89"]
```
> Similar to `extractall()` but returns a list per cell, not expanded rows.

---

### 15. match() / fullmatch()

**match()** — checks if the **beginning** of the string matches:
```python
df["Code"].str.match(r"EMP")
# True if the string starts with "EMP"
```

**fullmatch()** — the **entire** string must match:
```python
df["Code"].str.fullmatch(r"EMP-\d{3}")
# True only if the whole value is "EMP-" + exactly 3 digits
```

---

## 📋 .str Methods Cheatsheet

| Method | What it does |
|---|---|
| `str.lower()` | Lowercase |
| `str.upper()` | Uppercase |
| `str.title()` | Title Case |
| `str.strip()` | Remove leading/trailing spaces |
| `str.lstrip()` | Remove leading spaces |
| `str.rstrip()` | Remove trailing spaces |
| `str.replace(old, new)` | Replace text or regex |
| `str.contains("x")` | Boolean mask — contains text? |
| `str.startswith("x")` | Starts with? |
| `str.endswith("x")` | Ends with? |
| `str.split(expand=True)` | Split into columns |
| `str.cat(other, sep)` | Concatenate two columns |
| `str.len()` | Character count |
| `str.slice(n)` | Slice by position |
| `str.extract(r"(...)")` | First regex match |
| `str.extractall(r"(...)")` | All regex matches (expanded rows) |
| `str.findall(r"(...)")` | All matches as list |
| `str.match(r"...")` | Does beginning match? |
| `str.fullmatch(r"...")` | Does entire string match? |

---

## 🚀 How to Run

```bash
git clone https://github.com/ZeeshanTalpur/<repo-name>.git
cd <repo-name>
jupyter notebook Advanced_String_Processing.ipynb
```

**Requirements:** Python 3.x · Pandas · Jupyter Notebook

```bash
pip install pandas jupyter
```

---

## 📚 Complete Pandas Series

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
| 12 | Performance Optimization |
| 13 | Advanced I/O |
| 14 | Method Chaining & Functional Pandas |
| 15 | Window Functions & Analytical Operations |
| **16** | **Advanced String Processing ← You are here** |

---

## 🙋 About Me

I'm **Zeeshan**, a Data Science & AI enthusiast learning in public. 🌱
Follow my journey → [LinkedIn](https://www.linkedin.com/in/zeeshan-talpur-4277b4252) · [GitHub](https://github.com/ZeeshanTalpur)

More learning, more building, more data coming up! ✨
