# Amazon Product Price Tracker

A Python web-scraping project that extracts product information from an Amazon product page, tracks its price over time, saves the results in a CSV file, and sends an email alert when the price drops below a target threshold.

> **Note:** This project was built for learning and portfolio purposes. Amazon’s page structure and anti-bot policies can change, so the scraper may require updates or may not work reliably in production.

## Features

- Scrapes an Amazon product page using `requests`
- Extracts the product title and current price using BeautifulSoup
- Cleans raw scraped text
- Adds a date timestamp to every record
- Saves data to a CSV file
- Appends new price records instead of overwriting existing data
- Runs the scraper automatically once per day
- Sends an email notification when the price drops below a target value

## Tech Stack

- Python 3
- Jupyter Notebook
- Requests
- BeautifulSoup
- Pandas
- CSV
- SMTP / Gmail

## Project Workflow

1. The script sends an HTTP request to the Amazon product page.
2. BeautifulSoup parses the returned HTML.
3. The product title and price are extracted.
4. The price is cleaned by removing unwanted characters.
5. The current date is recorded.
6. The title, price, and date are appended to `AmazonWebScraperDataset.csv`.
7. The process repeats once every 24 hours.
8. If the price is below the target, an email alert can be sent.

## Files

| File | Description |
|---|---|
| `Amazon-Web-Scraper-Project.ipynb` | Main Jupyter Notebook containing the scraper, data storage, automation, and email-alert logic |
| `AmazonWebScraperDataset.csv` | Generated CSV file containing product title, price, and collection date |

## Installation

1. Clone this repository:

```bash
git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
cd your-repo-name
```

2. Create and activate a virtual environment:

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS/Linux
source venv/bin/activate
```

3. Install the required libraries:

```bash
pip install requests beautifulsoup4 pandas
```

4. Open the notebook:

```bash
jupyter notebook Amazon-Web-Scraper-Project.ipynb
```

## Usage

1. Open the notebook.
2. Replace the `URL` variable with the Amazon product page you want to track.
3. Update the HTML element IDs if Amazon has changed its page structure.
4. Run the cells in order.
5. To enable email alerts, update the email configuration and use an app password rather than your normal Gmail password.

### Example output

```text
Funny Got Data MIS Data Systems Business Analyst T-Shirt
16.99
```

### CSV format

| Title | Price | Date |
|---|---:|---|
| Funny Got Data MIS Data Systems Business Analyst T-Shirt | 16.99 | 2021-08-21 |

## Email Alerts

The notebook includes an optional `send_mail()` function that uses Gmail SMTP to notify you when the product price falls below a selected value.

For security, do **not** hard-code your email password in the notebook. Use environment variables or a `.env` file instead:

```python
import os

EMAIL_ADDRESS = os.getenv("EMAIL_ADDRESS")
EMAIL_PASSWORD = os.getenv("EMAIL_PASSWORD")
```

Gmail requires an **App Password** for SMTP access when two-factor authentication is enabled.

## Important Notes

- Web scraping may violate a website’s Terms of Service. Use this project only for educational purposes and respect `robots.txt`, rate limits, and website policies.
- Amazon frequently changes its HTML structure, so selectors such as `productTitle` and `priceblock_ourprice` may need to be updated.
- The current version tracks one product and assumes a stable page layout.
- The daily scheduler uses an infinite `while` loop with `time.sleep(86400)`, which is suitable for local experimentation but not ideal for production deployment.

## Possible Improvements

- Add error handling for failed requests or missing HTML elements
- Track multiple Amazon products
- Store data in SQLite or PostgreSQL instead of CSV
- Add price visualization using Matplotlib or Plotly
- Schedule the scraper using `schedule`, cron, or GitHub Actions
- Use environment variables for email credentials
- Add logging and retry logic
- Convert the notebook into a modular Python application

## Learning Outcomes

Through this project, I practiced:

- Web scraping with Python
- HTML parsing using BeautifulSoup
- Data cleaning and timestamping
- Working with CSV files
- Automating repetitive tasks
- Sending automated email notifications
- Building a simple data-collection pipeline

## License

This project is for educational purposes only.
