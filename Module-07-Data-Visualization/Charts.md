# Data Visualization: Charts

Charts are the atomic units of data visualization. Selecting the correct chart type is crucial for accurately communicating the underlying data and preventing misinterpretation. 

## 1. Chart Selection Guide

Choosing the right visual depends entirely on the relationship you are trying to show in your data.

### Showing Trends Over Time
* **Line Chart:** Best for continuous data to show an overall trend (e.g., revenue over 12 months).
* **Area Chart:** Similar to a line chart but filled in below the line; useful for showing the cumulative magnitude of a trend.

### Comparing Categories
* **Bar Chart (Horizontal):** Ideal for comparing discrete categories, especially when category names are long.
* **Column Chart (Vertical):** Good for comparing a few categories side-by-side.

### Showing Composition (Part-to-Whole)
* **Pie/Donut Chart:** Use only for a small number of categories (less than 5) that add up to 100%. 
* **Stacked Bar Chart:** Excellent for showing composition across multiple categories or time periods.

### Showing Distribution and Relationships
* **Scatter Plot:** Used to visualize the correlation between two numeric variables (e.g., identifying if higher marketing spend correlates with higher sales).
* **Histogram:** Visualizes the distribution of a single continuous variable by grouping data into "bins."

---

## 2. Best Practices for Chart Design

A well-designed chart minimizes cognitive load for the viewer.

* **Maximize the Data-to-Ink Ratio:** Remove unnecessary gridlines, borders, and heavy backgrounds. The "ink" should primarily represent the data itself.
* **Start the Y-Axis at Zero:** Truncating the y-axis (starting it at a number greater than zero) visually exaggerates differences and can be highly misleading, especially in bar charts.
* **Strategic Use of Color:** Use a single color for standard data and highlight specific data points (like an outlier or a specific year) with a contrasting accent color. Avoid relying entirely on red/green combinations for accessibility.
* **Clear Labeling:** Always label your axes, include units of measurement, and provide a descriptive, takeaway-focused title (e.g., "Sales Declined by 10% in Q3" instead of just "Q3 Sales").

---

## 3. Programmatic Charting Example (Python/Seaborn)

While GUI tools like Excel are great, programmatic charting allows for reproducibility. Here is an example of generating a distribution chart using Python's `seaborn` library:

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Load a sample dataset
tips = sns.load_dataset("tips")

# Create a histogram to show the distribution of total bills
sns.histplot(data=tips, x="total_bill", kde=True, color="blue")

# Apply clean styling
plt.title("Distribution of Total Bill Amounts")
plt.xlabel("Total Bill ($)")
plt.ylabel("Frequency")
sns.despine() # Removes top and right borders for a cleaner look

plt.show()
