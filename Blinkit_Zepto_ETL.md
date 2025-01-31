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

## How It Works
### 1. Extract Data (Web Scraping)
**Blinkit Scraper:**
```python
import requests
from bs4 import BeautifulSoup

def scrape_blinkit(search_query):
    url = f"https://www.blinkit.com/s/?q={search_query}"
    headers = {"User-Agent": "Mozilla/5.0"}
    response = requests.get(url, headers=headers)
    
    if response.status_code != 200:
        print("Failed to retrieve Blinkit data")
        return []
    
    soup = BeautifulSoup(response.text, "html.parser")
    products = soup.find_all("div", class_="ProductCard__Details")
    
    blinkit_data = []
    for product in products:
        name = product.find("div", class_="ProductCard__Name")
        price = product.find("div", class_="ProductCard__Price")
        availability = "In stock" if "Out of stock" not in product.text else "Out of stock"
        
        if name and price:
            blinkit_data.append({
                "platform": "Blinkit",
                "name": name.text.strip(),
                "price": price.text.strip(),
                "availability": availability
            })
    
    return blinkit_data
```

**Zepto Scraper:**
```python
def scrape_zepto(search_query):
    url = f"https://www.zeptonow.com/search?q={search_query}"
    headers = {"User-Agent": "Mozilla/5.0"}
    response = requests.get(url, headers=headers)
    
    if response.status_code != 200:
        print("Failed to retrieve Zepto data")
        return []
    
    soup = BeautifulSoup(response.text, "html.parser")
    products = soup.find_all("div", class_="ProductItem__Details")
    
    zepto_data = []
    for product in products:
        name = product.find("div", class_="ProductItem__Name")
        price = product.find("div", class_="ProductItem__Price")
        availability = "In stock" if "Out of stock" not in product.text else "Out of stock"
        
        if name and price:
            zepto_data.append({
                "platform": "Zepto",
                "name": name.text.strip(),
                "price": price.text.strip(),
                "availability": availability
            })
    
    return zepto_data
```

### 2. Transform Data (Compare Prices)
```python
import pandas as pd

def compare_prices(search_query):
    blinkit_results = scrape_blinkit(search_query)
    zepto_results = scrape_zepto(search_query)
    
    blinkit_df = pd.DataFrame(blinkit_results)
    zepto_df = pd.DataFrame(zepto_results)
    
    comparison_df = pd.merge(blinkit_df, zepto_df, on="name", suffixes=("_blinkit", "_zepto"))
    comparison_df.to_csv("price_comparison.csv", index=False)
    
    return comparison_df

search_product = "milk"  # Change product name as needed
comparison_df = compare_prices(search_product)
print(comparison_df)
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

---

## Contribution
Feel free to fork this project, submit PRs, and improve it.

## License
This project is open-source under the MIT License.
