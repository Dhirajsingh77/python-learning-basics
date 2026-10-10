# Phase 1: Essential Python Libraries — ML Lab & Placement Notes

**Goal:** Load data, manipulate it, perform basic EDA, and visualize results.

## 1. NumPy — Numerical Computing

NumPy provides efficient multidimensional arrays and mathematical operations.

### Import and create arrays

```python
import numpy as np

a = np.array([10, 20, 30, 40])
matrix = np.array([[1, 2], [3, 4]])

print(a)
print(matrix)
```

### Important attributes

```python
a.shape   # (4,)
a.ndim    # 1
a.size    # 4
a.dtype   # Data type of elements
```

- `shape`: Dimensions of the array.
- `ndim`: Number of dimensions.
- `size`: Total number of elements.
- `dtype`: Element data type.

### Array creation

```python
np.zeros((2, 3))       # Array filled with zeros
np.ones((2, 2))        # Array filled with ones
np.arange(0, 10, 2)    # [0, 2, 4, 6, 8]
np.linspace(0, 1, 5)   # 5 evenly spaced values
np.eye(3)              # 3x3 identity matrix
```

### Indexing and slicing

```python
a = np.array([10, 20, 30, 40, 50])

a[0]       # 10
a[-1]      # 50
a[1:4]     # [20, 30, 40]
a[::2]     # [10, 30, 50]
```

2D arrays:

```python
m = np.array([[1, 2, 3], [4, 5, 6]])

m[0, 1]    # 2
m[1, :]    # [4, 5, 6]
m[:, 0]    # [1, 4]
m[:, 1:3]  # [[2, 3], [5, 6]]
```

### Vectorized operations

```python
a = np.array([1, 2, 3])

a + 10     # [11, 12, 13]
a * 2      # [2, 4, 6]
a ** 2     # [1, 4, 9]

np.sum(a)   # 6
np.mean(a)  # 2.0
np.max(a)   # 3
np.min(a)   # 1
np.std(a)   # Standard deviation
```

**Interview point:** NumPy operations are often vectorized, avoiding explicit Python loops for element-wise computations.

### Broadcasting

Broadcasting allows compatible array shapes to work together.

```python
a = np.array([1, 2, 3])
print(a + 10)  # [11, 12, 13]
```

### Reshape and random numbers

```python
a = np.arange(6)
a.reshape(2, 3)

np.random.seed(42)
np.random.randint(1, 10, size=5)
```

**Common mistakes**
- NumPy indexing starts at `0`.
- The number of elements must remain the same when reshaping.
- `*` performs element-wise multiplication; `@` performs matrix multiplication.
- Basic slicing often returns a view, so modifying the slice may modify the original array.

---

## 2. Pandas — Data Analysis

Pandas is used to load, inspect, filter, transform, and analyze tabular data.

### Import and create a DataFrame

```python
import pandas as pd

data = {
    "Name": ["Aman", "Riya", "Raj"],
    "Marks": [80, 95, 70],
    "Age": [20, 21, 20]
}

df = pd.DataFrame(data)
print(df)
```

A **Series** is one-dimensional; a **DataFrame** is two-dimensional and tabular.

### Load and save CSV

```python
df = pd.read_csv("students.csv")
df.to_csv("output.csv", index=False)
```

`index=False` prevents the DataFrame index from being written as an additional CSV column.

### Inspect data

```python
df.head()       # First 5 rows
df.tail()       # Last 5 rows
df.shape        # (rows, columns)
df.columns      # Column names
df.info()       # Data types and non-null counts
df.describe()   # Summary statistics for numeric columns
df.dtypes       # Data type of each column
df.isnull().sum()  # Missing values per column
```

**Important:** `info()` prints information and normally returns `None`; `describe()` returns a summary DataFrame.

### Select columns

```python
df["Marks"]             # Series
df[["Name", "Marks"]]   # DataFrame
```

### Select rows with `loc` and `iloc`

```python
df.loc[0, "Name"]    # Label-based selection
df.iloc[0, 1]        # Position-based selection
df.iloc[:2, :]       # First two rows
```

- `loc` uses labels.
- `iloc` uses integer positions.

### Filter rows

```python
df[df["Marks"] > 80]

df[(df["Marks"] >= 70) & (df["Age"] == 20)]
```

Use `&` for AND and `|` for OR between Pandas conditions. Wrap each condition in parentheses.

### Add and modify columns

```python
df["Passed"] = df["Marks"] >= 40
df["Bonus_Marks"] = df["Marks"] + 5
```

### Handle missing values

```python
df.isnull().sum()
df.dropna()
df.fillna(0)
df["Marks"] = df["Marks"].fillna(df["Marks"].mean())
```

Choose an appropriate strategy for the data rather than automatically replacing all missing values with zero.

### Sorting and grouping

```python
df.sort_values("Marks", ascending=False)

df.groupby("Age")["Marks"].mean()
```

**Lab tip:** Start EDA with `head()`, `shape`, `info()`, `describe()`, and missing-value counts.

---

## 3. Matplotlib — Data Visualization

Matplotlib creates line plots, scatter plots, histograms, bar charts, and more.

```python
import matplotlib.pyplot as plt
```

### Line plot

Best for showing trends, often over time.

```python
x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

plt.plot(x, y, marker="o", label="Sales")
plt.xlabel("Day")
plt.ylabel("Sales")
plt.title("Daily Sales")
plt.legend()
plt.grid(True)
plt.show()
```

### Scatter plot

Best for exploring the relationship between two numerical variables.

```python
plt.scatter([1, 2, 3, 4], [10, 15, 13, 20])
plt.xlabel("Hours Studied")
plt.ylabel("Marks")
plt.title("Study Hours vs Marks")
plt.show()
```

### Histogram

Shows the distribution of a numerical variable.

```python
marks = [45, 50, 60, 60, 70, 75, 80, 90]

plt.hist(marks, bins=5, edgecolor="black")
plt.xlabel("Marks")
plt.ylabel("Frequency")
plt.title("Distribution of Marks")
plt.show()
```

### Bar chart

Compares values across categories.

```python
names = ["Aman", "Riya", "Raj"]
marks = [80, 95, 70]

plt.bar(names, marks)
plt.xlabel("Student")
plt.ylabel("Marks")
plt.title("Student Marks")
plt.show()
```

### Subplots

Display multiple plots in one figure.

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot([1, 2, 3], [2, 4, 6])
axes[0].set_title("Line Plot")

axes[1].scatter([1, 2, 3], [3, 2, 5])
axes[1].set_title("Scatter Plot")

plt.tight_layout()
plt.show()
```

- `plt.subplots(1, 2)` creates one row and two columns.
- `axes[0]` and `axes[1]` refer to the individual plotting areas.
- With axes objects, use `set_title()`, `set_xlabel()`, and `set_ylabel()`.

**Common mistake:** Use `plt.show()` to display a figure in a regular Python script.

---

## 4. Seaborn — Statistical Visualization

Seaborn builds on Matplotlib and makes statistical plots easier to create.

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

### Heatmap

Useful for visualizing a matrix, such as correlations.

```python
corr = df[["Marks", "Age"]].corr()

sns.heatmap(corr, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap")
plt.show()
```

- `annot=True` displays values inside the cells.
- `corr()` calculates correlations between numerical columns.

### Pairplot

Shows pairwise relationships between numerical features.

```python
sns.pairplot(df[["Marks", "Age"]])
plt.show()
```

For larger datasets, pairplots may be slow or visually cluttered.

---

## 5. Mini EDA Workflow

This is a reusable starting point for lab questions involving CSV data.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("students.csv")

# 1. Inspect
print(df.head())
print(df.shape)
df.info()

# 2. Summarize
print(df.describe())
print(df.isnull().sum())

# 3. Filter
high_scores = df[df["Marks"] >= 80]
print(high_scores)

# 4. Visualize distribution
df["Marks"].dropna().plot(kind="hist", bins=10)
plt.title("Marks Distribution")
plt.xlabel("Marks")
plt.show()

# 5. Correlation of numeric columns
numeric_df = df.select_dtypes(include="number")
sns.heatmap(numeric_df.corr(), annot=True)
plt.title("Feature Correlations")
plt.show()
```

The example assumes the CSV contains a `Marks` column. Adjust column names to match your actual dataset.

---

## 6. Quick Comparison

| Library | Main purpose | Remember |
|---|---|---|
| NumPy | Numerical arrays | `np.array()`, `reshape()`, `mean()` |
| Pandas | Tabular data and EDA | `read_csv()`, `loc`, `groupby()` |
| Matplotlib | General plotting | `plot()`, `scatter()`, `hist()` |
| Seaborn | Statistical visualization | `heatmap()`, `pairplot()` |

## 7. Lab and Placement Practice Checklist

### NumPy
- [ ] Create 1D and 2D arrays.
- [ ] Practise indexing, slicing, and reshaping.
- [ ] Calculate mean, standard deviation, minimum, and maximum.
- [ ] Demonstrate element-wise operations and broadcasting.

### Pandas
- [ ] Load a CSV and inspect its structure.
- [ ] Select rows and columns using `loc` and `iloc`.
- [ ] Filter records using multiple conditions.
- [ ] Handle missing values and sort data.
- [ ] Group data and calculate averages.

### Visualization
- [ ] Plot a line graph, scatter plot, histogram, and bar chart.
- [ ] Create two subplots in one figure.
- [ ] Add titles, labels, and legends.
- [ ] Create a correlation heatmap and pairplot.


