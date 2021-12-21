# Challenge_4

The goal of this project is to evaluate four new investment options so as to determine the fund with the most investment potential based on key risk-management metrics: the daily returns, standard deviations, Sharpe ratios, and betas.

## Technologies

<img width="388" alt="Import" src="https://user-images.githubusercontent.com/94569323/146983218-847bee22-04fc-4792-8111-44aa312a99d2.png">
**Note(see above):** After importing these required technologies and following the steps below, the program should be capable of functioning properly.

## Installation Guide

Read in the CSV file called "whale_navs.csv" using the Path module. Set the index to the column "date", set the parse_dates and infer_datetime_format parameters.

~~~
csvpath = Path("Resources/whale_navs.csv")
whale_df = pd.read_csv((csvpath),
    index_col = "date",
    parse_dates=True,
    infer_datetime_format=True)
~~~

Use the Pandas pct_change function together with dropna to create the daily returns DataFrame. Base this DataFrame on the NAV prices of the four portfolios and on the closing price of the S&P 500 Index.

~~~
daily_returns = whale_df.pct_change().dropna()
~~~

## Usage

### Analyze the Performance

1. Use the default Pandas plot function to visualize the daily return data of the four fund portfolios and the S&P 500.

~~~
daily_returns[['SOROS FUND MANAGEMENT LLC']].plot(legend = True, figsize=(15, 8), title="Daily Return")
~~~
**Note(see above):** This allows the user to plot a specific column from the dataframe.

<img width="661" alt="Plot_1" src="https://user-images.githubusercontent.com/94569323/146983554-2088ad3d-a95a-46d5-90cc-914601765a62.png">

~~~
daily_returns.plot(legend = True, figsize=(15, 8), title="Daily Return")
~~~
**Note(see above):** This allows the user to plot all of the data from the dataframe.

<img width="662" alt="Plot_2" src="https://user-images.githubusercontent.com/94569323/146983603-89ca87dc-eec2-4bdc-a1e9-666bc96336c5.png">

2. Use the Pandas cumprod function to calculate the cumulative returns for the four fund portfolios and the S&P 500.

~~~
cumulative_returns = (1 + daily_returns).cumprod() - 1
~~~
**Note(see above):** This calculates the cumulative returns of the 4 fund portfolios and the S&P 500.

3. Use the default Pandas plot to visualize the cumulative return values for the four funds and the S&P 500 over time.

~~~
cumulative_returns[['SOROS FUND MANAGEMENT LLC']].plot(figsize=(15, 8), title="Cumulative Return", color="blue")
~~~
**Note(see above):** This allows the user to plot a specific column from the dataframe.

<img width="663" alt="Plot_3" src="https://user-images.githubusercontent.com/94569323/146983692-54c59c9f-404f-4dea-a94c-63f9b58a71a1.png">

~~~
ax = cumulative_returns['SOROS FUND MANAGEMENT LLC'].plot(legend = True, figsize=(15, 8), title="Cumulative Return")
cumulative_returns['PAULSON & CO.INC.'].plot(ax=ax)
cumulative_returns['TIGER GLOBAL MANAGEMENT LLC'].plot(ax=ax)
cumulative_returns['BERKSHIRE HATHAWAY INC'].plot(ax=ax)
cumulative_returns['S&P 500'].plot(ax=ax)

ax.legend(['SOROS FUND MANAGEMENT LLC', 'PAULSON & CO.INC.', 'TIGER GLOBAL MANAGEMENT LLC', 'BERKSHIRE HATHAWAY INC', 'S&P 500'])
~~~
**Note(see above):** This allows the user to plot all of the data from the dataframe.

~~~
cumulative_returns.plot(legend = True, figsize=(15, 8), title="Cumulative Return")
~~~
**Note(see above):** This allows the user to plot all of the data from the dataframe, therefore it is capable of providing the same results as the previous code.

<img width="664" alt="Plot_4" src="https://user-images.githubusercontent.com/94569323/146983768-bd88c144-e3ad-4945-ae10-928dca2b1ac4.png">

4. Answer the following question: 

**Question: Based on the cumulative return data and the visualization, do any of the four fund portfolios outperform the S&P 500 Index?**

Answer: Based on the cumulative return data and the visualizations, it is apparent that none of the fund portfolios in question outperform the S&P 500 Index. However, based on the overlay plot of the cumulative data, it is clear that during short periods in the past (specifically towards the end of 2015 and the beginning of 2016) all of the fund portfolios briefly outperformed the S&P 500 Index.

### Analyze the Volatility

1. Use the Pandas plot function and the kind="box" parameter to visualize the daily return data for each of the four portfolios and for the S&P 500 in a box plot.

~~~
daily_returns.plot(kind = "box", legend = True, figsize=(14, 12), title="Daily Returns")
~~~
**Note(see above):** Uses the daily return data to create a box plot that visualizes the volatility of the 4 funds and the S&P 500.

~~~
daily_returns.plot.box(legend = True, figsize=(14, 12), title="Daily Returns")
~~~
**Note(see above):** Uses the daily return data to create a box plot that visualizes the volatility of the 4 funds and the S&P 500. Although this provides the same results as the previous code, it does not include the "kind = 'box'" parameter.

<img width="834" alt="Plot_5" src="https://user-images.githubusercontent.com/94569323/146983809-8c9df3b0-4131-4ae7-9a14-7394412e88b9.png">

2. Use the Pandas drop function to create a new DataFrame that contains the data for just the four fund portfolios by dropping the S&P 500 column. Visualize the daily return data for just the four fund portfolios by using another box plot.

~~~
new_daily_returns = (daily_returns.drop(columns = ['S&P 500']))
~~~
**Note(see above):** Creates a new DataFrame containing only the 4 fund portfolios by dropping the S&P 500 column from the daily_returns DataFrame.

~~~
new_daily_returns.plot.box(legend = True, figsize=(12, 14), title="New Daily Returns"))
~~~
**Note(see above):** Uses the daily return data from the "new_daily_returns" dataframe to create a box plot that visualizes the volatility of the 4 funds.

<img width="726" alt="Plot_6" src="https://user-images.githubusercontent.com/94569323/146983851-2332fe65-2537-4c61-b4dd-99b8576da267.png">

3. Answer the following question: 

**Question: Based on the box plot visualization of just the four fund portfolios, which fund was the most volatile (with the greatest spread) and which was the least volatile (with the smallest spread)?**

Answer: Based on the box plot visualization of the four fund portfolios it is evident that the Berkshire Hathaway INC fund was the most volatile fund, however, the identification of the least volatile fund remains unclear due to the similarities in appearance between the Soros Fund box plot and the Tiger Global box plot.

### Analyze the Risk

1. Use the Pandas std function to calculate the standard deviation for each of the four portfolios and for the S&P 500. Review the standard deviation calculations, sorted from smallest to largest.

~~~
standard_deviation = daily_returns.std()
~~~
**Note(see above):** Calculates the standard deviation for all 4 portfolios and the S&P 500.

~~~
standard_deviation.sort_values()
~~~
**Note(see above):** Reviews the standard deviations sorted smallest to largest.

<img width="321" alt="Sort_values_1" src="https://user-images.githubusercontent.com/94569323/146983921-4c7de0f2-ae06-489b-867a-2c659cb156f6.png">

2. Calculate the annualized standard deviation for each of the four portfolios and for the S&P 500. To do that, multiply the standard deviation by the square root of the number of trading days. Use 252 for that number.

~~~
annual_standard_deviation = standard_deviation * np.sqrt(252)
~~~
**Note(see above):** Calculates the annualized standard deviation for all 4 portfolios and the S&P 500.

~~~
annual_standard_deviation.sort_values()
~~~
**Note(see above):** Reviews the annualized standard deviations sorted smallest to largest.

<img width="324" alt="Sort_values_2" src="https://user-images.githubusercontent.com/94569323/146984014-7f21962a-d107-4508-a327-f47f7b728d37.png">

3. Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of the four fund portfolios and of the S&P 500 index.

~~~
daily_rolling_1 = daily_returns.rolling(window = 21).std()
~~~
**Note(see above):** Applies the 21-day rolling window and the ".std()" function to the "daily_returns" dataframe, and creates a new dataframe named "daily_rolling_1".

~~~
daily_rolling_1.plot(figsize=(15, 9), title="Rolling Standard Deviation")
~~~
**Note(see above):** Uses the data from the "daily_rolling_1" dataframe to plot the rolling standard deviation of the 4 portfolios and the S&P 500.

<img width="706" alt="Plot_7" src="https://user-images.githubusercontent.com/94569323/146984065-e43c7579-044e-4657-a846-bf42730ce610.png">

4. Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of only the four fund portfolios. Be sure to include the title parameter, and adjust the figure size if necessary.

~~~
daily_rolling_2 = new_daily_returns.rolling(window = 21).std()
~~~
**Note(see above):** Applies the 21-day rolling window and the ".std()" function to the "new_daily_returns" dataframe, and creates a new dataframe named "daily_rolling_2".

~~~
daily_rolling_2.plot(figsize=(15, 9), title="Rolling Standard Deviation 2")
~~~
**Note(see above):** Uses the data from the "daily_rolling_2" dataframe to plot the rolling standard deviation of the 4 portfolios.

<img width="707" alt="Plot_8" src="https://user-images.githubusercontent.com/94569323/146984112-8878ceff-08ac-4028-adb0-14c70f63d542.png">

5. Answer the following three questions:

**Question: Based on the annualized standard deviation, which portfolios pose more risk than the S&P 500?**

Answer: Based on the annualized standard deviation none of the portfolios pose more risk than the S&P 500. In other words, the annual standard deviation of the S&P 500 is higher than that of each of the four funds.

**Question: Based on the rolling metrics, does the risk of each portfolio increase at the same time that the risk of the S&P 500 increases?**

Answer: Based on the rolling metrics, a trend exists in which the risk of each portfolio tends to increase at the same time that the risk of the S&P 500 increases.

**Question: Based on the rolling standard deviations of only the four fund portfolios, which portfolio poses the most risk? Does this change over time?**

Answer: Based on the rolling standard deviations of only the four fund portfolios, the Berkshire Hathaway INC fund poses the most risk. However, the visualization also makes it clear that times exist when the Berkshire Hathaway INC fund is not the most volatile fund (this is highlighted by the 2015-2017 protion of the visualization).

### Analyze the Risk-Return Profile

1. Use the daily return DataFrame to calculate the annualized average return data for the four fund portfolios and for the S&P 500. Use 252 for the number of trading days. Review the annualized average returns, sorted from lowest to highest.

~~~
average_annual_returns = daily_returns.mean() * 252
~~~
**Note(see above):** Calculates the annual average return data for the for fund portfolios and the S&P 500 while using 252 as the number of trading days in the year.

~~~
average_annual_returns.sort_values()
~~~
**Note(see above):** Reviews the annual average returns sorted from lowest to highest.

<img width="325" alt="Sort_values_3" src="https://user-images.githubusercontent.com/94569323/146984177-ad2b1be1-51f5-4aec-a15e-b5366d132539.png">

2. Calculate the Sharpe ratios for the four fund portfolios and for the S&P 500. To do that, divide the annualized average return by the annualized standard deviation for each. Review the resulting Sharpe ratios, sorted from lowest to highest.¶

~~~
sharpe_ratios = average_annual_returns / annual_standard_deviation
~~~
**Note(see above):** Calculates the annualized Sharpe Ratios for each of the 4 portfolios and the S&P 500.

~~~
sharpe_ratios.sort_values()
~~~
**Note(see above):** Reviews the annualized Sharpe Ratios sorted from lowest to highest.

<img width="329" alt="Sort_values_4" src="https://user-images.githubusercontent.com/94569323/146984220-6100d9ac-56b5-4e91-a9a3-3a085e4a1356.png">

3. Visualize the Sharpe ratios for the four funds and for the S&P 500 in a bar chart.

~~~
sharpe_ratios.plot(kind = "bar", figsize=(15, 10), title="Sharpe Ratios")
~~~
**Note(see above):** Visualizes the Sharpe ratios as a bar chart.

<img width="833" alt="Plot_9" src="https://user-images.githubusercontent.com/94569323/146984261-88cdeaa3-ebcc-4802-92d8-909b21f8e66e.png">

4. Answer the following question: 

**Question: Which of the four portfolios offers the best risk-return profile? Which offers the worst?**

Answer: According to the visualization, it is clear that the Berkshire Hathaway INC fund offers the best risk-return profile, and that the Paulson & Company INC fund offers the worst risk-return profile.

### Diversify the Portfolio

Use the Pandas var function to calculate the variance of the S&P 500 by using a 60-day rolling window.

~~~
sp5_var = daily_returns['S&P 500'].rolling(window = 60).var()
~~~
**Note(see above):** Calculates the variance of the S&P 500 using a rolling 60-day window.

#### Choose two portfolios that you’re most likely to recommend as investment options and complete the following steps:

1. Using the 60-day rolling window, the daily return data, and the S&P 500 returns, calculate the covariance. Review the last five rows of the covariance of the portfolio.

~~~
tiger_cov = daily_returns['TIGER GLOBAL MANAGEMENT LLC'].rolling(window = 60).cov(daily_returns['S&P 500'])
~~~
**Note(see above):** Calculates the covariance for the Tiger Global Management LLC fund using a 60-day rolling window.

~~~
tiger_cov.tail()
~~~
**Note(see above):** Reviews the last five rows of the covariance data for the Tiger Global Management LLC fund.

~~~
berk_cov = daily_returns['BERKSHIRE HATHAWAY INC'].rolling(window = 60).cov(daily_returns['S&P 500'])
~~~
**Note(see above):** Calculates the covariance for the Berkshire Hathaway INC fund using a 60-day rolling window.

~~~
berk_cov.tail()
~~~
**Note(see above):** Reviews the last five rows of the covariance data for the Berkshire Hathaway INC fund.


2. Calculate the beta of the portfolio. To do that, divide the covariance of the portfolio by the variance of the S&P 500.

~~~
tiger_beta = (tiger_cov / sp5_var)
~~~
**Note(see above):** Calculates the beta for the Tiger Global Management LLC fund based on the 60-day rolling covariance compared to the market (S&P 500).

~~~
tiger_beta.tail()
~~~
**Note(see above):** Reviews the last five rows of the beta information for the Tiger Global Management LLC fund.

~~~
berk_beta =(berk_cov / sp5_var)
~~~
**Note(see above):** Calculates the beta for the Berkshire Hathaway INC fund based on the 60-day rolling covariance compared to the market (S&P 500).

~~~
berk_beta.tail()
~~~
**Note(see above):** Reviews the last five rows of the beta information for the Berkshire Hathaway INC fund.

3. Use the Pandas mean function to calculate the average value of the 60-day rolling beta of the portfolio.

~~~
tiger_beta.mean()
~~~
**Note(see above):** Calculates the average of the 60-day rolling beta for the Tiger Global Management LLC fund.

<img width="174" alt="Mean_1" src="https://user-images.githubusercontent.com/94569323/146984576-783956cc-5a32-4bf1-9e7c-f4446436af4e.png">

~~~
berk_beta.mean()
~~~
**Note(see above):** Calculates the average of the 60-day rolling beta for the Berkshire Hathaway INC fund.

<img width="160" alt="Mean_2" src="https://user-images.githubusercontent.com/94569323/146984628-ecf8bd5a-9701-410f-8f83-bb5926844262.png">

4. Plot the 60-day rolling beta.

~~~
tiger_beta.plot(legend = True, figsize=(15, 8), title="Rolling Beta", color = "blue", label = "Tiger")
~~~
**Note(see above):** Plots the rolling beta for the Tiger Global Management LLC fund.

<img width="834" alt="Plot_10" src="https://user-images.githubusercontent.com/94569323/146984329-58545bd9-bc6c-4bcb-bbf3-25df6ce59477.png">

~~~
berk_beta.plot(legend = True, figsize=(15, 8), color = "red", label = "Berkshire")
~~~
**Note(see above):** Plots the rolling beta for the Berkshire Hathaway INC fund.

<img width="836" alt="Plot_11" src="https://user-images.githubusercontent.com/94569323/146984361-d468cf50-91e5-4fc2-873b-e5b41c4e261b.png">

#### Answer the following two questions:

**Question: Which of the two portfolios seem more sensitive to movements in the S&P 500?**

Answer: 

**Question: Which of the two portfolios do you recommend for inclusion in your firm’s suite of fund offerings?**

Answer: 

## Contributors

Chancie Altham: Developer

## License

MIT License has been added to the project.