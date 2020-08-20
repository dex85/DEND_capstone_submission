# Capstone Project
## Data Lake with Apache Spark for daily Market Data and Indicators
### Introduction
The Final Project idea is, to gather Stock market data and load the data into parquet files using Apacha Spark with Python. Initially the Project was implemented in AWS using several EC2 instances for a Jupyter Notebook but due to an incident (forgot to turn off the instances, only closed the notebook) I decided to run everything on my local machine.
For one, the stock market data of the top 3 Stock Markets (New York Stock Exchange, NASDAQ, Tokyo Stock Exchange) where downloaded into JSON files from marketstack.com using its VIP API. For the second seven currency pairs where downloaded from https://eaforexacademy.com/software/forex-historical-data/ as CSV files.
Using the data, the ETL pipeline was implemented to build a basic data model. The data model can easily extended with more indicators as explained in the notebook.

### Data Model
#### Fact Table - Asset Data
- ticker_id - Number that represents the Stock or Currency or any other asset that might be added
- symbol - the symbol of the stock
- timestamp - the timestamp
- sma - the sma price
- price - the close price
#### Dimension Tables
##### symbol table
- ticker_id - Number that represents the Stock or Currency or any other asset that might be added
- symbol - the symbol of the stock
- exchange - the exchange where the stock is listed
##### price table
- ticker_id - Integer value of the stock
- timestamp - Long Integer value of the date
- high - Double of the highest value at that date
- low - Double of the lowest value at that date
- open - Double value of the open price at that date
- close - Double value of the close price at that date
- return - the return based on the close price

##### SMA table
- timestamp - the timestamp
- ticker_id - 
- sma_interval - 
- price - the weighted close price

### Questions
#### How often should the data be updated?
That depends on the user preference. Given that the data is daily data and a hypothetical protfolio of 10 assets with a monthly adjustment of the portfolio based on volatility prediction, once a week is sufficient. Could be fully automated with a spark job and publicly available market data given the short interval.
#### The data was increased by 100x
The cool thing about spark is, if someone needs more processing power it can be simply added. So in layman terms, buy more hardware and add spark clients. Also, as done in the preject, data could be processed in batches.
#### The data populates a dashboard that must be updated on a daily basis by 7am every day.
Implement a Cronjob / Cron tab or custom made (python) scripts that do the scheduled updates.
#### The database needed to be accessed by 100+ people.
If the data simply needs to be accessed, so read by many people, the configuration of Spark can be adjusted and if necessary add more hardware.
