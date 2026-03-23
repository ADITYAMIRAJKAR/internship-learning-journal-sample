## Cleaning Steps – Data Preparation

## Overview
Raw datasets are often messy and not directly suitable for analysis. They may contain duplicate records, missing values, inconsistent text formats, or unnecessary columns.  
Data cleaning helps transform this raw data into a structured and reliable dataset that can be used for analysis and machine learning tasks.

In this module, I learned how to clean and prepare datasets using tools such as spreadsheets, shell commands, text editors, and SQL tools like DuckDB.

---

### Inspecting the Data
The first step in cleaning a dataset is understanding its structure.  
This involves checking the columns, data types, missing values, and the overall size of the dataset.

Example commands:

```bash
head data.csv
```

Displays the first few rows of the dataset.

```bash
wc -l data.csv
```

Counts the number of rows in the dataset.

---

### Removing Duplicate Records
Duplicate rows can distort analysis results, so they should be removed.

Example command:

```bash
sort data.csv | uniq > cleaned_data.csv
```

Explanation:
- `sort` organizes the rows
- `uniq` removes duplicate records

---

### Handling Missing Values
Datasets often contain missing or empty fields. These values must be identified and handled appropriately.

Possible approaches:
- Fill missing values
- Remove incomplete rows
- Replace missing data with default values

Example command to locate missing values:

```bash
grep ",," data.csv
```

This helps find rows that may contain empty fields.

---

### Filtering Unwanted Data
Sometimes we only need rows that match certain conditions.

Example command:

```bash
grep "India" data.csv
```

This extracts rows containing the word **India**.

To exclude rows:

```bash
grep -v "India" data.csv
```

The `-v` option removes rows that match the pattern.

---

### Extracting Required Columns
Large datasets may contain many columns, but only some are needed for analysis.

Example command:

```bash
cut -d',' -f1,3,5 data.csv
```

Explanation:
- `-d','` specifies the delimiter
- `-f1,3,5` selects specific columns

---

### Cleaning and Standardizing Text
Text values may appear in inconsistent formats such as uppercase or lowercase variations.

Example command:

```bash
sed 's/india/India/g' data.csv
```

This replaces all occurrences of "india" with "India".

Another example:

```bash
tr 'A-Z' 'a-z' < data.csv
```

This converts all uppercase letters to lowercase.

---

### Restructuring Data
Sometimes multiple pieces of information are stored in a single column and need to be separated.

Example using `awk`:

```bash
awk -F',' '{print $1,$2}' data.csv
```

Explanation:
- `awk` helps process structured text
- `-F','` specifies the column delimiter

---

### Sorting and Aggregating Data
Sorting and grouping data helps in summarizing information.

Example command:

```bash
sort data.csv
```

Counting unique values:

```bash
cut -d',' -f2 data.csv | sort | uniq -c
```

This counts how many times each value appears.

---

### Preparing Data Using SQL (DuckDB)
For larger datasets, SQL-based tools like DuckDB can be used to transform and query data.

Example query:

```sql
SELECT column_name, COUNT(*)
FROM dataset
GROUP BY column_name;
```

This groups records and calculates aggregated values.

---

## Conclusion
Data cleaning is an essential step in the data preparation process. By inspecting datasets, removing duplicates, handling missing values, standardizing text, and restructuring data using tools like shell commands and SQL, raw data can be transformed into a clean and reliable dataset ready for analysis.
