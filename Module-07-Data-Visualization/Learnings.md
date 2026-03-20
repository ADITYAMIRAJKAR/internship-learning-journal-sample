# Module 7: Data Visualization

Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

---

## 1. Presentation Tools

Moving beyond static documents, modern presentation tools allow for code-driven, reproducible, and interactive data storytelling.

### Data Storytelling
The practice of building a compelling narrative around a set of data and its accompanying visualizations to help convey the meaning of that data in a powerful and contextualized way.

### HTML Slides: RevealJS
Reveal.js is an open-source HTML presentation framework. It allows you to create fully-featured, beautiful presentations using web technologies.
* **Basic Structure (`index.html`):**
    ```html
    <html>
      <head>
        <link rel="stylesheet" href="dist/reveal.css">
        <link rel="stylesheet" href="dist/theme/white.css">
      </head>
      <body>
        <div class="reveal">
          <div class="slides">
            <section>
              <h1>Data Storytelling</h1>
              <p>Visualizing our Q3 Growth</p>
            </section>
            <section>
              <h2>Revenue Trend</h2>
              </section>
          </div>
        </div>
        <script src="dist/reveal.js"></script>
        <script>
          Reveal.initialize();
        </script>
      </body>
    </html>
    ```

### Markdown Presentations: Marp
Marp (Markdown Presentation Ecosystem) allows you to write presentations in plain Markdown. It's excellent for keeping your slide content version-controlled in Git.
* **Basic Slide Deck (`presentation.md`):**
    ```markdown
    ---
    marp: true
    theme: default
    paginate: true
    ---

    # Executive Summary
    * Revenue increased by 15%
    * Churn decreased by 5%

    ---

    # Q3 Sales Breakdown
    ![Sales Chart](sales_chart.png)
    ```

### Interactive Notebooks: Marimo
Marimo is a reactive Python notebook built for UI and interactivity. Unlike Jupyter, when you update a cell in Marimo, dependent cells update automatically.
* **Example Marimo Cell:**
    ```python
    import marimo
    app = marimo.App()

    @app.cell
    def plot_data():
        import pandas as pd
        import matplotlib.pyplot as plt
        
        df = pd.DataFrame({"Month": ["Jan", "Feb", "Mar"], "Sales": [150, 200, 250]})
        fig, ax = plt.subplots()
        ax.bar(df["Month"], df["Sales"], color='skyblue')
        
        # Marimo can render matplotlib figures directly
        return df, fig
    ```

---

## 2. Excel Visualization

### Visualizing Forecasts with Excel
Excel's native charting tools are powerful for displaying historical data and future projections.
* **Creating a Forecast Chart:** 1. Select your historical time-series data (Dates and Values).
    2. Go to `Data` > `Forecast Sheet`.
    3. Excel automatically generates a line chart showing the historical data alongside a projected trendline and shaded confidence intervals (upper and lower bounds) using Exponential Smoothing (ETS).

---

## 3. Static Visualization

### RAWgraphs
RAWgraphs is an open-source data visualization framework built to make complex visual representations easy. 
* **Concept:** It acts as a bridge between spreadsheet applications and vector graphics editors (like Adobe Illustrator). You paste your data into the web interface, map dimensions to visual variables, and export as SVG. No coding required.

### Data Visualization with Seaborn
Seaborn is a Python data visualization library based on matplotlib. It provides a high-level interface for drawing attractive and informative statistical graphics.
* **Python Example:**
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt

    # Load sample dataset
    penguins = sns.load_dataset("penguins")

    # Create a scatterplot with a regression line and categorization
    sns.lmplot(
        data=penguins, 
        x="flipper_length_mm", 
        y="body_mass_g", 
        hue="species", 
        height=6
    )
    plt.title("Penguin Body Mass vs. Flipper Length")
    plt.show()
    ```

---

