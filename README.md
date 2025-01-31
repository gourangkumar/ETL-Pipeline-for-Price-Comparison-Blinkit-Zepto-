# ETL Pipeline for Price Comparison (Blinkit & Zepto)

## Project Overview
This project is an **ETL (Extract, Transform, Load) pipeline** for scraping product prices from **Blinkit** and **Zepto**, two online grocery platforms. The scraped data is cleaned, compared, and stored for further analysis. This project is built using **Python, BeautifulSoup, Requests, and Pandas** and can be deployed in a Jupyter Notebook.

## Features
- **Web Scraping**: Extracts product details from Blinkit and Zepto.
- **Data Cleaning**: Normalizes and structures product data.
- **Price Comparison**: Compares prices across platforms.
- **Storage**: Saves data in CSV format for analysis.
- **Scalability**: Can be extended to other e-commerce platforms.

## Tech Stack
- **Python**: Main programming language.
- **BeautifulSoup**: HTML parsing and data extraction.
- **Requests**: Fetches webpage content.
- **Pandas**: Data transformation and storage.
- **Jupyter Notebook**: Interactive execution.

---

## Installation
### Prerequisites
Ensure you have Python installed (version 3.7+).

### Install Required Libraries
```bash
pip install requests beautifulsoup4 pandas
```

---

## Running the Project
### Step 1: Open Jupyter Notebook
```bash
jupyter notebook
```

### Step 2: Execute the script step by step.

### Step 3: View the comparison data.
```python
import pandas as pd
comparison_df = pd.read_csv("price_comparison.csv")
comparison_df.head()
```

---

## Future Enhancements
- Automate scraping using **Airflow**.
- Store data in a **PostgreSQL or MongoDB database**.
- Build a **dashboard using Streamlit** for visualization.
- Expand to more e-commerce platforms.

## Contribution
Feel free to fork this project, submit PRs, and improve it.

## License
This project is open-source under the MIT License.
