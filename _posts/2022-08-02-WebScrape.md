---
layout: post
title:  "Scraping Central Utah's Rock Climbing Routes"
date:   2022-10-20
author: Alek Bacon
description: Scraping Central Utah's Rock Climbing Routes with Beautiful Soup
image: /assets/images/climb.jpg
---
I love rock climbing. I go, on average, 4-5 times a week. Although you may not be aware - unless you yourself are an avid climber - Utah is a top-tier location for outdoor rock climbing. Central Utah alone boasts 801 rock routes (not including Boulders, Ice, Aid, or Mixed) logged at the [Mountain Project.](https://www.mountainproject.com/) <br>

I'd like to take a look at some of the most popular routes in the area and see if we notice any interesting trends. We could go ahead and scrape every climb in Central Utah, or even every climb in the entirety of Utah, but I decided to filter the routes a bit to climbs that I would likely be more interested in. I'm going to reduce it to "rock" routes (Trad, Sport, or Toprope) in Central Utah, with a rating (difficulty) between 5.6 and 5.12a/b with at least 0 stars (community rating). This filtering still leaves 623 climbs. The website itself defaults to sorting first by popularity, and then by difficulty. With this filter, I'm going to pull the top 200 routes. 

The data on this site is not meant to be private. You may notice after filtering routes, they have a "Export CSV" link available. This provides similar information to what we will be scraping, but it has additional columns we don't need, and it is missing at least 1 column that we would like to include.
![image](https://user-images.githubusercontent.com/112503027/197302554-f4d4740d-69a7-49ae-94f1-b11e35c9d9f3.png)

The entirety of this scrape was done in Python using [requests](https://pypi.org/project/requests/) and [Beautiful Soup.](https://pypi.org/project/beautifulsoup4/) <br>

The website is arranged such that each route has its own page. So our initial scrape will be to go though all of the links on the page and sorting out the ones to the routes. 
### Pull all of the links from the page
![image](https://user-images.githubusercontent.com/112503027/197300925-913c70bb-28ec-494c-a78b-12d35d5a6e01.png) <br>
After looking through the links, I noticed all the links to the routes started with the same set of characters
### Filter the links
![image](https://user-images.githubusercontent.com/112503027/197301146-611b6607-b462-4deb-93a1-c217a81cf286.png) <br>

Now for each link we need to go through and find exactly where the data is that we want to scrape using the [inspect tool.](https://www.thoughtco.com/get-inspect-element-tool-for-browser-756549) Here, for example, we find the division that contains the type of climb (Sport), the length of the climb (105ft) and the first ascenders name (Boone Speed).
![image](https://user-images.githubusercontent.com/112503027/197303137-c6c6cb84-45c5-409e-9f3d-a50947087c29.png) <br>
To pull all of the text from this section we can use the following code. <br> ![image](https://user-images.githubusercontent.com/112503027/197303344-3826bbbd-1608-49bc-90fc-133223f89d7d.png) <br>
Of the 200 climbs that we pulled from, the code did not work completely for 3 of the climbs. We could alter our loop, trying to correct these small anomalies, but with only 3 of the 200 causing problems, I just manually corrected them. I would not recommend manual changes for more than a few rows of data. It is obviously better practice to have the main loop catch and correct exceptions that could be found. <br>
![image](https://user-images.githubusercontent.com/112503027/197304245-63f999e5-c5ed-48a3-89f3-b02fa633cb9f.png) <br>

I'm really curious where this will lead. In my next post we will explore this data together. Are higher grades or lower grades more popular? How strongly are popularity and rating correlated? What length of routes have the highest ratings? Hopefully we can find answers to these questions. We may even find interesting trends where we didn't expect! <br>
Link to the [GitHub repository.](https://github.com/Bacon-A/Web-Scrape) <br>
