
# Analyzing Historical Stock Revenue Data and Building a Dashboard

## Project Overview
This project aims to extract and visualize historical stock revenue data for Tesla and GameStop. The project utilizes the `yfinance` library to gather stock price data and web scraping techniques to extract revenue data from financial websites. The final output consists of interactive graphs displaying stock prices alongside their corresponding revenue data.

## Table of Contents
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Data Extraction](#data-extraction)
- [Graphing Function](#graphing-function)
- [Usage](#usage)
- [About the Authors](#about-the-authors)
- [Change Log](#change-log)

## Technologies Used
- Python
- Libraries: 
  - `yfinance`
  - `pandas`
  - `requests`
  - `bs4` (BeautifulSoup)
  - `plotly`

## Installation
Ensure you have Python installed on your system. Use the following commands to install the required libraries:

```bash
pip install yfinance
pip install pandas
pip install requests
pip install beautifulsoup4
pip install plotly
```

## Data Extraction
The project extracts stock data for Tesla and GameStop using the `yfinance` library and scrapes revenue data from [MacroTrends](https://www.macrotrends.net/). 

### Steps:
1. **Extract Tesla Stock Data**: 
   - Using `yfinance` to get the historical stock prices.
2. **Scrape Tesla Revenue Data**: 
   - Web scraping using BeautifulSoup to extract quarterly revenue data.
3. **Extract GameStop Stock Data**: 
   - Using `yfinance` for historical stock prices.
4. **Scrape GameStop Revenue Data**: 
   - Web scraping for quarterly revenue data.

## Graphing Function
The `make_graph` function creates an interactive dashboard that displays:
- Historical Share Price of the stock.
- Historical Revenue of the stock.

### Function Definition
```python
def make_graph(stock_data, revenue_data, stock):
    # Function implementation here
```

## Usage
1. Clone the repository or download the Jupyter Notebook.
2. Run the `final_assignment.ipynb` notebook in Jupyter Lab or Jupyter Notebook.
3. Follow the instructions within the notebook to visualize the data.

### Example of Function Call:
```python
make_graph(tesla_data, tesla_revenue, 'Tesla')
make_graph(gme_data, gme_revenue, 'GameStop')
```

## About the Authors
- **Joseph Santarcangelo**: PhD in Electrical Engineering, specializes in machine learning, signal processing, and computer vision.
- **Azim Hirjani**: [Add a brief bio if available]

## Change Log
| Date       | Version | Changed By      | Change Description                 |
|------------|---------|-----------------|------------------------------------|
| 2020-11-10 | 1.1     | Malika Singla   | Deleted the Optional part          |
| 2020-08-27 | 1.0     | Malika Singla   | Added lab to GitLab                |

---

### Sample `final_assignment.ipynb` Outline

```markdown
# Final Assignment: Analyzing Historical Stock Revenue Data

## Import Libraries
```python
import yfinance as yf
import pandas as pd
import requests
from bs4 import BeautifulSoup
import plotly.graph_objects as go
from plotly.subplots import make_subplots
```

## Define Graphing Function
```python
def make_graph(stock_data, revenue_data, stock):
    # Function implementation here
```

## Question 1: Extract Tesla Stock Data
```python
tesla = yf.Ticker("TSLA")
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)
tesla_data.head()
```

## Question 2: Extract Tesla Revenue Data
```python
url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, "html5lib")
tesla_revenue = pd.read_html(url, match="Tesla Quarterly Revenue", flavor='bs4')[0]
tesla_revenue = tesla_revenue.rename(columns={'Tesla Quarterly Revenue(Millions of US $)': 'Date', 'Tesla Quarterly Revenue(Millions of US $).1': 'Revenue'}, inplace=False)
tesla_revenue["Revenue"] = tesla_revenue["Revenue"].str.replace(",", "").str.replace("$", "")
tesla_revenue.dropna(inplace=True)
tesla_revenue.head()
```

## Question 3: Extract GameStop Stock Data
```python
gamestop = yf.Ticker("GME")
gme_data = gamestop.history(period="max")
gme_data.reset_index(inplace=True)
gme_data.head()
```

## Question 4: Extract GameStop Revenue Data
```python
url = "https://www.macrotrends.net/stocks/charts/GME/gamestop/revenue"
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, "html5lib")
gme_revenue = pd.read_html(url, match="GameStop Quarterly Revenue", flavor='bs4')[0]
gme_revenue = gme_revenue.rename(columns={'GameStop Quarterly Revenue(Millions of US $)': 'Date', 'GameStop Quarterly Revenue(Millions of US $).1': 'Revenue'}, inplace=False)
gme_revenue["Revenue"] = gme_revenue["Revenue"].str.replace(",", "").str.replace("$", "")
gme_revenue.dropna(inplace=True)
gme_revenue.tail()
```

## Question 5: Plot Tesla Stock Graph
```python
make_graph(tesla_data, tesla_revenue, 'Tesla Stock Data Graph')
```

## Question 6: Plot GameStop Stock Graph
```python
make_graph(gme_data, gme_revenue, 'GameStop Stock Data Graph')
```
```
