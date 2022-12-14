- š Hello, welcome to my repo and portfolio!
- š· I'm Anthony De Faria, an engineer and data scientist.
- š Iām passionate about [photography](https://www.anthonydefaria.com), travel and motorbikes.
- šŖ I'll show you here the extent of my skills in data science through a use case project.

# šļø Project#1: French second-hand motorcycle market vizualisation dashboard and price prediction.

## š” Introduction

The main project that you can find here is the **French second-hand motorcycle market vizualisation dashboard and price prediction.**
The objective is to predict the price of new motorbike ads and detect good deals š¤!

### How does it works?

The project is separated into several microservices:

- **Data gathering**: pre configured robots (also know as spiders) are scraping 11 websites twice a day to gather market data.
- **Data cleaning**: raw data from scraping is cleaned and prepared for vizualisation and machine learning.
- **Data storing**: data is stored in a self hosted postgres database.
- **Data vizualisation**: data can be visualized through an interactive dashboard to monitor spiders and understand market trends.
- **Traine (in progress)r**: data is used to train a machine learning model to predict the price.
- **Rest API (in progress)**: query the price prediction from anywhere you need it!

## š Micoservices detailed

### š Gathering data with scraping (private repo)

[bike-price](https://github.com/AnthonyDF/bike_price) is a private repo with all my spiders ready to scrap the internet. It's a top secret repo but I can at least detail the strategy (keep it for yourself šµļø). I use the famous [scrapy](https://fr.wikipedia.org/wiki/Scrapy) framework to configure and run my spiders š·ļø. They are clever and will never scrap twice the same url thanks to a fine tuned middleware. They have a special digestion pipeline to format the data and send it to a postgresql database. They are hosted on a scalable virtual machine aka Digitalocean [droplet](https://www.digitalocean.com/products/droplets) š§. They are dedicated workers, they wake up early, they go to bed very late and will always listen to what they are asked to do by the **cron**. Sometimes the task can be tricky. Itās the case for javascript based websites. They are smart enough to run a scriptable web browser called [splash](https://github.com/scrapinghub/splash) to help them to scrap the data. Thanks to continuous development they are super easy to deploy even after a small modification. Pushing on the master branch will trigger github actions to pull modifications on the droplet via ssh and then bluid containers with [docker](https://www.docker.com/) compose š.

### š§¹ Cleaning and transforming data

 Raw data is like an unpolished diamond. It needs some work to be done to prepare the data before vizualisation and machine learning. 
 [bike-price-cleaner](https://github.com/AnthonyDF/bike-price-cleaner) is a service that will automatically clean and prepare the data after each scraping session as detailed below.

1. Remove data out of physical and acceptable range.
2. Dropping duplicates (Vendors tend to post the same ad on mutiple websites).
3. Standardization of brand names and categories with advanced technique of fuzzy matching. Generaly speaking, the brand and model is a free text input.

### š» Storing data

The data is stored in a **postgresql** database. 

### š Vizualise spiders heart beats and market trends

[bike-price-dashboard](https://github.com/AnthonyDF/bike-price-dashboard) is an [interactive dashboard](http://188.166.201.70:8080/) with [Dash plotly](https://plotly.com/dash/) (be patient, it can takes a few secs to load). It allows to visualize spiders workload and scraping anomalies. You will also be able to dive into the second hand market stats and history, very handy if you look for a bike at the best price.

### šØāš« Machine learning training (In progress)

### Coming soon:
- Implementation of Celery and Redis to improve the UX
- Standardization of bike model names with fuzzy matching
- Deployement of an ExtraTreesRegressor model to predict the price
- Check for PCA integration
