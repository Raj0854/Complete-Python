
# Day 50 – Data Visualization with Matplotlib and Seaborn

## 1. Introduction to Data Visualization

Data visualization means representing data using charts, graphs, and plots.

It helps us:
- Understand large datasets.
- Identify patterns and trends.
- Compare different values.
- Detect unusual values.
- Communicate findings clearly.

### Example

Suppose a company has monthly sales data:

| Month | Sales |
|---|---:|
| January | 12000 |
| February | 15000 |
| March | 18000 |
| April | 14000 |
| May | 22000 |

A table shows the exact values, but a line chart makes the sales trend easier to understand.

### Common Types of Charts

| Chart | Purpose |
|---|---|
| Line Chart | Shows trends over time |
| Bar Chart | Compares categories |
| Histogram | Shows data distribution |
| Scatter Plot | Shows relationships between variables |
| Pie Chart | Shows proportions |
| Box Plot | Shows distribution and outliers |
| Heatmap | Shows values using colors |

---

## 2. Installing Visualization Libraries

We will use two important Python libraries:

1. Matplotlib
2. Seaborn

### Matplotlib

Matplotlib is a Python library used to create charts and graphs.

### Seaborn

Seaborn is a statistical data visualization library built on top of Matplotlib.

It provides attractive charts with simpler syntax for many statistical visualizations.

### Installation

Run these commands in the terminal:

```bash
pip install matplotlib seaborn pandas numpy
```

### Import Libraries

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np
```

`matplotlib.pyplot` provides functions for creating charts.

`sns` is the commonly used alias for Seaborn.

---

## 3. Understanding Figure and Axes

Matplotlib uses two important concepts:

### Figure

A Figure is the complete drawing area or canvas.

### Axes

An Axes is the actual plotting area where a chart is drawn.

A figure can contain one or multiple Axes.

### Example

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()

ax.plot([1, 2, 3, 4], [10, 20, 15, 30])

ax.set_title("Simple Line Chart")
ax.set_xlabel("X Values")
ax.set_ylabel("Y Values")

plt.show()
```

### Explanation

- `plt.subplots()` creates a Figure and an Axes.
- `ax.plot()` creates a line chart.
- `set_title()` adds a chart title.
- `set_xlabel()` adds the X-axis label.
- `set_ylabel()` adds the Y-axis label.
- `plt.show()` displays the chart.

---

## 4. Creating a Line Chart

A line chart connects data points using lines.

It is useful for showing trends over time.

### Example

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr", "May"]
sales = [12000, 15000, 18000, 14000, 22000]

plt.plot(months, sales)

plt.title("Monthly Sales")
plt.xlabel("Months")
plt.ylabel("Sales")

plt.show()
```

### Adding Markers and Line Styles

```python
plt.plot(
    months,
    sales,
    color="blue",
    marker="o",
    linestyle="--",
    linewidth=2,
    markersize=8
)

plt.title("Monthly Sales")
plt.xlabel("Months")
plt.ylabel("Sales")

plt.grid(True)
plt.show()
```

### Important Parameters

| Parameter | Meaning |
|---|---|
| color | Sets line color |
| marker | Sets data point marker |
| linestyle | Sets line style |
| linewidth | Controls line thickness |
| markersize | Controls marker size |

Common line styles:

- `-` Solid line
- `--` Dashed line
- `:` Dotted line
- `-.` Dash-dot line

### Multiple Lines in One Chart

```python
months = ["Jan", "Feb", "Mar", "Apr"]

product_a = [100, 150, 130, 180]
product_b = [120, 140, 160, 200]

plt.plot(months, product_a, label="Product A")
plt.plot(months, product_b, label="Product B")

plt.title("Product Sales Comparison")
plt.xlabel("Months")
plt.ylabel("Sales")

plt.legend()
plt.grid(True)

plt.show()
```

`plt.legend()` displays labels for the plotted lines.

---

## 5. Creating a Bar Chart

A bar chart compares values across different categories.

### Example

```python
import matplotlib.pyplot as plt

products = ["Laptop", "Mobile", "Tablet", "Monitor"]
sales = [50, 100, 40, 70]

plt.bar(products, sales)

plt.title("Product Sales")
plt.xlabel("Products")
plt.ylabel("Units Sold")

plt.show()
```

### Horizontal Bar Chart

Use `barh()` to create horizontal bars.

```python
plt.barh(products, sales)

plt.title("Product Sales")
plt.xlabel("Units Sold")
plt.ylabel("Products")

plt.show()
```

### Grouped Bar Chart

Grouped bars help compare two or more datasets.

```python
import numpy as np
import matplotlib.pyplot as plt

products = ["Laptop", "Mobile", "Tablet"]

sales_2025 = [50, 100, 40]
sales_2026 = [70, 120, 60]

x = np.arange(len(products))
width = 0.35

plt.bar(x - width / 2, sales_2025, width, label="2025")
plt.bar(x + width / 2, sales_2026, width, label="2026")

plt.xticks(x, products)

plt.title("Yearly Product Sales")
plt.xlabel("Products")
plt.ylabel("Units Sold")

plt.legend()
plt.show()
```

---

## 6. Creating a Histogram

A histogram displays the distribution of numerical data.

It groups numerical values into intervals called bins.

### Example

```python
import matplotlib.pyplot as plt

marks = [45, 50, 55, 60, 65, 70, 72, 75, 80, 85, 90, 95]

plt.hist(marks, bins=5, edgecolor="black")

plt.title("Student Marks Distribution")
plt.xlabel("Marks")
plt.ylabel("Number of Students")

plt.show()
```

### Important Parameters

- `bins`: Number of intervals.
- `edgecolor`: Color of bar borders.
- `alpha`: Transparency of bars.

### Understanding Bins

If marks range from 0 to 100 and we use 5 bins, the histogram divides the range into five intervals.

Each bar represents how many observations fall into that interval.

---

## 7. Creating a Scatter Plot

A scatter plot displays the relationship between two numerical variables.

Each point represents one observation.

### Example

```python
import matplotlib.pyplot as plt

hours = [1, 2, 3, 4, 5, 6, 7]
marks = [35, 40, 50, 55, 65, 75, 85]

plt.scatter(hours, marks)

plt.title("Study Hours vs Marks")
plt.xlabel("Study Hours")
plt.ylabel("Marks")

plt.show()
```

### Interpretation

If points generally move upward from left to right, the variables may have a positive relationship.

If they move downward, they may have a negative relationship.

A scatter plot can also reveal clusters and unusual observations.

Remember: A relationship between two variables does not automatically prove that one causes the other.

---

## 8. Creating a Pie Chart

A pie chart represents how a total is divided among categories.

### Example

```python
import matplotlib.pyplot as plt

categories = ["Food", "Travel", "Shopping", "Bills"]
expenses = [3000, 2000, 1500, 3500]

plt.pie(
    expenses,
    labels=categories,
    autopct="%1.1f%%",
    startangle=90
)

plt.title("Monthly Expenses")

plt.show()
```

### Important Parameters

- `labels`: Category names.
- `autopct`: Displays percentages.
- `startangle`: Rotates the chart.

Use pie charts only when the number of categories is small and the proportions are easy to compare. For many categories, a bar chart is usually clearer.

---

## 9. Creating a Box Plot

A box plot summarizes the distribution of numerical data.

It helps identify:
- Median.
- Lower and upper quartiles.
- Spread of data.
- Potential outliers.

### Example

```python
import matplotlib.pyplot as plt

marks = [45, 50, 55, 60, 65, 70, 72, 75, 80, 85, 95, 150]

plt.boxplot(marks)

plt.title("Student Marks Distribution")
plt.ylabel("Marks")

plt.show()
```

### Understanding a Box Plot

- The line inside the box represents the median.
- The box represents the interquartile range (IQR).
- Whiskers show the range within the box plot's whisker rule.
- Points beyond the whiskers are potential outliers.

An outlier is not automatically an error. It should be investigated before removal.

---

## 10. Customizing Matplotlib Charts

A chart should be readable and properly labeled.

### Example

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr"]
sales = [10000, 15000, 12000, 20000]

plt.figure(figsize=(8, 5))

plt.plot(
    months,
    sales,
    color="green",
    marker="o",
    linewidth=2,
    label="Monthly Sales"
)

plt.title("Company Sales Report", fontsize=16)
plt.xlabel("Month", fontsize=12)
plt.ylabel("Revenue", fontsize=12)

plt.legend()
plt.grid(True, linestyle="--", alpha=0.5)

plt.tight_layout()
plt.show()
```

### Useful Customization Functions

| Function | Purpose |
|---|---|
| `plt.figure(figsize=(8, 5))` | Sets figure dimensions |
| `plt.title()` | Adds title |
| `plt.xlabel()` | Labels X-axis |
| `plt.ylabel()` | Labels Y-axis |
| `plt.xticks()` | Controls X-axis ticks |
| `plt.yticks()` | Controls Y-axis ticks |
| `plt.legend()` | Displays legend |
| `plt.grid()` | Displays grid |
| `plt.tight_layout()` | Adjusts spacing |

### Saving a Chart

```python
plt.figure(figsize=(8, 5))

plt.plot([1, 2, 3, 4], [10, 20, 15, 30])

plt.title("Sales Chart")

plt.savefig("sales_chart.png", dpi=300, bbox_inches="tight")

plt.show()
```

`savefig()` saves the chart as an image.

- `dpi=300` provides high-resolution output.
- `bbox_inches="tight"` helps avoid unnecessary blank space.

Call `savefig()` before `show()` for reliable saving across plotting environments.

---

## 11. Introduction to Seaborn

Seaborn is built on Matplotlib and provides a high-level interface for statistical visualization.

It works especially well with Pandas DataFrames.

### Setting a Theme

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.set_theme(style="whitegrid")

data = [10, 20, 15, 30, 25]

sns.lineplot(x=range(len(data)), y=data)

plt.title("Sales Trend")

plt.show()
```

### Common Seaborn Styles

- `darkgrid`
- `whitegrid`
- `dark`
- `white`
- `ticks`

Example:

```python
sns.set_theme(style="darkgrid", palette="deep")
```

---

## 12. Seaborn Scatter Plot

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

df = pd.DataFrame({
    "hours": [1, 2, 3, 4, 5, 6],
    "marks": [35, 40, 50, 60, 70, 85],
    "class": ["A", "A", "B", "B", "A", "B"]
})

sns.scatterplot(
    data=df,
    x="hours",
    y="marks",
    hue="class"
)

plt.title("Study Hours vs Marks")
plt.show()
```

The `hue` parameter assigns different colors to categories.

---

## 13. Seaborn Line Plot

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

df = pd.DataFrame({
    "month": ["Jan", "Feb", "Mar", "Apr"],
    "sales": [10000, 15000, 12000, 20000]
})

sns.lineplot(data=df, x="month", y="sales", marker="o")

plt.title("Monthly Sales")
plt.show()
```

---

## 14. Seaborn Bar Plot

A Seaborn bar plot displays an estimated statistic for each category. By default, it shows the mean.

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

df = pd.DataFrame({
    "department": ["IT", "IT", "HR", "HR", "Sales", "Sales"],
    "salary": [50000, 55000, 40000, 45000, 60000, 65000]
})

sns.barplot(data=df, x="department", y="salary")

plt.title("Average Department Salary")
plt.show()
```

### Count Plot

A count plot displays the number of observations in each category.

```python
sns.countplot(data=df, x="department")

plt.title("Employees by Department")
plt.show()
```

Difference:

- `barplot()` displays an estimated numerical statistic.
- `countplot()` displays category counts.

---

## 15. Seaborn Histogram

```python
import seaborn as sns
import matplotlib.pyplot as plt

marks = [45, 50, 55, 60, 65, 70, 72, 75, 80, 85, 90]

sns.histplot(marks, bins=5, kde=True)

plt.title("Marks Distribution")
plt.xlabel("Marks")

plt.show()
```

`kde=True` adds a smooth density curve to the histogram.

---

## 16. Seaborn Box Plot

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

df = pd.DataFrame({
    "department": ["IT", "IT", "IT", "HR", "HR", "HR"],
    "salary": [50000, 55000, 60000, 35000, 40000, 45000]
})

sns.boxplot(data=df, x="department", y="salary")

plt.title("Salary Distribution by Department")
plt.show()
```

This chart helps compare salary distributions across departments.

---

## 17. Seaborn Violin Plot

A violin plot displays the distribution and density of numerical data across categories.

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

df = pd.DataFrame({
    "class": ["A", "A", "A", "B", "B", "B"],
    "marks": [40, 50, 60, 65, 75, 85]
})

sns.violinplot(data=df, x="class", y="marks")

plt.title("Marks Distribution by Class")
plt.show()
```

A violin plot combines information about distribution shape with a summary of the data.

---

## 18. Correlation Heatmap

A heatmap displays values using colors.

It is commonly used to visualize correlation between numerical variables.

### What Is Correlation?

Correlation measures the strength and direction of a relationship between two numerical variables.

Correlation values range from -1 to +1.

| Value | Meaning |
|---|---|
| +1 | Perfect positive correlation |
| 0 | No linear correlation |
| -1 | Perfect negative correlation |

### Example

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.DataFrame({
    "hours": [1, 2, 3, 4, 5],
    "marks": [30, 40, 50, 60, 70],
    "sleep": [8, 7, 7, 6, 6]
})

correlation = df.corr(numeric_only=True)

sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm",
    vmin=-1,
    vmax=1
)

plt.title("Correlation Heatmap")
plt.show()
```

### Important Parameters

- `annot=True`: Displays numerical values.
- `cmap`: Selects the color palette.
- `vmin` and `vmax`: Set the color scale limits.

Important: Correlation does not prove causation. A high correlation alone does not establish that one variable causes another.

---

## 19. Pair Plot

A pair plot compares relationships between multiple numerical variables.

```python
import seaborn as sns
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame({
    "hours": [1, 2, 3, 4, 5],
    "marks": [30, 40, 50, 60, 70],
    "sleep": [8, 7, 7, 6, 6]
})

sns.pairplot(df)

plt.show()
```

Pair plots are useful for quickly exploring relationships between multiple variables.

They can become difficult to read when a dataset contains many columns.

---

## 20. Creating Multiple Charts with Subplots

Subplots allow us to display multiple charts in one figure.

### Example

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr"]
sales = [100, 150, 120, 200]
profit = [20, 35, 25, 50]

fig, axes = plt.subplots(1, 2, figsize=(12, 5))

axes[0].plot(months, sales, marker="o")
axes[0].set_title("Monthly Sales")
axes[0].set_xlabel("Month")
axes[0].set_ylabel("Sales")

axes[1].bar(months, profit)
axes[1].set_title("Monthly Profit")
axes[1].set_xlabel("Month")
axes[1].set_ylabel("Profit")

plt.tight_layout()
plt.show()
```

### Explanation

- `plt.subplots(1, 2)` creates one row and two columns.
- `axes[0]` accesses the first chart.
- `axes[1]` accesses the second chart.
- `figsize` controls the overall figure size.

---

# 21. Mini Project – Sales Performance Visualization Dashboard

## Project Description

Create a visualization report for a company using sales data.

The report should display:

1. Monthly revenue trend.
2. Revenue by product category.
3. Revenue distribution.
4. Revenue comparison by region.
5. Correlation between numerical sales variables.

### Step 1: Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_theme(style="whitegrid")
```

### Step 2: Create Sample Dataset

```python
df = pd.DataFrame({
    "month": [
        "Jan", "Feb", "Mar", "Apr", "May",
        "Jun", "Jul", "Aug", "Sep", "Oct",
        "Nov", "Dec"
    ],

    "revenue": [
        12000, 15000, 18000, 14000,
        22000, 25000, 21000, 28000,
        30000, 27000, 32000, 35000
    ],

    "category": [
        "Laptop", "Mobile", "Tablet", "Laptop",
        "Mobile", "Tablet", "Laptop", "Mobile",
        "Tablet", "Laptop", "Mobile", "Tablet"
    ],

    "region": [
        "North", "South", "East", "West",
        "North", "South", "East", "West",
        "North", "South", "East", "West"
    ],

    "units_sold": [
        10, 15, 20, 12, 22, 25,
        21, 28, 30, 27, 32, 35
    ]
})

print(df)
```

### Step 3: Analyze the Dataset

```python
print("Total Revenue:", df["revenue"].sum())

print("Average Revenue:", df["revenue"].mean())

print("Highest Revenue:", df["revenue"].max())

print("Lowest Revenue:", df["revenue"].min())
```

Expected output:

```text
Total Revenue: 269000
Average Revenue: 22416.666666666668
Highest Revenue: 35000
Lowest Revenue: 12000
```

### Step 4: Monthly Revenue Line Chart

```python
plt.figure(figsize=(10, 5))

sns.lineplot(
    data=df,
    x="month",
    y="revenue",
    marker="o"
)

plt.title("Monthly Revenue Trend")
plt.xlabel("Month")
plt.ylabel("Revenue")

plt.tight_layout()
plt.show()
```

### Step 5: Product Category Revenue

```python
category_revenue = df.groupby("category")["revenue"].sum()

plt.figure(figsize=(8, 5))

category_revenue.plot(kind="bar")

plt.title("Revenue by Product Category")
plt.xlabel("Category")
plt.ylabel("Revenue")

plt.xticks(rotation=0)
plt.tight_layout()
plt.show()
```

### Step 6: Revenue Distribution

```python
plt.figure(figsize=(8, 5))

sns.histplot(
    data=df,
    x="revenue",
    bins=6,
    kde=True
)

plt.title("Revenue Distribution")
plt.xlabel("Revenue")

plt.show()
```

### Step 7: Region Revenue Comparison

```python
region_revenue = df.groupby("region")["revenue"].sum()

plt.figure(figsize=(8, 5))

sns.barplot(
    x=region_revenue.index,
    y=region_revenue.values
)

plt.title("Revenue by Region")
plt.xlabel("Region")
plt.ylabel("Revenue")

plt.show()
```

### Step 8: Correlation Heatmap

```python
plt.figure(figsize=(7, 5))

correlation = df[
    ["revenue", "units_sold"]
].corr()

sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm",
    vmin=-1,
    vmax=1
)

plt.title("Sales Correlation Heatmap")

plt.show()
```

### Step 9: Save the Dataset and Charts

```python
df.to_csv("sales_report.csv", index=False)

plt.figure(figsize=(10, 5))

sns.lineplot(data=df, x="month", y="revenue", marker="o")

plt.title("Monthly Revenue")

plt.savefig(
    "monthly_revenue.png",
    dpi=300,
    bbox_inches="tight"
)

plt.show()
```

### Expected Project Output

The student should produce:

- A sales dataset saved as CSV.
- A monthly revenue line chart.
- A product category bar chart.
- A revenue distribution histogram.
- A region comparison chart.
- A correlation heatmap.

The student should also write 3–5 observations based on the charts.

Example observations:

1. December has the highest monthly revenue.
2. January has the lowest monthly revenue.
3. Revenue generally increases toward the end of the year.
4. The correlation heatmap shows the relationship between revenue and units sold.

---

# 22. Student Practical Exercises

## Exercise 1 – Line Chart

Create a line chart showing weekly temperatures.

Use at least seven days of sample data.

## Exercise 2 – Bar Chart

Create a bar chart comparing marks of five students.

## Exercise 3 – Histogram

Generate 100 random student marks and display their distribution using a histogram.

## Exercise 4 – Scatter Plot

Create a scatter plot showing the relationship between study hours and exam marks.

## Exercise 5 – Pie Chart

Create a pie chart showing monthly expenses across five categories.

## Exercise 6 – Box Plot

Create a box plot comparing salaries of two departments.

## Exercise 7 – Seaborn Heatmap

Create a DataFrame containing at least four numerical columns and generate its correlation heatmap.

## Exercise 8 – Multiple Subplots

Create a figure containing:
- One line chart.
- One bar chart.
- One histogram.
- One scatter plot.

## Exercise 9 – Sales Report

Use a dataset with at least 20 records and create:
- Monthly sales chart.
- Category comparison chart.
- Sales distribution histogram.
- Region comparison chart.

Save at least two charts as PNG files.

---

# 23. Trainer Assessment

Ask the student these questions:

1. What is data visualization?
2. What is Matplotlib?
3. What is Seaborn?
4. What is the difference between a Figure and an Axes?
5. When should we use a line chart?
6. What is the difference between a bar chart and histogram?
7. What does a scatter plot represent?
8. What is a box plot used for?
9. What is the purpose of `plt.legend()`?
10. What does `plt.tight_layout()` do?
11. What is the purpose of `savefig()`?
12. What does the `hue` parameter do in Seaborn?
13. What is a correlation heatmap?
14. What is the difference between `barplot()` and `countplot()`?
15. Why does correlation not prove causation?

## Practical Assessment

Ask the student to:

1. Load a CSV file using Pandas.
2. Create a line chart using two numerical columns.
3. Create a category-wise bar chart.
4. Create a histogram.
5. Create a scatter plot.
6. Generate a correlation heatmap.
7. Save two charts as PNG images.
8. Explain three findings from the visualizations.

---

# 24. Completion Criteria

The student should be able to:

- Explain the purpose of data visualization.
- Select an appropriate chart for a given problem.
- Create charts using Matplotlib.
- Customize titles, labels, legends, and grids.
- Create statistical visualizations using Seaborn.
- Visualize Pandas DataFrames.
- Create subplots.
- Interpret histograms, scatter plots, and box plots.
- Generate correlation heatmaps.
- Save visualizations as image files.
- Explain findings from a dataset using charts.

---

# 25. Next Day Preview

**Day 51 – Exploratory Data Analysis (EDA)**

Topics:
- Understanding a dataset.
- Data inspection and profiling.
- Univariate analysis.
- Bivariate analysis.
- Multivariate analysis.
- Finding patterns and outliers.
- Asking meaningful questions from data.
- EDA mini-project.
