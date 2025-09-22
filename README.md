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

## Recipee for simple chart
1) HTML ***Container*** for chart to be displayed
2) Instantiate a ***chart*** object
3) Add a ***series*** to the chart
4) Create or load some ***Data*** with appropriate structure for the series added
5) use the seriesVar.setData( loadedData )
6) Add a window resize event handler to refresh the chart when necessary

 { time, open, high, low, close, customValue, color }

 ## Series Data format
 | Serie Type | SeriesDataType | List of { key:value ) pairs |
|---|---|---|
| CandlestickSeries | CandlestickData | { time, open, high, low, close, customValue?, color?, borderColor?, wickColor? } |
| BarSeries | BarData | { time, open, high, low, close, color?, customValue? } |
| LineSeries | LineData | { time, value, color?, customValue? } |
| AreaSeries | AreaData | { time, value, lineColor?, topColor?, bottomColor?, customValue? } |
| HistogramSeries | HistogramData | { time, value, color?, customValue? } |
| . | . | . |


> *keys with a "?" are optional data fields.*


## List of Data Example
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
