#  Module 5 – Data Preparation
**Topic:** Data Cleansing, Transformation, Shell Scripting, DuckDB, OpenRefine, and Media Processing

---

## Concept Explanations

Data preparation is the most time-consuming phase of the data science lifecycle. Real-world data is rarely clean; it is often unstructured, inconsistent, and noisy. This module focuses on the tools and techniques required to transform raw data into an analysis-ready format.

### 1. Excel Preparation
Excel remains one of the most powerful and widely used tools for quick data manipulation.
* **Data Cleansing:** Removing anomalies like extra spaces, blank cells, and invisible characters using formulas like `TRIM()` and `CLEAN()`. Or using "Go To Special" to find and delete blank rows.
* **Data Transformation:** Standardizing date formats, standardizing country codes (e.g., converting "U.S.A" and "United States" to "USA"), and handling missing values.
* **Splitting Text:** Using the "Text-to-Columns" feature or text manipulation formulas (`LEFT`, `RIGHT`, `MID`, `FIND`, `LEN`) to split combined strings (e.g., "Last Name, First Name").
* **Data Aggregation:** Summarizing large datasets using Pivot Tables and aggregate functions like `SUMIFS` and `COUNTIFS`.

### 2. Command Line Tools
For large files (like Apache server logs), opening them in Excel or an Editor will crash your system. The Shell is the best tool for this.
* **Data Preparation in the Shell:** Using UNIX tools like `grep` (filtering), `sed` (stream editing/substitution), `awk` (pattern scanning and processing), and `cut` (extracting columns).
* **Data Preparation in the Editor:** Using advanced features in VS Code such as **Multi-cursor editing** (to edit multiple lines simultaneously) and Regex (Regular Expression) Find and Replace.

### 3. Database Tools
* **DuckDB:** An in-process SQL OLAP database management system. It is incredibly fast and allows you to run SQL queries directly on `CSV`, `JSON`, and `Parquet` files without needing to import them into a traditional database server first.
* **dbt (Data Build Tool):** A transformation workflow tool that allows data teams to write modular SQL `SELECT` statements. It handles the "T" (Transform) in ELT (Extract, Load, Transform) pipelines.

### 4. Specialized Tools
* **OpenRefine:** An open-source tool built specifically for cleaning messy data. It excels at **Clustering** and **Faceting**. For example, it uses algorithms like "Key Collision" and "Fingerprinting" to group and merge inconsistent text entries like "IBM", "I.B.M.", and "International Business Machines" into a single standard name.
* **Parsing JSON:** Dealing with deeply nested JSON data. Tools like `jq` in the command line or the `json` library in Python allow for safe extraction of specific keys.

### 5. Media Processing
Data isn't just text; it includes images, audio, and video.
* **Transforming Images:** Compressing images to save bandwidth without losing essential features (e.g., converting PNG/JPEG to WebP). Command-line tools like `cwebp` or `mogrify` are used for bulk processing.
* **Extracting Audio and Transcripts:** Using `yt-dlp` to download media, `ffmpeg` to rip audio from video, and tools like `faster-whisper` or LLM APIs (Gemini/OpenAI) to generate text transcripts from audio files.

---

## Examples and Code Snippets

### 1. Excel Text Splitting Formulas
Extracting the first name from a "Last Name, First Name" format in cell A1:
```excel
=MID(A1, FIND(",", A1) + 2, LEN(A1))

```
### 2. Shell Commands for Data Prep
Extracting lines from an Apache Log containing the word "GET" and cutting out the IP address (assuming it's the first column):

```
grep "GET" access.log | cut -d' ' -f1 > ip_addresses.txt

```
### 3. Parsing JSON in the Shell with jq
Extracting the name field from a JSON array of users:

```Bash
cat users.json | jq '.[] | .name'

```
