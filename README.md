# Data Sources and SQL
Working with data is fun, but having access to quality and readily available data might sometimes be challenging. This article attempts to touch on few sources of data and how to store structured data.

### Data Sources
Data Scientist or Analyst often work in an environment where the organization has its own source of data for example, most retail companys store the data of their customers and busines transactions; these could be made availble to analyst when necessary. But in a situation where such is absent, the responsibility might lie on the analyst to source for data; ususally via the internet.

### Data Storage
Structured (tabular) data depending on their size could be stored in spreadsheet or relational database. Relational database could accommodate bigger data than  spreadsheet and they are relational because of their algorithm that allow interconnectivity among the tables.

### Web Scraping
Web scraping is the act of gatheing or collecting data from various websites. While some websites have heavy security around their data and prohibit unauthorized collection of them, others allow free scraping of thiers. It is responsible and ethical to check website rules before tampering with their data. For Data that are available in HTML(Hyper Text Markup Language) BeautifulSoup might be a good way to extract such data.

### Extracting HTML Tags with BautifulSoup
Tags in websites that are built in Hyper Text Markup Language (HTML) could be extracted with [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc) Tags could be accompany by some unwanted texts that could also be separate with  [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc). Below is a demonstration of how this could be achieved. We'll be using BeautifulSoup to access data from [Books to scrape](https://books.toscrape.com/)- a website that allows free collection of its data.


### Connect to a website 
First we need to import the library that will help us connect to the website the "urllib.request"
***Ensure that all libraries have been downloaded before import***

```
import urllib.request

def open_webpage(url):
  #print(urllip.request.urlopen(url))    # To ascertain the connection was successful
  return urllip.request.urlopen(url)

# Let's insert the url to test our function
open_webpage("https://books.toscrape.com/")
```

![successful connection]()

### Access HTML Elements with BeautifuSoup
Now, let's view the HTML elements with BeautifulSoup.
```
from bs4 import BeautifulSoup as bee

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

### Extracting HTML Tags
One of the tags that I will like to get is the anchor tag. It houses the catalogue link of books and their categories. But then, it also need to be separated from unwanted text. Let's combine [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigating-using-tag-names)  and python [Regular Expresion](https://docs.python.org/3/library/re.html) to extract what we need.

```
import re

def anchor_tag(tags):

"""
Get the anchor tag
View the anchor tag, optional
Extract the category link
Extract book category
Optional to view the list

"""
  tag = tags("a")       
  #print(tag)            
  anchor_tag_ind = tag[3:53]
  category_link = re.findall("<a.+category.+", str(anchor_tag_ind))   

  book_category = []

  for anchor in anchor_tag_ind:
    book_category.append((anchor.next_element).strip())

  #print(book_category)     

  # Get other needed tags and return all extracted tags
     
  book_price = re.findall('<p.+(£\\d{2}\\.\\d{2})',str(tags))
  ratings = re.findall(r'<p.+(star.+?)"', str(tags))
  title_catalogue = tag("h3")
  title =re.findall(r'title=(".+?)>', str(title_catalogue))

	title_links=[]

  for links in title_catalogue:
	title_links.extend(re.findall('<a.+\\.html', str(links)))
	
	
return category_link, book_category, title_links, title, book_price, ratings

# Test the function
anchor_tag(open_webpg_get_elements("https://books.toscrape.com/"))

```


### Save Data for Future Use
Now that we have our data ready, it can be saved in different ways for future use.

### Save Data as Comma Separated Value CSV 
For tha saving to be successfull, all data must be of equal length

```
import csv

def csv_data(data):
	data = (title_links, title, book_price, ratings)
	data_heading = ("catalogue_link", "price", "title", "ratings")

	title_list=[]
	for i in range(len(data)):
		dict_data = {data_heading[0]:data[0][i], data_heading[1]:data[1][i], data_heading:data[2][i],data_heading:data[3][i]}
		title_list.append(dict_data)
		
     with open("catalogue.csv", "w", newline='\n', encoding="utf-8") as csvfile:
	 writer = csv.DictWriter(csvfile, fieldnames=["catalogue_link", "price", "title", "ratings"])
 	 writer.writeheader()
 	 writer.writerows(title_list)

csv_data(open_webpage(anchor_tag(open_webpage(url)))

# 	 print(pd.read_csv("catalogue.csv"))  # i.e to check the saved data

"""
Using the Easier method: One can convert the data to a data frame and then
use .to_csv to save the data into csv format

"""

import pandas as pd

catalogue=pd.DataFrame({"catalogue_links":cata_links, "book_title":title, "book_price":book_price, "ratings":ratings})
catalogue.to_csv
# print(catalogue)

```

### Save Data in JSON Format

```
import json
def json_file(data):
	header = ["category_link", "category","catalogue_link", "price", "title", "ratings"]
	dict_json = {"category_link":category_link, "category":category_link, "catalogue_link":catalogue_link,"price":price, "title":title, "ratings":ratings}

	with open("catalogue.json", "w", encoding="utf-8") as json_catalogue:
 		json.dump(dict_json, json_catalogue, indent=3)
json_file(anchor_tag(open_webpage(url)))

#Check or open the file
with open("catalogue.json", "r") as bk:
 		books = json.load(bk)

```
### Save Data in Database using SQL

Here, I will be using SQLite

def save_to_database():


***To be continued***
