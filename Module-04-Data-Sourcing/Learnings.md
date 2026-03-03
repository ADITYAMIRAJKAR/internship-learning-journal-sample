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

## 7. Document Standardization (MarkItDown)

**Overview:**
I explored Microsoft's MarkItDown, a tool designed to convert diverse file formats into standardized Markdown, optimizing them for LLM consumption.

**Key Skills Acquired:**
* Operating the tool without an LLM for rapid, direct parsing of structured documents and simple PDFs.
* Pairing it with an LLM to activate OCR capabilities, understand complex layouts, and boost formatting accuracy.

**Core Concepts:**
* Markdown is optimal because it is lightweight, readable by humans, platform-independent, and highly conducive to RAG (Retrieval-Augmented Generation) chunking.
* While MarkItDown is a strong tool, alternatives like Docling are currently more feature-rich and mature.
* High-quality data preprocessing is the absolute foundation for getting good performance out of AI systems.

**Practical Application:**
This workflow is vital for cleaning PDFs, structuring enterprise knowledge bases, generating datasets, and preparing RAG pipelines.

---

## 8. Geocoding with Nominatim


**Overview:**
Learned how to translate plain-text location names (e.g., "IIT Madras") into highly structured geographic coordinates.

**Key Skills Acquired:**
* Accessing the OpenStreetMap-powered Nominatim service using the `geopy` Python library.
* Ensuring the mandatory `user_agent` parameter is passed during the API call.
* Extracting attributes like Longitude, Latitude, display names, bounding boxes, and categorizations (such as type: "university" or class: "amenity") from the returned JSON.

**Practical Application:**
Converting unstructured text into spatial intelligence is highly applicable for geo-tagging data, delivery logistics, urban planning, and mapping applications.

---

## 9. Advanced Scraping & Debugging Strategies (DocSearch)

**Overview:**
This session covered the philosophy and strategy of building a semantic search engine proof-of-concept.

**Key Concepts & Techniques:**
* **Keyword vs. Semantic Search:** Keyword relies on identical word matching, while semantic uses vector embeddings to match the actual meaning of the query.
* **The Power of Caching:** Writing a `cached_get()` function to save HTML responses to the local disk. This stops the script from re-downloading files on every run, safely handles interruptions, and drastically accelerates debugging. 
* **Modular Scraping:** Breaking the architecture into tiny steps: fetching archives -> extracting URLs -> removing duplicates -> downloading articles -> parsing text -> saving data.
* **XPath Mastery:** Using DevTools to find stable parent `div` containers and avoiding volatile sidebars. Relying on the `contains()` function in XPath instead of exact class matches to handle website variations.
* **Incremental Saves:** Writing JSON data to the disk *inside* the execution loop. This prevents catastrophic data loss if the scraper crashes hours into a run.
* **Handling Edge Cases:** Building logic to anticipate empty HTTP 200 responses, class mismatches, URL redirects, and duplicates.

**Top Debugging Tips:**
1.  Print variables constantly to ensure assumptions meet reality.
2.  Deploy `breakpoint()` commands to freeze execution and inspect the environment.
3.  Use "Rubber Ducking" by explaining the broken code aloud to an LLM or a peer.

---

## 10. Extracting Data from PDFs


**Overview:**
PDF scraping requires a completely different pipeline compared to standard HTML extraction due to layout complexities.

**Key Skills Acquired:**
* **Bulk Downloading:** Using BeautifulSoup to scrape anchor tags, isolating `.pdf` links, pulling the filename via `link.split("/")[-1]`, and writing the files to disk in binary mode. This eliminates manual downloading.
* **Table Extraction:** Utilizing the `tabula` library (`read_pdf()`), which operates very similarly to Pandas.
* **Fixing Layout Errors:** When scraping landscape pages, Tabula frequently pulled in garbage text (like logos or headers). I solved this by passing exact bounding box coordinates using the `area=[top, left, bottom, right]` argument to force the scraper to only look at the table grid.
* **Direct Export:** Using the `convert_into()` function to bypass manual formatting and dump the extracted tables straight into CSVs.

**Practical Application:**
This automated pipeline is perfect for extracting tables from research papers, sports statistics, government records, and corporate financial reports.

---

## 11. Vibe Coding

**Overview:**
This module focused on modern "idea-first" development workflows rather than getting lost in "syntax-first" coding.

**Key Skills Acquired:**
* Translating abstract problem statements into structured, actionable coding steps.
* Harnessing AI assistance for rapid application prototyping.
* Integrating APIs, parsing JSON payloads, and properly isolating API keys in environment variables for security.
* Practicing effective prompt engineering to force LLMs to output clean, modular code.

**Overall Takeaway:**
This workshop massively boosted my confidence in designing products rather than just writing scripts. It proved that AI vastly accelerates development velocity, provided the developer maintains strong logical structuring and problem-solving skills.
