# BHTP-TradingView-Scaffolding
Example HTML Files with Javascriprt integration of TradingView's LightWeight Charts for non Technical Hobbyists learning to code through trading examples.  
*This is mostly a reference project for myself, so I don't have to go through all the documentation research process in the futur.*

# Installation
```
git clone https://github.com/poivronjaune/BHTP-TradingView-Scaffolding.git
```  
This will install a copy of the HTML files used has scaffolding for the lightweight charts javascript library.  
Please note, that a copy of the version 5 standalone Javascript library will be copied in the libs folder.  
This makes chart viewing available when an internet connection is not available.

> *Footnotes* :  
> For more information on the Lightweight Charts JS Library offered by TradingView, see the nodejs installation section below.    
> For a CDN link rather than a local copy of the library, see the CDN Section below.  5

# TradingView Tutorial  
In the HTML file named : *customization-tutorial-start.html*  
is the result of following the TradingView Customization [Tutorial](https://tradingview.github.io/lightweight-charts/tutorials/customization/intro), a self paced well defined step by step approach to using some basic elements of the free open-source library.  

# CDN Version  
TradingView offers a dynamically downloadable CDN (Content Delivery Network) version of the lightweightCharts Javascript library. To use this version simply replace the following lines of code:
```
<!-- Adding the standalone version of Lightweight charts -->
<script
    type="text/javascript"
    src="libs\lightweight-charts.standalone.production.js"
></script>  
```
With these lines  (*notice the change destination of the src attribute*) 
```
<!-- Adding the Online CDN version of Lightweight charts -->
<script
    type="text/javascript"
    src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"
></script>
```
Hope this makes sense for everyone.  


# Example code
| # | File | Description |
|---|---|---|
| 1 | chart01.html | The most basic example full width using hard coded price data and all the default values such as white background, green and red candles, time frame at the bottom and price scale on the right |
| 2 | chart02.html | Simple line chart that represents an Simple Moving Average. SMA Data is hard coded for simplicity, but should be calculated in real charts |
| 3 | chart03.html | Chart with multiple data (candlestick and SMA). Also custom color for line chart |
| 4 | chart04.html | Loading data from web source and display simple candlestick chart. See Javascript lessons for code structure to call each step in sequece without using Async calls<br><br>Beginer firendly examples to understand calling sequences. |
| 5 | chart05.html | Loading data from web source and display simple candlestick chart sized to the chart container width and size. Also added flexibility for csv file headers (checking strings and column names). Used a unix timestamp instead of a string date |

||||
| 5 | fetch01.html | Example of fetching data from a github repository using TRADITIONAL Javascript .then() methods  |
| 6 | fetch02.html | Example of fetching data from a github repository using MODERN Javascript async() / await methods  |

## Recipee for simple chart
1) HTML ***Container*** for chart to be displayed
2) Instantiate a ***chart*** object
3) Add a ***series*** to the chart
4) Create or load some ***Data*** with appropriate structure for the series added
5) use the seriesVar.setData( loadedData )
6) Add a window resize event handler to refresh the chart when necessary



 ## Series Data format
{ time, open, high, low, close, customValue, color }  
    

| Serie Type | SeriesDataType | List of { key:value ) pairs |
|---|---|---|
| CandlestickSeries | CandlestickData | { time, open, high, low, close, customValue?, color?, borderColor?, wickColor? } |
| BarSeries | BarData | { time, open, high, low, close, color?, customValue? } |
| LineSeries | LineData | { time, value, color?, customValue? } |
| AreaSeries | AreaData | { time, value, lineColor?, topColor?, bottomColor?, customValue? } |
| HistogramSeries | HistogramData | { time, value, color?, customValue? } |
| . | . | . |


> *keys with a "?" are optional data fields.*


## Hard Coded Data For testing
```
candles = [
  { time: "2018-10-19", open: 180.34, high: 180.99, low: 178.57, close:  179.85 },
  { time: "2018-10-22", open: 180.82, high: 181.41, low: 177.56, close:  178.75 },
  { time: "2018-10-23", open: 175.77, high: 179.49, low: 175.44, close:  178.53 },
  { time: "2018-10-24", open: 178.58, high: 182.37, low: 176.31, close:  176.97 },
  { time: "2018-10-25", open: 177.52, high: 180.51, low: 176.83, close:  179.07 },
]
```

# NODE JS Installation
Even if the library is considered to be a client side application, the files can be installed using a simple npm (Node Package Manager) command.  
Go to [nodejs.org/en/download](https://nodejs.org/en/download) to get an installable version of node that will include NPM.  
Get NPM version to test if it was installed properly
```
npm --version
```
Now install the nodejs version of the lightweigth charts
```
npm install --save lightweight-charts
```
This will create a folder "node_modules/lightweight-charts/dist"  
This folder contains the distribution file for the library.  
The "lightweight-charts.standalone.production.js" is the standalone version of the javascript file required to load locally.  
It is not recommended to point directly to node_module folder from the front-end, so copy this file to a folder called libs in the root of your project.  
That's it, load it in your HTML File using:
```
<!-- Adding the standalone version of Lightweight charts -->
<script
    type="text/javascript"
    src="libs\lightweight-charts.standalone.production.js"
></script>  
```

# Javascript lessons  
## Fetching data
When a web page is displayed in the browser and calls another source (web page, API, Database, etc..) to obtain data, there's always a delay before the response gets back to the browser (network latency, external source server processing time, data trasnfer time depending on size of payload, etc...).  
  
Javascript executes each line of code immediately and **DOES NOT WAIT** for responses. So, if the execution of a line of code is required, the browser must pause and wait for the request to complete. This ia an asynchronous execution.  

This delayed response can complete succesfully or fail. Enter the concept of a ***Promise***.

>💡 the command ***fetch()*** is not actually a javascript function but a Web API exposed by most browsers to allow Javascript to interact with the browser.   

### A Promise  
A **Promise** is an object that is returned by the javascript request (fetch in our example) that represents the eventual completion or failure of the asynchronous operation including its resulting value.

The promise is returned instantly after a call and can be used later. In our examples, we block the code flow to wait for the promise to complete (succesfully or not).  
  
- Traditionnal method, using ***.then()*** can be used to force the codeflow to wait until it's previous call is finished and the result is automatically pased to the next chained operation.  
  
- Modern method, using ***async()*** has the same flow. We use the **await** keyword to block code flow. One more difference is error handling that is implemented inside our helper functions. We used IIFE (Immediately Invoked Function Expression) to implement this flow neatly and similarly to .then().

### Side by side .then() vs Async
<table>
<tr><td> Traditional </td> <td> Modern </td></tr>
<tr>
<td> 

Main Flow Code - .Then()<br>-> fetch01.html
``` 
fetch(url)
    .then(handleResponse)
    .then(formatCsvData)
    .then(useData)  
    .catch(errorHandling)  
``` 
</td>
<td> 

Main Flow Code - Async (IIFE)<br>-> fetch02.html
``` 
(async () => {
    const data = await handleFetchRequest(url);
    const candleStickData = await formatCsvData(data);
    useData(candleStickData);
})();
``` 

</td>
</tr>
<table>

---
# Some references
2021: [Javascript Promises vs Async EXPLAINED (in 5 minutes)](https://www.youtube.com/watch?v=li7FzDHYZpc) by Roberts Dev Talk  
2025: [Master Async Await Javascript in an easy way](https://www.youtube.com/watch?v=H9nFFE5_VS4) by Nova Designs
