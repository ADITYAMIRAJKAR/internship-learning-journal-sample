## 1. What is an API? (The "Waiter" Analogy)
Imagine you are at a restaurant:
* **You** are the **Client** (the user/app).
* **The Kitchen** is the **Server** (where the data/food is).
* **The Waiter** is the **API** (Application Programming Interface).

You don't go into the kitchen to cook. You give your order to the waiter. The waiter takes the request to the kitchen and brings the food back to you. 

**Technical Definition:** An API is a set of rules that allows one software program to "talk" to another to exchange data or perform tasks securely.

### Why do we need it?
1. **Security:** Servers don't have to show you their whole "kitchen" (database), just the specific data you asked for.
2. **Efficiency:** Instead of building a weather station or a map system from scratch, you just "call" the Google Maps or BBC Weather API.
3. **Connectivity:** It’s how your phone syncs your Instagram feed or how a travel site compares prices from 50 different airlines at once.



---

## 2. How an API Call Works (The Request-Response Cycle)

1. **The Request:** Your code sends a message to a specific URL (the **Endpoint**).
2. **Parameters:** You add details like `city=Mumbai` or `api_key=12345` to the URL.
3. **The Processing:** The server validates your key and looks up the data.
4. **The Response:** The server sends back a **JSON** file (a structured text format that looks like a list).

---

## 3. API & Scraping Examples

### A. Professional API: BBC Weather
This experiment uses the official BBC locator API to find a city and then extract weather details.

* **Libraries:** `beautifulsoup4`, `requests`, `pandas`, `re` (Regex), `datetime`.
* **Extracted Data:** Daily High/Low Temp (°C), Weather Summary, and Date.

```python
import requests
from urllib.parse import urlencode

required_city = "Mumbai"
location_url = 'https://locator-service.api.bbci.co.uk/locations?' + urlencode({
   'api_key': 'AGbFAKx58hyjQScCXIYrxuEwJh2W2cmv',
   's': required_city,
   'stack': 'aws',
   'locale': 'en',
   'filter': 'international',
   'place-types': 'settlement,airport,district',
   'order': 'importance',
   'a': 'true',
   'format': 'json'
})
result = requests.get(location_url).json()
result
```
### B. Library Wrapper: Wikipedia Data Extraction

Instead of writing complex URLs, we use a Python library that "wraps" the API for us.
* **Libraries:** wikipedia, pandas.
* **Key Functions:**
    * `wikipedia.search("Keyword"):` Searches for relevant articles.

    * `wikipedia.summary("Title", sentences=3):` Gets a quick summary.

    * `wikipedia.page("Title"):` Accesses full content, images, and links.

### C. Browser Scraping: IMDb (JavaScript Console)

Sometimes you don't need Python. You can scrape directly from the browser's "Console."

1. **Inspect:** Right-click the movie title -> Inspect (Ctrl+Shift+I).

2. **Select:** Find the `div` or `li` that wraps the movie info.

3. **Console:** Run the following code to extract all 250 movies:

```bash
document.querySelectorAll(".ipc-metadata-list-summary-item") #returns a nodelist of all 250 movies

$$(".ipc-metadata-list-summary-item") # return a list of all 250 movies

$$(".ipc-metadata-list-summary-item").map(item => [
    item.querySelector(".ipc-title-link-wrapper").href,
    item.querySelector(".ipc-title__text").textContent,
    item.querySelector(".cli-title-metadata-item:nth-child(1)").textContent,
    item.querySelector(".cli-title-metadata-item:nth-child(2)").textContent,
    item.querySelector(".cli-title-metadata-item:nth-child(3)")?.textContent,
    item.querySelector(".ipc-rating-star").textContent,
]) 
#returns a list of all the movie content

```

### D. Automated Browser: Playwright

Playwright is used for "Headless" scraping—where a script controls a browser to click buttons or wait for JavaScript to load.

```bash
from playwright.sync_api import sync_playwright


def scrape_quotes():
    with sync_playwright() as p:
        # Channel is optional. Use "chrome", "msedge", "chrome-beta", "msedge-beta", "msedge-dev"
        browser = p.chromium.launch(headless=True, channel="chrome")
        page = browser.new_page()
        page.goto("https://quotes.toscrape.com/js/")
        quotes = page.query_selector_all(".quote")
        for q in quotes:
            text = q.query_selector(".text").inner_text()
            author = q.query_selector(".author").inner_text()
            print(f"{text} — {author}")
        browser.close()


if __name__ == "__main__":
    scrape_quotes()
```

---

## 4. No-Code Scraping Methods (For Non-Programmers)

If you don't want to write a single line of Python code, you can use built-in tools in Excel and Google Sheets to pull data instantly.

### Method 1: Microsoft Excel (Power Query)
Excel has a powerful engine called "Power Query" that can "read" a website and turn its tables into a spreadsheet.
1.  **Copy the Link:** Go to the website you want to copy data from (e.g., [TimeAndDate Weather - Bengaluru](https://www.timeanddate.com/weather/india/bengaluru/ext)).
2.  **Open Excel:** Go to the **Data** tab.
3.  **Get Data:** Select **Get Data** -> **From Other Sources** -> **From Web**.
4.  **Connect:** Paste the URL and click OK. 
5.  **Navigator:** A window will appear showing all tables found on that page. Select the table you need, click **Transform Data** (to clean it) or **Load** (to import it immediately).

### Method 2: Google Sheets (`IMPORTHTML`)
Google Sheets has a "magic" formula that fetches live data from a website and keeps it updated.
* **The Formula:** `=IMPORTHTML("URL", "query", index)`
* **The Parameters:**
    * **URL:** The link to the website.
    * **Query:** Use `"table"` or `"list"`.
    * **Index:** The number of the table on the page (starting from 1).
* **Example:** `=IMPORTHTML("https://en.wikipedia.org/wiki/List_of_countries_by_population", "table", 1)`

---

## 5. Scheduled Scraping with GitHub Actions

What if you want to scrape data every day at 8:00 AM automatically without keeping your computer on? You use **GitHub Actions**.

### Required Libraries
* **httpx:** A high-performance library for making web requests (faster than `requests`).
* **lxml:** A library used for parsing HTML and XML data extremely quickly.

### Process of setting up GitHub Actions for Scheduled Scraping:

1.  **Create the Script:** Write your Python scraping script (e.g., `scraper.py`) and test it locally.
2.  **Workflow Folder:** Inside your GitHub repository, create a folder path: `.github/workflows/`.
3.  **The YAML Configuration:** Create a file (e.g., `daily_scrape.yml`) inside that folder. This file tells GitHub:
    * **When to run:** Using a "Cron" schedule (e.g., `0 8 * * *` for 8 AM daily).
    * **What to do:** Install Python, install your libraries (`pip install httpx lxml`), and run `python scraper.py`.
4.  **Git Commit:** The action can be configured to "Commit" the new data (CSV or JSON) back into your repository automatically.
5.  **Verification:** Check the "Actions" tab in your GitHub repository to see the logs and ensure the "Virtual Machine" is running your code successfully.



---

## 🚀 Summary Checklist
* **API:** Use when the website provides a structured "doorway" (e.g., BBC, Wikipedia).
* **Scraping:** Use when there is no API and you must "read" the visual page (e.g., IMDb, Quotes).
* **Automation:** Use GitHub Actions for recurring tasks.
