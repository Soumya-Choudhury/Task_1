# Mall Customers Data Analysis

This project analyzes the **Mall_Customers.csv** dataset to explore customer demographics, income levels, and spending patterns.

---

## 📂 Dataset
- **File:** `Mall_Customers.csv`
- **Columns:** `CustomerID`, `Gender`, `Age`, `Annual Income (k$)`, `Spending Score (1-100)`

---

## 📊 Steps Performed

### 1. **Imports and Setup**
Libraries used:
- `pandas` → Data handling
- `numpy` → Numerical operations
- `matplotlib.pyplot` → Data visualization  

Also, suppressed warnings for cleaner output to keep logs clean:
```python
import warnings
warnings.filterwarnings("ignore")
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

---

### 2. **Data Loading**
```python
df = pd.read_csv("Mall_Customers.csv")
```
Loaded the dataset into a Pandas DataFrame (`df`).

---

### 3. **Initial Inspection**
Performed basic EDA to understand structure and quality:
```python
df.head()
df.tail()
df.shape
df.columns
df.describe()
df.isna().sum()
df.duplicated().any()
```
- Viewed first/last rows
- Checked dimensions and column names
- Summary statistics (mean, quartiles, etc.)
- Checked for missing values and duplicates

---

### 4. **Mean Annual Income by Gender**
Grouped data by `Gender` and computed the average annual income.  
Visualized comparison using a bar chart:
```python
income_by_gender = df.groupby("Gender")["Annual Income (k$)"].mean()
income_by_gender.plot(kind="bar")
plt.title("Mean Annual Income by Gender")
plt.ylabel("Annual Income (k$)")
plt.xlabel("Gender")
plt.show()
```

---

### 5. **Mean Spending Score by Gender**
Grouped by `Gender` to get average spending score.  
Displayed with a bar chart:
```python
spending_by_gender = df.groupby("Gender")["Spending Score (1-100)"].mean()
spending_by_gender.plot(kind="bar")
plt.title("Mean Spending Score by Gender")
plt.ylabel("Spending Score (1-100)")
plt.xlabel("Gender")
plt.show()
```

---

### 6. **Top & Bottom Annual Incomes**
Extracted extremes in annual income:
```python
top5_income = df.sort_values("Annual Income (k$)", ascending=False).head(5)
bottom5_income = df.sort_values("Annual Income (k$)", ascending=True).head(5)
```
Displayed columns:
```
CustomerID | Age | Annual Income (k$) | Spending Score (1-100)
```

---

### 7. **Top & Bottom Spending Scores by Gender**
For each gender, identified:
- Top 5 highest spending scores
- Top 5 lowest spending scores  
Example:
```python
for gender in df["Gender"].unique():
    subset = df[df["Gender"] == gender]
    top5 = subset.sort_values("Spending Score (1-100)", ascending=False).head(5)
    bottom5 = subset.sort_values("Spending Score (1-100)", ascending=True).head(5)
    # display or store top5 / bottom5
```
Displayed:
```
CustomerID | Age | Annual Income (k$) | Spending Score (1-100)
```

---

### 8. **Age Category Analysis**
Bucketed customers into age groups:
- 18–29
- 30–39
- 40–49
- 50–59
- 60–70

Created a new column for age category and computed:
```python
bins = [17, 29, 39, 49, 59, 70]
labels = ["18-29", "30-39", "40-49", "50-59", "60-70"]
df["AgeGroup"] = pd.cut(df["Age"], bins=bins, labels=labels)

age_group_stats = (
    df.groupby("AgeGroup")["Spending Score (1-100)"]
      .agg(mean_score="mean", n="count")
      .reset_index()
      .sort_values("mean_score", ascending=False)
)
```
**Findings:**
- **Highest avg spending score:** `30–39` → `61.10` (n=61)
- **Lowest avg spending score:** `50–59` → `34.72` (n=25)  
*(n = number of customers in that age category)*

---

## 💡 Key Insights
- **Gender differences** exist in both income and spending behavior.
- **Customers aged 30–39** have the highest average spending score, indicating strong engagement or discretionary spending in that segment.
- **Customers aged 50–59** exhibit the lowest average spending score, which may affect targeting strategy.
- **Sample size (n)** per age bin helps assess reliability—larger groups give more stable averages.

---

## 🛠️ How to Reproduce
1. Clone or download this repository.
2. Ensure dependencies are installed:
   ```bash
   pip install pandas numpy matplotlib
   ```
3. Place `Mall_Customers.csv` in the project directory.
4. Run the analysis script or notebook to generate the tables and plots.

---

## 📷 Visualizations
Include the generated charts here (add image files to the repo and reference them):
- `mean_income_by_gender.png`
- `mean_spending_by_gender.png`
- `top_bottom_income.png`
- `spending_score_extremes_by_gender.png`
- `age_group_spending_scores.png`

Example Markdown to embed:
```markdown
![Mean Income by Gender](images/mean_income_by_gender.png)
```

---


## 📌 Requirements
```bash
pip install pandas numpy matplotlib
```

---
