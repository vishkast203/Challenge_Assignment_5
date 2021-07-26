# Challenge_Assignment_5
Savings &amp; Retirement Financial Planner Assignment-5
Executive Summary:
The objective of this project was to evaluate two financial planning tools using a single Jupyter notebook, Part-1. evaluated a financial plabnner for emergencies and Part-2 evaluated a financial planner for emergencies. 
The results of the evaluation of Part-1 showed that members had sufficient funds for an emergency. The results for Part-2 showed that a 60:40 split between stocks/bonds to Crypto currencies was a favorable approach and deserved further evaluation through addtional more detailed simulation runs.

Program steps follwed:
Both Parts-1 & 2 were evaluated using Python Version 3.8 and in tandem with Jupyter Notebook run via the vscode platorm. The initial files provided consisted of a .env file that allowed upload of the API keys to access the online databases containing the stock data, a MCForecasttools.py file that containesd the code to run Monte Carlo Simulations and evaluate the results.  The programmer created a remote repository in Github.com to allow management to track the progress of the project as the code was developed.
PART-1:The initial steps required the import of the following libraries and dependencies:
    import os
    import requests
    import json
    import pandas as pd
    from dotenv import load_dotenv
    import alpaca_trade_api as tradeapi
    from MCForecastTools import MCSimulation
    %matplotlib inline
Next the .env file  with the current portfolio status (# of coins & monthly income) were set as per instructions. The json files for the the crypto currencies (BTC & ETH) were pulled by making API calls to the FreeCrypto daata site. The current values for the two crypto currencies were extracted from the json dictionary dump files and the total value of the crypto holdings withn the portfolio was calculated. 
The next step was to determine the value of the  Stocks & Bonds within the portfolio. The first step was to access the ALPACA database using the ALPACA keys & the ALPACA secret key to access the database previously loaded into the .env file. Then the GET function was used to pull the prices for tickers = ["SPY", "AGG"]. Next step was to create the REST object and pass it the  ALPACA API Key & the Secret Key using the current API version 2 of the Alpaca program to allow authentication of the user. The closing prices for the two stocks were verified and the portfolio value was established (Price x quantity) for the date of 07/08/2020.  Finally the total portfolio value was established taking the sum of the Stocks & the Crypto accounts ($ 119,917.37). 
Next this portfolio value was assessed against the minimum cut-off for the Emergency fund (3 x Monthly Income $36,000). The first step was to create a dataframe (& a subsequent Pie Chart)for the portfolio as follows:
	         amount
crypto	     59227.867
stock/bond	 60689.500 

Next  "if - else" statements were used to provide the user with status of accounts with respect to meeting the minimum requirements for fund sufficeincy. It was determined that there was suffcuent funds for an emergency. 

PART-2 Analysis
This part of the project required that a Financial Planner for retirement be created such that portfolio weightitngs can be changed, simuated into the future to forecast portfolio performance. 
Again the Alpaca web site was accessed using the Alpaca API keys using a 3-year timeframe July 2017 - 2020) & using the "alpaca.get_barset" function.  The dataframe was checked and used as a basis for a (30 year, 60:40 split, (Stocks to Bonds) Monte Carlo simulation as follows:
    MC_60_40_30YR = MCSimulation(
     portfolio_data = prices_df,
     weights = [.60,.40],
     num_simulation = 500,
     num_trading_days = 252*30
     )
After 500 simulations the resukts were plotted in as a line plot  as a Histogram. The sumamry statistics were extracted using the "summarize_cumulative_return()" function and the impact of the Lower & Upper CI's on the portfolio values were determined. Based on this simulation run it was determined that a 60:40 weight in Stocks to Bonds over a 30 year period would result in a maximum values of $996,235 & a minimum value of $146,640. 
A second simulation was run iver a 10 year timeframe with a portlio containing 80% weighting in Stocks & the rest in Bonds. The resukts of this second simulation (500 trials) showed unfavorable results versus the first run. The minimum reduction in portfolio value was $72,000 & the maximum possible reduction in value was $480,000 over a 10 year period. 
The results of these simulation runs show that the program is robust and can be utilized to simulate any portfolio make-up across several time frames. While stock & Crytpo values can vary significantly some of the additional ways that the program can be used to reduce uncertainity are as follows:
1. Create a dataframe to use as a basis for the simulation that retrives data over longer periods when available.  This improves the validity of the forecast period assuming all other factors are kept equal (Economic, Inflation, Interest Rates, Socio-Political)

2. Additonal sensitivities should be run for differeing portfolio weightings to improve our understaning the base data

3. 500 trials may not be sufficient to get better forecasts, at least a higher numn=ber of trials shoud be run per simulation to validate the results of each run.


