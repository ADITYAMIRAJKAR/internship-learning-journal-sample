# Module 4 – Internship Learnings

## 1. Web Data Extraction via Excel


**Overview:**
In this session, I explored how to bypass complex coding by pulling live website data straight into Excel utilizing the Power Query tool. 

**Key Skills Acquired:**
* Navigating to the Data tab, selecting "Get Data," and choosing the "From Web" option to initiate an import.
* Creating a live connection by feeding the target website URL into the prompt.
* Scanning the webpage to identify and select the appropriate data tables.
* Leveraging the Query Editor to filter out unnecessary columns, preview information, and apply data transformations before finalizing the import.
* Understanding the "Applied Steps" window, which sequentially logs every modification made to the dataset.
* Importing the finalized, clean table directly into an Excel sheet.
* Using the refresh functionality to dynamically sync the spreadsheet with the latest live web data.

**Core Concepts:**
* Excel functions as a highly capable, lightweight web scraper.
* The spreadsheet maintains an active link to the original web source.
* Refreshing the data updates the values automatically.
* Any saved transformations are reapplied instantly upon refreshing.

**Practical Application:**
I successfully imported a two-week weather forecast for Chennai. This dataset is now primed for trend analysis, dashboard integration, and visual reporting.

---

## 2. Scraping with Python (IMDB Case Study)


**Overview:**
This module covered using Python to programmatically extract structured information from IMDB. 

**Key Skills Acquired:**
* Importing foundational scraping libraries: `requests`, `BeautifulSoup`, and `pandas`.
* Utilizing `requests` to grab the raw webpage content.
* Applying `BeautifulSoup` to parse the raw HTML code.
* Using browser developer tools (Inspect) to locate class names, tag names, and nested elements.
* Grasping HTML hierarchies: Parent containers group multiple records together, while lower-level child tags hold the precise data points.
* Targeting specific data, such as using `a.text` for movie titles, `span.text` for release years, and `strong.text` for user ratings.
* Appending the scraped data into Python lists.
* Transforming these lists into a structured `pandas` DataFrame for clean, tabular display.

**Core Concepts:**
* Websites are fundamentally built on structured HTML tags.
* Successful scraping requires precise identification of parent and child relationships.
* Targeting higher-level containers makes it easy to loop through and extract multiple rows of data.
* The `pandas` library is crucial for taking messy scraped text and turning it into a structured format.

**Practical Application:**
I wrote a script that successfully scraped the IMDB Top Movies page, converting it into a clean table ready for deeper processing and visualization.

---

## 3. Querying the Wikipedia API

**Overview:**
Instead of fighting with raw HTML, this session taught me how to use the official Python `wikipedia` wrapper library to fetch structured data instantly.

**Key Skills Acquired:**
* Installing external packages using `pip`.
* Utilizing the `search()` method to locate relevant Wikipedia topics.
* Using the `summary()` function to pull brief overviews, utilizing the `sentences` parameter to restrict the length of the output.
* Calling the `page()` method to download comprehensive article data.
* Extracting specific page properties like `.references`, `.images`, and the `.url`.
* Grabbing tabular data by passing the page's HTML directly into `pandas.read_html()`.

**Core Concepts:**
* The wrapper library abstracts away the tedious parts of HTML parsing.
* It offers highly structured access to a massive knowledge base.
* Since Wikipedia stores tables as lists within the code, locating the correct table often requires a bit of trial-and-error with index numbers.

**Practical Application:**
I can now rapidly pull structured knowledge from Wikipedia, which is highly useful for automating research, academic data collection, and broader analysis tasks.

---

## 4. Extracting BBC Weather Data

**Overview:**
This lab involved building a Python scraper specifically targeted at BBC Weather to collect structured forecasting data.

**Key Skills Acquired:**
* Deploying `find_all()` to scrape multiple matching HTML elements at once.
* Isolating the exact data needed from the resulting element lists.
* Cleaning dirty text data using string splitting, regular expressions, and indexing.
* Converting text strings into usable numerical types.
* Managing and cleaning special formatting, such as degree symbols.
* Using `pandas` to dynamically generate sequential date columns.
* Merging various data lists into a unified DataFrame.
* Exporting the final output into Excel and CSV files.

**Core Concepts:**
* Scraping fundamentally requires pulling raw HTML from servers.
* `requests` does the fetching, while `BeautifulSoup` handles the parsing.
* Data cleaning is just as critical as the extraction phase itself.
* You must always verify the legal guidelines of a website before deploying a scraper.

**Practical Application:**
I compiled a pristine, 14-day weather forecast dataset for Mumbai that is fully prepared for comparative analysis and visual plotting.

---

## 5. Automation via GitHub Actions


**Overview:**
I learned to automate DevOps and scraping workflows using GitHub Actions based on pull requests, pushes, or time schedules (cron).

**Key Skills Acquired:**
* Setting up YAML configuration files strictly inside the `.github/workflows/` directory.
* Structuring Cron expressions (Minute, Hour, Day, Month, Day-of-week) to dictate execution times.
* Example: Using `*/5 * * * *` to trigger a workflow every five minutes.
* Understanding that all scheduled tasks operate on the UTC timezone.

**Core Concepts:**
* While a task might be scheduled every 5 minutes, GitHub's internal queueing means exact execution times are not guaranteed.
* Because of these delays, cron schedules are inappropriate for strict real-time monitoring.

**Practical Application:**
This technology is perfect for scheduling monthly reporting, triggering regular backups, executing security audits, and running automated deployments.

---

## 6. Vision-Based Scraping (Gemini)

**Overview:**
Instead of navigating messy DOM structures with Selenium or BeautifulSoup, this session introduced recording screen content and passing the frames to a multimodal LLM to pull structured data.

**Key Skills Acquired:**
* Recording screen activity at 1 frame-per-second to generate analyzable image sequences.
* Passing these sequential frames into Gemini for processing.
* Forcing the LLM into JSON mode to guarantee a structured data output.

**Core Concepts:**
* This approach bypasses HTML entirely, relying purely on computer vision.
* It easily parses JavaScript-rendered and highly dynamic websites without complex browser automation.
* At approximately 250 tokens per image, analyzing 1,000 frames only costs a few cents, making it highly cost-efficient.
* *Limitations:* It cannot scrape what isn't visible on screen, will miss data if the page scrolls too fast, and isn't meant for massive, high-speed extraction tasks.

**Practical Application:**
This signifies a massive shift in data extraction from writing brittle code-based logic to leveraging adaptable vision-based AI.

---
