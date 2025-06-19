# Data Sources and SQL
Working with data is fun, but having access to quality and readily available data might sometimes be challenging. This article attempts to touch on few sources of data and how to store structured data.

### Data Sources
Data Scientist or Analyst often work in an environment where the organization has its own source of data for example, most retail companys store the data of their customers and busines transactions; these could be made availble to analyst when necessary. But in a situation where such is absent, the responsibility might lie on the analyst to source for data; ususally via the internet.

### Data Storage
Structured (tabular) data depending on their size could be stored in spreadsheet, relational databases. Relational databases could accommodate bigger data than  spreadsheet and they are relational because of their algorithm that allow interconnectivity among the table.

### Web Scraping
Web scraping is the act of gatheing or collecting data from various websites. While some websites have heavy security around their data and prohibit unauthorized collection of them, others allow free scraping of thiers. It is responsible and ethical to check website rules before tampering with their data. For Data that are available in HTML(Hyper Text Markup Language) or JavaScript format, BeautifulSoup and or Selenium might be a good way to extract such data. But some websites that render their available data in a semi organized formt- json; could be accessed with provided API-key. 

### Sourcing HTML Data with BautifulSoup
Websites built with HTML usually have some dirts that could easily be separated from the needed data with [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc). Below is a demonstration on how this could be achieved. We'll be using BeautifulSoup to access data from [Books to scrape](https://books.toscrape.com/)- a website that allows free collection of its data.


### Connect to a website 
First we need to import an important library that will help us connect to the website the "urllib.request"
***Ensure that all libraries have been downloaded before import***
```
import urllib.request

def open_webpage(url):
  print(urllip.request.urlopen(url))    # To ascertain the connection was successful
  return urllip.request.urlopen(url)

# Let's insert the url to test our function
open_webpage("https://books.toscrape.com/")
```

![successful connection]()

### Access HTML Elements with BeautifuSoup
Now, let's view the HTML elements with BeautifulSoup.
```
import from bs4 import BeautifulSoup as bee

def get_elements(elements):
  print(bee(elements, "url.parser"))    # To view the elements 
  return bee(elements, "url.parser")

# Ready to test our function
get_elements(open_webpage("https://books.toscrape.com/"))
```
***Function Execution: For "get_elements()" to work, it has to first process "open_webpage()"; hence, "get_elements(open_webpage("https://books.toscrape.com/"))"***


***Let's combine both functions into one for readability***
```
import urllib.request
from bs4 import BautifulSoup

def open_webpg_get_elements(url):
  elements = bee(url.requests.url.open(url), "html.parser")
  print(elements)
  return elements

# Let's test our function and print some texts
open_webpg_get_elements("https://books.toscrape.com/")

```
![page]()
**A Glimpse of the printed page**
The printed data has a lot of tags with both wanted and unwanted texts

### HTML Tags
One of the tags that I will like to get is the anchor tag. It houses the catalogue link of books and their category. But then, it also need to be separated from unwanted text. This extraction could be done using [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigating-using-tag-names) but I will use python [Regular Expresion](https://docs.python.org/3/library/re.html) to extract what I need.

```
import re

def anchor_tag(tags):
  tag = tags("a")       # Get the anchor tag
  #print(tag)            # View the anchor tag, optional
  category_link = re.findall("<a.+category.+", str(tags))  # Extract the category link

  category_link_list = []
  book_category = []

  for cat in category_link:
    category_link_list.append(cat)
    book_category.extend(re.findall("<.+books/(.+)/", str(cats))      # Extract book category

# Now that the data is clean and ready, we can create panda's dataframe for direct analysis,
# we can save it as a json, csv, excel file or store it in database.file, 

import pandas as pd

book_category = pd.DataFrame({"book_category_link":category_link_list[1:], "category":book_category})    # The 1st link in the list is not needed hence, the index

#print(book_category)       # To view the table, optional
return book_category

# Test the function
anchor_tag(open_webpg_get_elements("https://books.toscrape.com/"))

```


![category link table]() 




