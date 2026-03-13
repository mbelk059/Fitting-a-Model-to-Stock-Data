1. Dataset Description and Preprocessing
   For this analysis, Apple Inc. (AAPL) stock price data was pulled using the yfinance Python
   package, covering 5 years from January 2019 to January 2024. The prices used are adjusted
   closing prices, meaning they account for things like stock splits, so the numbers are
   consistent across the whole period.

In total, 1,258 trading days of data were downloaded. From there, daily returns were
calculated, basically how much the stock price went up or down each day as a percentage.
The first row was removed since it had no previous day to compare to. There were no missing
values to deal with since yfinance already skips weekends and holidays automatically.

To set up the data for the model, the previous 5 days of returns were used as inputs to predict
the next day's return. After doing this, 1,252 rows were ready to use. The data was then split
into 80% for training (1,001 days) and 20% for testing (251 days).

2. Model Description and Purpose
   A Linear Regression model was used to try and predict what the next day's return would be,
   based on the last 5 days of returns. The overall idea is if there's any pattern in recent price
   movements, the model should be able to realize.
   Linear regression was chosen because it's straightforward and easy to understand. The model
   was only trained on the training data, and then tested on data it had never seen before to get a
   fair evaluation.
   How well the model did on the test set:
   Metric Value
   RMSE 0.013010
   MAE 0.00989

The errors are pretty small, as the model was off by about 1% on average per day. Daily stock
returns are naturally small numbers, so this doesn't mean the model is great at predicting
which direction the stock will move.  
3. Financial Metrics (on Unseen Test Set)
These three metrics were all calculated using only the test set, the 251 days the model never
trained on. This makes them a fair reflection of real performance. A risk-free rate of 5% per
year was used (based on U.S. Treasury bill rates at the time), which is the return you would
get instead of investing.

Metric Value
Annual Return 49.61%
Sharpe Ratio 1.8443
Sortino Ratio 2.8761
Annual Return (49.61%): This means if you had held AAPL during the test period, you
would have made about 49.61% on your money in a year. The stock market on average
returns around 10% a year, so this is well above that. A big reason for this is that the test
window caught AAPL bouncing back strongly after a rough 2022.
Sharpe Ratio (1.8443): The Sharpe ratio measures how much return you're getting for the
amount of risk you're taking. Anything above 1.0 is generally considered good, so a score of
1.84 means AAPL was delivering really good returns without taking on high amounts of risk
during this period.
Sortino Ratio (2.8761): The Sortino ratio is similar to Sharpe, but only counts the bad
volatility (the days the stock dropped) as risk. A score of 2.88 is quite high, and it tells us that
most of AAPL's volatility during this period was positive, meaning mostly gains, not losses.  
4. Insights and Observations
Overall, AAPL had a really strong run during the test period. The gap between the Sharpe
and Sortino ratios shows that the stock's ups were much bigger than its downs.

However, a 49.61% annual return is unusually high and probably won't repeat itself every
year. It was largely driven by the specific timing of the test window catching a recovery
period. So while the numbers look good, it's important not to rely too much into them as a
long-term forecast.

On the modelling side, linear regression was a good starting point for this kind of analysis,
but it has its limits when it comes to predicting stock returns day to day. The error values
being in a similar range to the actual returns means the model is doing okay, but there's
definitely room to do better. Adding more inputs like trading volume or news headlines, or
trying a more advanced model like an LSTM, would likely give stronger results in the future.

References
Yahoo Finance. (2024). AAPL historical data. Retrieved March 2026, from
https://finance.yahoo.com/quote/AAPL/history/
