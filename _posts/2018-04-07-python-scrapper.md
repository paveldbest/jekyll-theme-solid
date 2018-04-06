---
layout: post
title: A simple python scrapper 
categories: Coding 
description: python scrapper,real estate
---

So this is a really simple python scrapper. It worked on the search result page of 
realestate.au ONLY. And at this state it can only pull data from one single page.
I am writing this article just to go through the code again. &nbsp;&nbsp;

The code is as follows :

```# -*- coding: utf-8 -*-
import requests
from urllib.request import urlopen
from bs4 import BeautifulSoup

## open the webpage using bs
def get_webpage(url):
	html_page = requests.get(url)

	if html_page.status_code != 200:
		print("invalid url, please check",html_page.status_code)
	else:
		return html_page.text ## why there is a text format webpage??	


site = 'https://www.realestate.com.au/rent/in-2033/list-1?source=location-search'
html = get_webpage(site)
soup = BeautifulSoup(html, "lxml")

#for containers in soup.find_all('listingInfo rui-clearfix'):
"""containers = soup.find("div",class_ = "listingInfo rui-clearfix")

address = containers.find("h2",class_ = "rui-truncate")
agentname = containers.p.get_text()

print(address.get_text(), price.get_text(), agentname)"""


for list in soup.find_all("div",class_ = "listingInfo rui-clearfix"):
	address = list.find("h2",class_ = "rui-truncate")
	price = list.find("p",class_ = "priceText")
	agentname = list.p.get_text()
	print (address.get_text(),price.get_text(),agentname,sep = ' | ')``` 


- First using beautifulsoup to parse the html page opened by requests
- Then find the tag that contains each property info, in my case it is under < class listingInfo rui-clearfix >
- Finally go through each property by find_all function and print

