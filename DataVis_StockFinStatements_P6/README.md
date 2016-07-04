# Data Visualization
_by Alex Bugrimenko_

## Summary 

#### In this project I want to create a visualization for company financial statements.

Usually, financial statements presented as a simple table with a lot of numbers grouped by years and divided into 3 documents: Income Statement, Cash Flow Statement and Balance Sheet. For example, here is how annual statements for Apple Inc. presented on NASDAQ and Google:

* [NASDAQ](http://www.nasdaq.com/symbol/aapl/financials?query=income-statement)

![Apple Financial Statements - NASDAQ presentation](/DataVis_StockFinStatements_P6/img/AAPL_FinStatemenet_NASDAQ.PNG)

* [Google](https://www.google.com/finance?q=NASDAQ%3AAAPL&fstype=ii)

![Apple Financial Statements - Google presentation](/DataVis_StockFinStatements_P6/img/AAPL_FinStatemenet_Google.PNG)


The problem is investor really have to study these numbers to make sense out of it. And after studying, in general, investors are focusing on the financial ratios, such as Return on Investment, Return on Assets and such. The row numbers do not tell a lot of a story, but the growth of the major categories such as Equity or EPS can quickly show investor if the company’s finances are in a good shape.

Of course it is important to know what specific amount was reported as a revenue or book value in the latest annual statement. And the next important thing is to see the trend – if revenue growth is slowing down, it is usually raises a red flag. Only trained eye can quickly see if the change in a row numbers is good enough. For example, value investors want to see consistent growth of major characteristic by at least 15% year over year. It almost guarantees that a business can successfully funds its own future growth. And this is relatively difficult to see by looking at a raw numbers.

My goal in this project is to create effective visualization for presenting company’s financial statements and allow user to see major profitability ratios as well as major financial statement items along with their year-over-year growth rates.


## Design 

In this project we are focusing on a single stock analysis - my visualization should present data for a single stock at a time and I’m considering stock selection to be out of scope of this project (yet, for simplicity and proper testing, information about several stocks available and it is easy to switch between them at the bottom of the page).

### The Data

I can generate annual financial statements in a simple CSV file format for all major US stocks using [stock2own.com](http://www.stock2own.com) services. Each file contains information about a single stock and may contain up to 10 years of historical data for each item (as much as available). All items in each file are sorted by item type and date (reverse sort order for date – the latest row is always the first one).

### Design

#### Financial Ratios

There are two types of financial ratios could be relatively easy computed based on financial statements:

**Liquidity Ratios** – measure the amount of cash available to cover expenses both current and long term. These ratios are especially important in keeping a business alive. It includes the following ratios:

* Current Ratio
* Quick Ratio
* Financial Leverage

**Profitability Ratios** - measure and help control income. This is done through higher sales, larger margins, getting more from expenses and/or combination of these methods. The major Profitability Ratios are:

* Return on Assets (ROA)
* Return on Equity (ROE)
* Return on Invested Capital (ROIC)

For each ratio I want to show historical values for as many years as available. Because this is a time series type of data, the best representation for it is a linear chart, so for each ratio I show its own line chart, with clear indication of the latest value available.

Almost all of the listed above ratios (except of financial leverage) have "generally accepted" standards. For example, the generally accepted standard for Current Ratio is 2 (current assets should be 2 times or 200% of current liabilities), meaning that if the most recent value is below 2, it is considered to be a "red flag", while values equal or above 2 are considered to be a good signs.

In order to illustrate it, I'm adding a base line for each ratio where generally accepted value is available and if the most recent value is satisfying this base line, I want to highlight it with a green background color. If the most recent value is not satisfying generally accepted standard, I want to highlight it with a red background. The color change is done gradually, illustrating that this analysis is rather a recommendation and user should make her own decision.

I also want to highlight min and max values on a chart by marking those points with a different color and also adding a year label to clearly and easily identifying best and worst performing years.

And lastly, I'm adding a quick description of each ratio and explanation of the generally accepted standard because this page is designed for general audience and should not require any special financial knowledge.

### Financial Statements

There are couple of dozens of items in financial statements and it makes sense to group them by type of a document: Income Statement, Cash Flow Statement and Balance Sheet. User is available to select any item from each category and see the data one item at a time. The default selection is set to the most "popular" item. For example, in an Income Statement it is usually Earnings per Share.

Just like ratios, financial statement item is a time series type of data, therefore the best representation for it is a linear chart, so for each statement item I show its own line chart, with clear indication of the latest value available and min/max values - just like I did for ratios.

It is very important to see the trend of the data change, therefore I'm adding a year-over-year growth rate chart for any item selected. I'm presenting growth rates as a vertical bar chart, where it is easy to compare value for each year with previous and next year. 

The whole purpose of the growth rate chart is to show the trend, therefore there is no necessity to focus on exact values (each value will be shown if user points mouse pointer over any circle or bar), which allows me to combine two types of charts without warring about different axis and scales. However, I want to make sure that they are synchronized to time axis, because this is important to know which year produced what growth. To better demonstrate relationship between raw data and growth rates, in the final version I'm showing both linear and bar charts on the same place. It allows clearly and easily identify which growth rates was produced in what year.

#### Technical Implementation

In this project I'm using D3.js to create my visualization. To set the page layout and make it mobile-friendly, I'm using bootstrap styles and jQuery.


## Feedback 
- include all feedback you received from others on your visualization from the first sketch to the final visualization

## Resources

* [http://www.visualcinnamon.com/2015/11/learnings-from-a-d3-js-addict-on-starting-with-canvas.html](http://www.visualcinnamon.com/2015/11/learnings-from-a-d3-js-addict-on-starting-with-canvas.html)
* [https://bocoup.com/weblog/d3js-and-canvas](https://bocoup.com/weblog/d3js-and-canvas)
* [http://www.tnoda.com/blog/2013-12-19](http://www.tnoda.com/blog/2013-12-19)
* [https://github.com/d3/d3/wiki/Time-Formatting](https://github.com/d3/d3/wiki/Time-Formatting)
* [http://bl.ocks.org/d3noob/a22c42db65eb00d4e369](http://bl.ocks.org/d3noob/a22c42db65eb00d4e369)
* [http://stackoverflow.com/questions/13728402/what-is-the-difference-d3-datum-vs-data](http://stackoverflow.com/questions/13728402/what-is-the-difference-d3-datum-vs-data)

