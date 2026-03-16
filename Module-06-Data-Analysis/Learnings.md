# Module 6: Data Analysis

Data analysis involves inspecting, modeling, and interpreting data to discover useful information, draw conclusions, and support decision-making. This module covers analytical techniques across spreadsheets, programming languages, databases, and specialized tools.

---

## 1. Excel Analysis

Excel provides built-in statistical functions and the "Data Analysis Toolpak" for deep numerical analysis without writing traditional code.

### Correlation with Excel
Measures the strength and direction of a relationship between two variables.
* **Using Formulas:**
    ```excel
    =CORREL(A2:A100, B2:B100)
    ```
    *(Returns a value between -1 and 1. Closer to 1 or -1 means strong correlation; close to 0 means weak/no correlation.)*

### Regression with Excel
Models the relationship between a dependent variable and one or more independent variables.
* **Linear Regression Formula:**
    ```excel
    =LINEST(known_y's, known_x's, [const], [stats])
    ```
* **Toolpak Method:** `Data` > `Data Analysis` > `Regression` (Generates a full statistical summary table including R-squared and P-values).

### Forecasting with Excel
Predicting future values based on historical trends.
* **Linear Forecast:**
    ```excel
    =FORECAST.LINEAR(target_date, known_values, known_dates)
    ```
* **Visual Forecasting:** Use `Data` > `Forecast Sheet` to automatically generate a trend chart with confidence intervals based on Exponential Smoothing (ETS).

### Outlier Detection with Excel
Identifying anomalous data points that deviate significantly from the rest of the dataset.
* **Using Z-Score (Standardization):** Values with a Z-score > 3 or < -3 are typically outliers.
    ```excel
    =STANDARDIZE(A2, AVERAGE($A$2:$A$100), STDEV.P($A$2:$A$100))
    ```
* **Using Interquartile Range (IQR):**
    ```excel
    =QUARTILE.INC(array, 3) - QUARTILE.INC(array, 1)
    ```

---

## 2. Code Analysis

Programming languages allow for programmatic, repeatable, and complex data analysis pipelines.

### Data Analysis with Python
Python, powered by `pandas`, is the industry standard for programmatic data analysis.
* **Basic Exploratory Data Analysis (EDA):**
    ```python
    import pandas as pd

    df = pd.read_csv('data.csv')
    
    # Generate descriptive statistics (mean, std, min, max, quartiles)
    print(df.describe())
    
    # Value counts for categorical data
    print(df['category'].value_counts())
    
    # Grouping and aggregation
    summary = df.groupby('region')['sales'].agg(['mean', 'sum']).reset_index()
    ```

### Data Analysis with SQL
SQL is optimized for querying and analyzing large datasets directly within a relational database.
* **Window Functions for Analytics:**
    ```sql
    -- Calculate a running total and rank sales reps by performance
    SELECT 
        sales_rep,
        sales_amount,
        SUM(sales_amount) OVER (ORDER BY sale_date) AS running_total,
        RANK() OVER (ORDER BY sales_amount DESC) AS sales_rank
    FROM sales_data;
    ```

---
## 3. Database Analysis

### Data Analysis with Datasette
Datasette is an open-source tool that instantly turns SQLite databases into an interactive web interface and a REST API.
* **Use Case:** Great for rapidly publishing datasets, exploring data via a UI, and sharing analytical results as interactive tables or JSON endpoints without building a backend.
* **Execution:**
    ```bash
    datasette serve my_database.db
    ```

### Data Analysis with DuckDB
DuckDB is an analytical (OLAP) database optimized for fast querying on complex data, running entirely in-process.
* **Fast Aggregations on Raw Files:**
    ```sql
    -- Querying a Parquet file directly for aggregations
    SELECT 
        department, 
        AVG(salary) as avg_salary 
    FROM read_parquet('employees.parquet') 
    GROUP BY department 
    ORDER BY avg_salary DESC;
    ```

---

## 4. AI Analysis

### Vibe Analysis
"Vibe Analysis" refers to using Large Language Models (LLMs) to perform qualitative analysis, sentiment extraction, and pattern recognition on unstructured text data.
* **Workflow:** Passing bulk text (like user reviews, social media posts, or interview transcripts) to an LLM via API to classify the "vibe" (sentiment, urgency, underlying intent) that traditional rule-based sentiment analysis might miss.
* **Python Example (Pseudo-code via OpenAI/Gemini API):**

   ```python
    # Prompting an LLM to categorize the unstructured 'vibe' of a dataset
    prompt = f"Analyze the following feedback and categorize the overall 'vibe' as positive, frustrated, or confused. Feedback: {user_text}"

    ```

---

## 5. Specialized Analysis

### Geospatial Analysis with Excel
Handling location data within spreadsheets.
* **Geography Data Types:** Convert cells containing country/city names to the "Geography" data type (`Data` > `Data Types` > `Geography`) to automatically pull in demographic and spatial data.
* **3D Maps:** Use `Insert` > `3D Map` to plot geographic coordinates or location names onto a globe.

### Geospatial Analysis with Python
Using Python for programmatic mapping and spatial operations.
* **Using GeoPandas:**
    ```python
    import geopandas as gpd

    # Load a shapefile
    gdf = gpd.read_file("neighborhoods.shp")
    
    # Calculate the area of each polygon
    gdf['area'] = gdf.geometry.area
    
    # Plot the map
    gdf.plot(column='area', cmap='viridis', legend=True)
    ```

### Geospatial Analysis with QGIS
QGIS is a powerful, open-source desktop Geographic Information System (GIS) application.
* **Capabilities:** Used for viewing, editing, and analyzing geospatial data. Perfect for complex spatial joins, creating heatmaps, and layering vector (shapefiles/GeoJSON) and raster (satellite imagery) data visually without code.

### Network Analysis in Python
Analyzing relationships and connections between entities (nodes and edges).
* **Using NetworkX:**
    ```python
    import networkx as nx

    # Create a graph
    G = nx.Graph()
    G.add_edges_from([('UserA', 'UserB'), ('UserA', 'UserC'), ('UserB', 'UserD')])

    # Calculate Degree Centrality (who is the most connected?)
    centrality = nx.degree_centrality(G)
    print(centrality)
    ```

    
