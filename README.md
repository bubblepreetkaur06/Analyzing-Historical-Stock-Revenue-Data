# Analyzing-Historical-Stock-Revenue-Data

```python
!pip install yfinance==0.1.67
!mamba install bs4==4.10.0 -y
!pip install nbformat==4.2.0
```

```python
import yfinance as yf
import pandas as pd
import requests
from bs4 import BeautifulSoup
import plotly.graph_objects as go
from plotly.subplots import make_subplots
```
```python
import yfinance as yf
tesla=yf.Ticker("TSLA")
tesla_data=tesla.history(period="max")
tesla_data.reset_index(inplace=True)
tesla_data.head(5)
```
```python
url="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm"
html_data=requests.get(url).content
soup=BeautifulSoup(html_data,'html.parser')
tesla_data=pd.read_html(url)
tesla_revenue=tesla_data[1]
tesla_revenue.rename(columns={'Tesla Quarterly Revenue (Millions of US $)':'Date','Tesla Quarterly Revenue (Millions of US $).1':'Revenue'},inplace=True)
tesla_revenue["Revenue"] = tesla_revenue['Revenue'].str.replace('$',"")
tesla_revenue["Revenue"] = tesla_revenue['Revenue'].str.replace(',',"")
tesla_revenue.dropna(inplace=True)
tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
tesla_revenue.tail(5)
```
```python
gamestop=yf.Ticker("GME")
gme_data=gamestop.history(period="max")
gme_data.reset_index(inplace=True)
gme_data.head(5)
```

```python
url1="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"
html_data1=requests.get(url1).content
soup1=BeautifulSoup(html_data,'html.parser')
read_html_Data=pd.read_html(url1)
gme_revenue=read_html_Data[1]
gme_revenue.rename(columns={'GameStop Quarterly Revenue (Millions of US $)':'Date','GameStop Quarterly Revenue (Millions of US $).1':'Revenue'},inplace=True)
gme_revenue["Revenue"] = gme_revenue['Revenue'].str.replace('$',"")
gme_revenue["Revenue"] = gme_revenue['Revenue'].str.replace(',',"")
gme_revenue.tail(5)
```
