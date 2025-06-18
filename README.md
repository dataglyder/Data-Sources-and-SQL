# Data Sources and SQL
Working with data is fun, but having access to a quality and readily available data might sometimes be challenging. This article attempts to touch on some of the various sources of data and how to store structured data.

### Data Sources
Data Scientist or Analyst often work in an environment where the organization has its own source of data for example, most retail companys store the data of their customers and busines transactions; these could be made availble to analyst when necessary. But in a situation where such is absent, the responsibility might lie on the analyst to source for data; ususally via the websites that allows such.

### Data Storage
Structured (tabular) data depending on their size could be stored in spreadsheet, relational databases. Relational databases could accommodate bigger data than  spreadsheet and they are relational because of their algorithm that allow interconnectivity among the table.

### Web Scraping
Web scraping is the act of gatheing or collecting data from various websites. While some websites have heavy security around their data and prohibit unauthorized collection of them, others allow free scraping of thiers. It is responsible and ethical to check website rules before tampering with their data. For Data that are available in HTML or JavaScript format, BeautifulSoup and or Selenium might be a good way to extract such data. But some websites that render their available data in a semi organized formt- json; could be accessed with provided API-key. 

### Sourcing HTML Data with BautifulSoup
Websites built with HTML usually have some dirts that could easily be separated from the needed data with [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc). Below is a demonstration on how this could be achieved. We'll be using BeautifulSoup to access data from [Books to scrape](https://books.toscrape.com/)- a website that allows free collection of its data.


### Connect to a website 
First we need to import an important library that will help us connect to the website the "urllib.requests"
***Ensure that all libraries have been downloaded before import***

![Connect to the website]()

### Access HTML Elements with BeautifuSoup

![Access Elements]()

***Let's combine both functions into one***

![combined_func]()

#### A Glimpse of the printed page
The printed data has a lot of tags with both wanted and unwanted texts

![page]()

### HTML Tags
One of the tags that I will like to get is the anchor tag. It houses the catalogue link of books and their category. But then, it aslso need to be separated from unwanted text. This extraction could be done using [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigating-using-tag-names)

![anchor tag]()


