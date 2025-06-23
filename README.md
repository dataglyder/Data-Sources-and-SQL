# Data Sources and SQL
Working with data is fun, but having access to quality and readily available data might sometimes be challenging. This article attempts to touch on few sources of data and how to store structured data.

### Data Sources
Data Scientist or Analyst often work in an environment where the organization has its own source of data for example, most retail companys store the data of their customers and busines transactions; these could be made availble to analyst when necessary. But in a situation where such is absent, the responsibility might lie on the analyst to source for data; ususally via the internet.

### Data Storage
Structured (tabular) data depending on their size could be stored in spreadsheet or relational database. Relational database could accommodate bigger data than  spreadsheet and they are relational because of their algorithm that allow interconnectivity among the table.

### Web Scraping
Web scraping is the act of gatheing or collecting data from various websites. While some websites have heavy security around their data and prohibit unauthorized collection of them, others allow free scraping of thiers. It is responsible and ethical to check website rules before tampering with their data. For Data that are available in HTML(Hyper Text Markup Language) BeautifulSoup might be a good way to extract such data.

### Extracting HTML Tags with BautifulSoup
Tags in websites that are built in Hyper Text Markup Language (HTML) could sometimes be acompany with unwanted texts; these tags could be separated with  [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc). Below is a demonstration of how this could be achieved. We'll be using BeautifulSoup to access data from [Books to scrape](https://books.toscrape.com/)- a website that allows free collection of its data.


### Connect to a website 
First we need to import the library that will help us connect to the website the "urllib.request"
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
One of the tags that I will like to get is the anchor tag. It houses the catalogue link of books and their categories. But then, it also need to be separated from unwanted text. Let's combine [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigating-using-tag-names)  and python [Regular Expresion](https://docs.python.org/3/library/re.html) to extract what we need.

```
import re

def anchor_tag(tags):
  tag = tags("a")       # Get the anchor tag
  #print(tag)            # View the anchor tag, optional
  anchor_tag_ind = tag[3:53]
  category_link = re.findall("<a.+category.+", str(anchor_tag_ind))   # Extract the category link

  book_category = []

  for anchor in anchor_tag_ind:
    book_category.append((anchor.next_element).strip())      # Extract book category 


#print(book_category)       # Optional to view the list
return category_link, book_category

# Test the function
anchor_tag(open_webpg_get_elements("https://books.toscrape.com/"))

```
Let's extract other necessary tags


```
def other_tags(others):
  book_price = re.findall('<p.+(£\\d{2}\\.\\d{2})',str(others))
	ratings = re.findall(r'<p.+(star.+?)"', str(others))
	title_catalogue = others("h3")
  title =re.findall(r'title=(".+?)>', str(title_catalogue))

	title_links=[]

  for links in title_catalogue:
	title_links.extend(re.findall('<a.+\\.html', str(links)))
	#print(title_links,title, book_price, ratings)
	return (title_links,title, book_price, ratings)

other_tags(open_webpg_and_access_elements("https://books.toscrape.com/"))
```

![category link table]()

### Save Data for future use
Now that we have our data ready, it can be saved in different ways for future use.

```
def save_data(data):


```




***To be continued***
