# CIS4340 Homework 03 – Project Summary

## Name: Matheus Santos Gomes

## Overview

The goal of this assignment was to extract Falcon 9 and Falcon Heavy booster launch data from the Wikipedia page **List of Falcon 9 first-stage boosters** using two different scraping approaches:

1. Traditional Python web scraping  
2. AI-assisted web scraping using ScrapeGraphAI  

The extracted data was then used to generate multiple reports such as Falcon 9 only launches, Falcon Heavy launches, Block type reports, turnaround reports, and most launches reports.

---

# Selected Traditional Scraper: Beautiful Soup

## Why Beautiful Soup Was Selected

I selected **Beautiful Soup** instead of Scrapy for this assignment because:

- It is lightweight and simple to install.
- It is efficient for scraping a single webpage.
- Wikipedia data is organized in HTML tables, which Beautiful Soup handles well.
- It allows quick navigation through tags such as `<table>`, `<tr>`, and `<td>`.
- It required less setup time than Scrapy.

Since this assignment focused on one webpage rather than crawling multiple pages, Beautiful Soup was the most practical option.

---

## Quick Review of Steps and Time Required

### Steps Used

1. Sent an HTTP request to the Wikipedia page using the `requests` library.
2. Parsed the webpage HTML using `BeautifulSoup`.
3. Located the booster history tables.
4. Iterated through rows and columns.
5. Extracted required fields:
   - Engine number
   - Block type
   - Flight number
   - Flight type
   - Launch date
   - Launch pad
   - Landing location
   - Turnaround time
   - Engine status
   - Total launches
6. Cleaned irregular formatting and converted dates to `YYYY-MM-DD`.
7. Printed CSV output to STDOUT and redirected into `Blocks.csv`.

### Approximate Time

- Initial scraper development: **1 hour**
- Cleaning irregular rows / debugging: **2+ hours**
- Building report scripts: additional time

---

# ScrapeGraphAI Prompt Review

ScrapeGraphAI was used as the AI-assisted scraping tool.

```text
Return ONLY valid JSON. No markdown. No explanation.

Extract Falcon 9 or Falcon Heavy launch rows from the provided HTML tables.

Return exactly this structure:

{
  "records": [
    {
      "engine_number": "",
      "block_type": "",
      "flight_number": "",
      "flight_type": "",
      "launch_date": "",
      "launch_pad": "",
      "landing_location": "",
      "turnaround_days": "",
      "status": "",
      "total_launches": ""
    }
  ]
}

Rules:
- Include only launches where the flight number begins with F9 or FH.
- flight_type must be F9 for Falcon 9 or FH for Falcon Heavy.
- engine_number should preserve IDs such as B0003, B1058, etc.
- block_type should match the engine version shown in the table.
- Convert launch dates into YYYY-MM-DD format.
- Preserve launch pad values such as LC-40, LC-39A, or SLC-4E.
- Preserve landing locations exactly when available.
- If turnaround time is missing, use 0.
- If total launches is missing, use 1.
- Do not summarize, explain, or add commentary.
- Return JSON only.
