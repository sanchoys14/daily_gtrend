Recently, I needed some seven years of Google Trends daily data. It turned out that by default it’s not possible to get it neither through the web interface nor via API. So I wrote a tiny script that pulls daily Google Trends data for any period using gtrendsR package.

![g_trends_splitscreen](https://github.com/sanchoys14/daily_gtrend/assets/53646551/624d4d1d-3376-4613-ab42-b3973abdb5db)

**What’s the problem with Google Trends?**

Google Trends returns data in daily granularity only if the timeframe is less than 9 months. If the timeframe is between 9 months and 5 years, you’ll get weekly data, and if it’s longer than 5 years – you’ll get monthly data.

A trivial solution like querying the data month by month and then tieing it together won’t work in this case, because Google Trends assess interest in relative values within the given time period. It means that for a given keyword and month, Google Trend will estimate interest identically – with a local minimum of 0 and a local maximum of 100 – event in one month it had twice as many searches than in the other.

**Querying Google Trend daily data properly**

To get proper daily estimates, I do the following:

1. Query daily estimates for each month in the specified timeframe;
2. Queries monthly data for the whole timeframe;
3. Multiply daily estimates for each month from step 1 by its weight from step 2.

**How to use it**

Just pull daily_trend.R (or simply copy the get_daily_gtrend() function to your project). Run get_daily_gtrend() with desired parameters and it will retuern a data frame with daily Google Trends data.
