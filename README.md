# Data Scraping Project
## Scraping data from bookstoscrape.com


## Table of Content 
- [Project Overview](#project_overview)
- [Data Sources](#data_sources)
- [Tools Used](#tools_used)
- [Data Cleaning/Preparation](#data_cleaning/preparation)
- [Exploratory Data Analysis](#exploratory_data_analysis)
- [Data Analysis](#data_analysis)
- [Results/Findings](#results/findings)
- [Recommendations](#recommendations)
### Project Overview
This Data Analysis project aims to scrape information about the books from bookstoscrape.com website.


### Data Sources
The major source of information for this project is bookstoscrape.com website

### Tools Used
- Python - Used for Data Scraping
- Microsoft Excel - used for Data cleaning aand storage.

### Data Cleaning/Preparation



### Exploratory Data Analysis


### Data Scraping


```python
from bs4 import BeautifulSoup
import requests
import pandas as pd

# title, price, availability, rating, category
books = []

for i in range(1,51):
    url = f"http://books.toscrape.com/catalogue/page-{i}.html"
    request = requests.get(url)
    request = request.content
    soup = BeautifulSoup(request, 'html.parser')
    ol = soup.find('ol')
    article = ol.find_all('article', class_='product_pod')

for x in article:
  image = x.find('img')
  title = image.attrs['alt']
  price = x.find('p', class_ = 'price_color').text[1:]
  price = float(price)
  availability = x.find('p', class_ = 'instock availability').text[15:-6].strip()
  rating = x.find('p', class_ = 'star-rating')['class'][1]
  books.append([title, price, availability, rating])

df = pd.DataFrame(books, columns = ['Title', 'Price', 'Availability', 'Rating'])
df

df.to_csv('books.csv')
```

### Results/Findings
![image](https://github.com/VicOdum/book_to_scrape_proj/assets/158152192/ed0ebb58-a8cc-4515-a010-0c23555db122)


### Recommendations

### Limitations
- This was just a data scraping project, however, there would be need for further data cleaning which is beyond the scope of this project.

### References
