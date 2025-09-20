# BHTP-TradingView-Scaffolding
Example HTML File with Javascriprt integration of TradingView's LightWeight Charts for non Technical Hobbyists learning to code through trading examples.  
*This is mostly a reference project for myself, so I don't have to go through all the documentation process in the futur.*

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
| 2 | chart02.html | insert details here |
| 3 | chart03.html | insert details here |