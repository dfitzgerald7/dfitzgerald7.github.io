---
layout: post
title:      "TopSongs: Project 1"
date:       2018-10-19 15:13:51 +0000
permalink:  topsongs_project_1
---


For our first project, I wanted to scrape the Billboard 100 website and print the top songs of each chart. The cli would list all of the charts, and the the user would enter a chart name to list all of the songs, albums, or artists. 
The most challenging aspects of this project were scraping the html and deciding how to store the scraped data. There were two levels to the scraping. The main web page is https://www.billboard.com/charts. There are 15 total charts but two different html formats. The top 3 , Hot 100, Artist 100, and Billboard 200, are formatted differently than the bottom 12 charts. For each chart, I scraped the chart name and also the reference url to the actual chart. At this level, the top song is formatted differently from the rest, so that had to be scraped by itself. For the rest of the chart, all the relevant items for each song were attributes to "div.chart-list-item". 
All of the scraped data was stored in one of two objects, a chart or a list_item. The chart has a name and a reference url, and also can print all of the list_items that belong to that chart instance. A chart has many list_items. The list_items class contains a name, artist, and rank.  There is also a boolean as to whether the list contains songs. Two of the charts only contain artsits, so they must be printed differently.  
First, many chart objects are created by scraping the main web page. Then, each chart object is used to find and scrape the associated list. The list is scraped to create many objects that all belong to the original chart object. 
Finally, the cli class is what is run in the bin file. It calls the scraper methods and stores all the relevant data. Then prints all the chart commands and waits for user input. The user can then decide how many songs they would like to see. Since the scraped chart names are mostly long, there is also a cli class constant hash that contains the shorter commands that point to the long chart names. This makes inputting easier for the user. 
