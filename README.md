# Readme for Bitcoin Price Prediction Project with ARIMA, XGBoost and LSTM
### Bootcamp Data Science PRO - Kodołamacz - DS 11/09/2021


This notebook contains sections as below:

1. Abstract
2. Notebook introduction
3. Data description
4. Gathering data
5. Data preprocessing
6. ARIMA Model
   - 6.1. ARIMA Model  =>  complete data + ln(data)
   - 6.2. ARIMA Model  =>  complete data + without ln(data)
   - 6.3. ARIMA Model  =>  data start from 2018-01-01 + ln(data)
   - 6.4. ARIMA Model  =>  data start from 2021-01-01 + ln(data)
   - 6.5. ARIMA Model  =>  summary
7. XGBoost
   - 7.1. XGBRegressor  =>  data start from 2018-01-01
   - 7.2. XGBRegressor  =>  data start from 2021-01-01
   - 7.3. XGBRegressor  =>  summary
8. LSTM Model
   - 8.1. LSTM  =>  data start from 2018-01-01
   - 8.2. LSTM  =>  data start from 2021-01-01
   - 8.3. LSTM  =>  summary
9. Notebook summary


## 1. Abstract

Bitcoin is a cryptocurrency, created in 2009. Bitcoin system is a set of decentralized nodes with the bitcoin code, that contains collection of transactions. A blockchain is a distributed database that is shared among the nodes of a computer network. As a database, a blockchain stores information in digital format. All the computers running the blockchain has the same list of blocks and transactions, and can see all these new blocks being filled with new bitcoin transactions.

The original purpose of Bitcoin (BTC in short) is to allow two people to exchange value directly (using peer-to-peer technology), without centralbanks or goverments, regardless where they are. What this means is that Bitcoin blockchain is decentralized -  there is no centralized controll on this network.

Responsibility for processing transactions on the blockchain is done by - so called - Miners. "Mining" is performed using sophisticated hardware that solves an extremely complex math problem. The first computer to find the solution to the problem receives the next block of bitcoins, and the process begins again. A newly mined block of bitcoins now can be used to store a value or be sold.

The amount of bitcoins is predetermined. Each and every Bitcoin had to be mined previously. For every four years, the amount of bitcoins that can be mined, decreeses by half. That is so called halving of Bitcoin. The next halving will be in 2024, and means that miners will receive half of current revard for processing transactions.

Decentralization, predetermined amount of the cryptocurrency and current dificulty of gaining new Bitcoins by miners, is the reason why Bitcoin is so popular. Some people even call it a "digital gold". Popularity of Bitcoin makes the bitcoin market very volatile, that is much higher compared to traditional currencies. Volatile marcet, may be an opportunity for speculation and other advantages of bitcoin, may lead to long term, store of value strategy.

Popularity of bitcoin has led invest founds to gain digitall assets in their wallets. This may disturb Bitcoin, four years halving cycles.

Predicting Bitcoin price based on historical data should be accounted for by the prism of marcet sentiment, current bitcoin phase and movement of large capital from invest founds and current big holders. In General - DO NOT USE THIS NOTEBOOK FOR INVESTING.


## 2. Notebook introduction

This notebook was created to predict the Bitcoin price (in USD) using the ARIMA, XGBoost and LSTM models.
Each model used a different range of data to generate forecasts. Each model also requires a different approach to the dataset.
The mean square error (RMSE) was used to evaluate the performance of the model - it should be as low as possible.

The data variants (ranges) used to train the models are the main difference between the results of a given model. Reason for that is to show how the training results and plotting, varies from other variants and estimate the best approach for the data, that is time series.

Another difference is the optimization of the parameters. Auto_ARIMA was used for ARIMA, GridSearchCV was used for XGBoost, and the variants of the LSTM model contain the same parameters that have been empirically optimized.

The forecast is within the range of the test data, there is no "walk-forward" approach in this notebook.

Training data is the first 80% of the dataset and the rest is in the test datasets.

At the end of the notebook, a summary of the task is presented along with a graph of the RMSE results of the models.


## 3. Data description

Historical data price has been taken from Coinpaprika API Python Client.
- Web Site - https://coinpaprika.com/waluta/btc-bitcoin/
- Github   - https://github.com/s0h3ck/coinpaprika-api-python-client

Coinpaprika is a popular data source for various cryptocurrencies, with Polish origins based in city of Poznań.
Free Coinpaprika API provides data in JSON, and has limitation for amount of data per request. For example maximum of 50 tweets or historical data for at most 365 days at one request.
Examples of use can be found in their Github site.