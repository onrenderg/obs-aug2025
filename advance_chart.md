
Version

```console
: console.log(TradingView.version());
CL v25.002 (internal id ea00b60e @ 2023-07-12T14:51:16.080Z)

```



1.

```html
<div id="chart">         
</div> <script type="text/javascript" src="https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js"></script>

```

2.

```html
<!-- 1. Define Datafeed FIRST with hoopks/funcSignatures  having callbacks -->
<script> 
  // Properly attach to window object
  window.Datafeed = {
    onReady: (callback) => {
      console.log('[onReady]: Method call');
    },
    searchSymbols: (userInput, exchange, symbolType, onResultReadyCallback) => {
      console.log('[searchSymbols]: Method call');
    },
    resolveSymbol: (symbolName, onSymbolResolvedCallback, onResolveErrorCallback, extension) => {
      console.log('[resolveSymbol]: Method call', symbolName);
    },
    getBars: (symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) => {
      console.log('[getBars]: Method call', symbolInfo);
    },
    subscribeBars: (symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) => {
      console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
    unsubscribeBars: (subscriberUID) => {
      console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
  };
</script>

```


## arrow functions to traditional function expressions

```html
<!-- 1. Define Datafeed FIRST with hooks/funcSignatures having callbacks -->
<script> 
  // Properly attach to window object
  window.Datafeed = {
    onReady: function(callback) {
      console.log('[onReady]: Method call');
    },
    searchSymbols: function(userInput, exchange, symbolType, onResultReadyCallback) {
      console.log('[searchSymbols]: Method call');
    },
    resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback, extension) {
      console.log('[resolveSymbol]: Method call', symbolName);
    },
    getBars: function(symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) {
      console.log('[getBars]: Method call', symbolInfo);
    },
    subscribeBars: function(symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) {
      console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
    unsubscribeBars: function(subscriberUID) {
      console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
  };
</script>

```

# Working :

```python
from flask import Flask, render_template_string, jsonify

app = Flask(__name__)


data = [
    {
        "time": 1622505600000, # it is time = 2021-06-01 00:00:00
        "open": 15,
        "high": 30,
        "low":  10,
        "close": 20,
    },
    {
        "time": 1622592000000, # it is time = 2021-06-02 00:00:00
        "open": 10,
        "high": 20,
        "low": 5,
        "close": 15,
    }
]

@app.route('/historical')
def historical():
    return jsonify(data)



html_doc = """
<html>
<body>

<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js"></script>
<div id="chart-container"></div>





<script> 
  // Properly attach to window object
  var  Datafeed = {
    onReady: function(callback) {
      console.log('[onReady]: Method call');
      setTimeout(callback, 1000);
    },
    resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback, extension) {
      console.log('[resolveSymbol]: Method call', symbolName);
      setTimeout(function() {
        onSymbolResolvedCallback({
          symbol: symbolName,
          name: symbolName,
          timezone: "Etc/UTC",
          session: "24x7",
          pricescale: 100,   // Means 1 = 1.00 (supports 2 decimal places)
          minmov: 1          // Smallest allowed price change is 0.01
        });
      }, 1000);
    },
    getBars: function(symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) {
      console.log('[getBars]: Method call', symbolInfo);
      fetch('/historical')
        .then(function(response) {
          response.json().then(function(data) {
                const { from, to, firstDataRequest } = periodParams;
                    if (firstDataRequest) {
                    // Pass the received  bars data back to the TradingView chart
                    onHistoryCallback(data, { noData: data.length === 0 });
                    } else {
                        onHistoryCallback([], { noData: true });
                    }
          

          });
        });
    },
        subscribeBars: function(symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) {
      console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
    unsubscribeBars: function(subscriberUID) {
      console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
    },

  };



const widget = new TradingView.widget({
    container: "chart-container",
    datafeed: Datafeed,
    library_path: "https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/",
    symbol: "BTCUSDT",

    width: window.innerWidth,
    height: window.innerHeight,
    
});

</script>

</body>
</html>
"""
@app.route('/')
def index():
    return render_template_string(html_doc)


app.run(debug=True, host='0.0.0.0', port=80)


```

## ## For seconds to work in resolve symbol hook it should have options for and onReady should have resuplitons onReady

```html
<script>
    // Properly attach to window object
    window.Datafeed = {
      onReady: (callback) => callback({ supported_resolutions: ["5S", "10S", "15S", "30S"] }),
      searchSymbols: (userInput, exchange, symbolType, onResultReadyCallback) => {
        console.log('[searchSymbols]: Method call');
      },
      resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback) {
      setTimeout(function() {
        onSymbolResolvedCallback({
          name: symbolName,
          ticker: symbolName,
          session: "24x7",  // Must be a non-empty string.
          timezone: "Etc/UTC",
          minmov: 1,
          pricescale: 100,
          has_intraday: true,
          has_seconds: true, 
        });
      }, 0);
    },
      getBars: (symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) => {
        console.log('[getBars]: Method call', symbolInfo);
      },
      subscribeBars: (symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) => {
        console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
      },
      unsubscribeBars: (subscriberUID) => {
        console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
      },
    };
</script>

```

# Intraday 
## addition to @working

```html
     interval: "1", timezone: "Asia/Kolkata" to widget construjcvtr 
     has_intraday: true, to resolveSymgol fn 
```

```python
from flask import Flask, render_template_string, jsonify

app = Flask(__name__)


data = [
    {
        "time": 1735703100000 , # it is time = "2025-06-01 03:45:00"
        "open": 15,
        "high": 30,
        "low":  10,
        "close": 20,
    },
    {
        "time": 1735789560000, # it is time = "2025-06-01 03:46:00"
        "open": 10,
        "high": 20,
        "low": 5,
        "close": 15,
    }
]

@app.route('/historical')
def historical():
    return jsonify(data)



html_doc = """
<html>
<body>

<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js"></script>
<div id="chart-container"></div>





<script> 
  // Properly attach to window object
  var  Datafeed = {
    onReady: function(callback) {
      console.log('[onReady]: Method call');
      setTimeout(callback, 1000);
    },
    resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback, extension) {
      console.log('[resolveSymbol]: Method call', symbolName);
      setTimeout(function() {
        onSymbolResolvedCallback({
          symbol: symbolName,
          name: symbolName,
          timezone: "Etc/UTC",
          session: "24x7",
          pricescale: 100,   // Means 1 = 1.00 (supports 2 decimal places)
          minmov: 1,          // Smallest allowed price change is 0.01

          has_intraday: true,
        });
      }, 1000);
    },
    getBars: function(symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) {
      console.log('[getBars]: Method call', symbolInfo);
      fetch('/historical')
        .then(function(response) {
          response.json().then(function(data) {
                const { from, to, firstDataRequest } = periodParams;
                    if (firstDataRequest) {
                    // Pass the received  bars data back to the TradingView chart
                    onHistoryCallback(data, { noData: data.length === 0 });
                    } else {
                        onHistoryCallback([], { noData: true });
                    }
          

          });
        });
    },
        subscribeBars: function(symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) {
      console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
    unsubscribeBars: function(subscriberUID) {
      console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
    },

  };



const widget = new TradingView.widget({
    container: "chart-container",
    datafeed: Datafeed,
    library_path: "https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/",
    symbol: "BTCUSDT",
    interval: "1",

    width: window.innerWidth,
    height: window.innerHeight,
    timezone: "Asia/Kolkata",
});

</script>

</body>
</html>
"""
@app.route('/')
def index():
    return render_template_string(html_doc)


app.run(debug=True, host='0.0.0.0', port=80)


```

# Seconds 

## addition to @working

```html
     interval: "5S", timezone: "Asia/Kolkata" to widget construjcvtr  and         enabled_features: ["seconds_resolution"],
     has_seconds: true, to resolveSymgol fn 
```

and 

```js
    onReady: function(callback) {

      console.log('[onReady]: Method call');

      setTimeout(callback({ supported_resolutions: ["5S", "10S", "15S", "30S"] }), 1000);

    },
```
# working 

```python
from flask import Flask, render_template_string, jsonify

app = Flask(__name__)


data = [
    {
        "time": 1735703105000 , # it is time = "2025-06-01 03:45:05"
        "open": 15,
        "high": 30,
        "low":  10,
        "close": 20,
    },
    {
        "time": 1735703110000, # it is time = "2025-06-01 03:46:10"
        "open": 10,
        "high": 20,
        "low": 5,
        "close": 15,
    }
]

@app.route('/historical')
def historical():
    return jsonify(data)



html_doc = """
<html>
<body>

<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js"></script>
<div id="chart-container"></div>





<script> 
  // Properly attach to window object
  var  Datafeed = {
    onReady: function(callback) {
      console.log('[onReady]: Method call');
      setTimeout(callback, 1000);
    },
    resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback, extension) {
      console.log('[resolveSymbol]: Method call', symbolName);
      setTimeout(function() {
        onSymbolResolvedCallback({
          symbol: symbolName,
          name: symbolName,
          timezone: "Etc/UTC",
          session: "24x7",
          pricescale: 100,   // Means 1 = 1.00 (supports 2 decimal places)
          minmov: 1,          // Smallest allowed price change is 0.01

          has_intraday: true,
          has_seconds: true, 
        });
      }, 1000);
    },
    getBars: function(symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) {
      console.log('[getBars]: Method call', symbolInfo);
      fetch('/historical')
        .then(function(response) {
          response.json().then(function(data) {
                const { from, to, firstDataRequest } = periodParams;
                    if (firstDataRequest) {
                    // Pass the received  bars data back to the TradingView chart
                    onHistoryCallback(data, { noData: data.length === 0 });
                    } else {
                        onHistoryCallback([], { noData: true });
                    }
          

          });
        });
    },
        subscribeBars: function(symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) {
      console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
    unsubscribeBars: function(subscriberUID) {
      console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
    },

  };



const widget = new TradingView.widget({
    container: "chart-container",
    datafeed: Datafeed,
    library_path: "https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/",
    symbol: "BTCUSDT",
    interval: "5S",

    width: window.innerWidth,
    height: window.innerHeight,
    timezone: "Asia/Kolkata",
});

</script>

</body>
</html>
"""
@app.route('/')
def index():
    return render_template_string(html_doc)


app.run(debug=True, host='0.0.0.0', port=80)


```

3. ## exptra otiopns 

```html
 <script>
    new TradingView.widget({
      container: "chart_container",
      datafeed: window.Datafeed, // Now available
      library_path: "https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js",
      symbol: "BTC/USD",
      interval: "5S",
      timezone: "Asia/Kolkata", //"Etc/UTC"
      theme: "dark",
      locale: "en",
      fullscreen: "true",   
      enabled_features: ["dont_show_boolean_study_arguments", "seconds_resolution"],
    });
</script>

```



# Indicators 

```python
from flask import Flask, render_template_string, jsonify

app = Flask(__name__)

# from datetime import datetime
# datetime.fromisoformat(item["time"]).timestamp() * 1000
# print(int(datetime.fromisoformat(strtime).replace(tzinfo=timezone.utc).timestamp() * 1000))

data = [
    {
        "time": 1735703105000 , # it is time = "2025-06-01 03:45:05"
        "open": 15,
        "high": 30,
        "low":  10,
        "close": 20,
    },
    {
        "time": 1735703110000, # it is time = "2025-06-01 03:46:10"
        "open": 10,
        "high": 20,
        "low": 5,
        "close": 15,
    }
]

@app.route('/historical')
def historical():
    return jsonify(data)



html_doc = """
<html>
<body>

<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js"></script>
<div id="chart-container"></div>





<script> 
  // Properly attach to window object
  var  Datafeed = {
    onReady: function(callback) {
      console.log('[onReady]: Method call');
      setTimeout(callback({ supported_resolutions: ["5S", "10S", "15S", "30S"] }), 1000);
    },
    resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback, extension) {
      console.log('[resolveSymbol]: Method call', symbolName);
      setTimeout(function() {
        onSymbolResolvedCallback({
          symbol: symbolName,
          name: symbolName,
          timezone: "Etc/UTC",
          session: "24x7",
          pricescale: 100,   // Means 1 = 1.00 (supports 2 decimal places)
          minmov: 1,          // Smallest allowed price change is 0.01

          has_intraday: true,
          has_seconds: true, 
          
        });
      }, 1000);
    },
    getBars: function(symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) {
      console.log('[getBars]: Method call', symbolInfo);
      fetch('/historical')
        .then(function(response) {
          response.json().then(function(data) {
                const { from, to, firstDataRequest } = periodParams;
                    if (firstDataRequest) {
                    // Pass the received  bars data back to the TradingView chart
                    onHistoryCallback(data, { noData: data.length === 0 });
                    } else {
                        onHistoryCallback([], { noData: true });
                    }
          

          });
        });
    },
        subscribeBars: function(symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) {
      console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
    unsubscribeBars: function(subscriberUID) {
      console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
    },

  };



const widget = new TradingView.widget({
    container: "chart-container",
    datafeed: Datafeed,
    library_path: "https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/",
    symbol: "BTCUSDT",
    interval: "5S",
    

    width: window.innerWidth,
    height: window.innerHeight,
    timezone: "Asia/Kolkata",

    enabled_features: ["study_templates", "seconds_resolution"],  
    disabled_features: ["create_volume_indicator_by_default"],  
});

widget.onChartReady(() => {
  // Add multiple MAs
  const studies = [
    { name: "Moving Average", inputs: { length: 12 }, id: "MA12", options: { "plot.linewidth": 3, "plot.color": "yellow" } },
    { name: "Moving Average", inputs: { length: 24 }, id: "MA24", options: { "plot.linewidth": 3, "plot.color": "red" } },
    { name: "Moving Average", inputs: { length: 50 }, id: "MA50", options: { "plot.linewidth": 3, "plot.color": "black" } },
    { name: "Moving Average", inputs: { length: 200 }, id: "MA200", options: { "plot.linewidth": 4, "plot.color": "blue" } }
  ];

  studies.forEach(study => {
    widget.chart().createStudy(study.name, false, false, study.inputs, study.options, { id: study.id });
  });

  // Add MACD study
  widget.chart().createStudy('MACD', false, false, {
    fast_length: 12,
    slow_length: 26,
    signal_length: 9,
  });

  // Add RSI study
  widget.chart().createStudy('Relative Strength Index', false, false, {
    length: 14,
  }, {
    'plot.color': '#2196F3',
    'plot.linewidth': 2,
    'upperband.color': '#f23645',
    'lowerband.color': '#089981',
  }
  );

});



  
</script>

</body>
</html>
"""
@app.route('/')
def index():
    return render_template_string(html_doc)


app.run(debug=True, host='0.0.0.0', port=80)
```





# SingleTf


```python
from flask import Flask, render_template_string, jsonify

app = Flask(__name__)

# from datetime import datetime
# datetime.fromisoformat(item["time"]).timestamp() * 1000
# print(int(datetime.fromisoformat(strtime).replace(tzinfo=timezone.utc).timestamp() * 1000))


# acer@DESKTOP-IC0J9HE MINGW64 ~
# $ date  -u -d @1731901500000
# Tue Oct 10 06:00:00 UTC 56851

# acer@DESKTOP-IC0J9HE MINGW64 ~
# $ date  -u -d @1731901500
# Mon Nov 18 03:45:00 UTC 2024


import pandas as pd 

@app.route('/historical')
def historical():
    csv_file_path = '/var/lib/data/one.csv'
    df  = pd.read_csv(csv_file_path)

    # Convert seconds to milisconds 
    df.time = df.time * 1000
    # Ensure numeric columns are properly typed
    numeric_columns = ['open', 'high', 'low', 'close', 'volume']
    df[numeric_columns] = df[numeric_columns].apply(pd.to_numeric, errors='coerce')
    data = df.to_dict('records')
    return jsonify(data)



html_doc = """
<html>
<body>

<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js"></script>
<div id="chart-container"></div>





<script> 
  // Properly attach to window object
  var  Datafeed = {
    onReady: function(callback) {
      console.log('[onReady]: Method call');
      setTimeout(function() {
        callback({ supported_resolutions: ["5S", "10S", "15S", "30S"] })
      },0)
    },
    resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback, extension) {
      console.log('[resolveSymbol]: Method call', symbolName);
      setTimeout(function() {
        onSymbolResolvedCallback({
          symbol: symbolName,
          name: symbolName,
          timezone: "Etc/UTC",
          session: "24x7",
          pricescale: 100,   // Means 1 = 1.00 (supports 2 decimal places)
          minmov: 1,          // Smallest allowed price change is 0.01

          has_intraday: true,
          has_seconds: true, 
          
        });
      }, 1000);
    },
    getBars: function(symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) {
      console.log('[getBars] entrypoint : Method call', symbolInfo);
      fetch('/historical')
        .then(function(response) {
          response.json().then(function(data) {
                const { from, to, firstDataRequest } = periodParams;
                    if (firstDataRequest) {
                      console.log(`[getBars]: Returning historical data (${data.length} bars)`);
                    // Pass the received  bars data back to the TradingView chart
                      onHistoryCallback(data, { noData: data.length === 0 });
                    } else {
                        onHistoryCallback([], { noData: true });
                    }
          

          });
        });
    },
        subscribeBars: function(symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) {
      console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
    },
    unsubscribeBars: function(subscriberUID) {
      console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
    },

  };



const widget = new TradingView.widget({
    container: "chart-container",
    datafeed: Datafeed,
    library_path: "https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/",
    symbol: "BTCUSDT",
    interval: "5S",
    

    width: window.innerWidth,
    height: window.innerHeight,
    timezone: "Asia/Kolkata",

    enabled_features: ["seconds_resolution"],  
    disabled_features: ["create_volume_indicator_by_default"],  
});




widget.onChartReady(() => {




  // Add Moving Averages
  const studies = [
    { name: "Moving Average", inputs: { length: 12 }, id: "MA12", options: { "plot.linewidth": 3, "plot.color": "yellow" } },
    { name: "Moving Average", inputs: { length: 24 }, id: "MA24", options: { "plot.linewidth": 3, "plot.color": "red" } },
    { name: "Moving Average", inputs: { length: 50 }, id: "MA50", options: { "plot.linewidth": 3, "plot.color": "black" } },
    { name: "Moving Average", inputs: { length: 200 }, id: "MA200", options: { "plot.linewidth": 4, "plot.color": "blue" } }
  ];

  studies.forEach(study => {
    widget.chart().createStudy(study.name, false, false, study.inputs, study.options, { id: study.id });
  });

  // Add MACD
  widget.chart().createStudy('MACD', false, false, {
    fast_length: 12,
    slow_length: 26,
    signal_length: 9,
  });

    // Add RSI study
  widget.chart().createStudy('Relative Strength Index', false, false, {
    length: 14,
  });

});





  
</script>

</body>
</html>
"""
@app.route('/')
def index():
    return render_template_string(html_doc)


app.run(debug=True, host='0.0.0.0', port=80)
```



## MultiTimeframe 









## ## getBars Datafeed Imp

* 
[[h_dataprep]]



### ### Datafeed Imp


```html
<script>
    // Properly attach to window object
    window.Datafeed = {
      onReady: (callback) => callback({ supported_resolutions: ["5S", "10S", "15S", "30S"] }),
      searchSymbols: (userInput, exchange, symbolType, onResultReadyCallback) => {
        console.log('[searchSymbols]: Method call');
      },
      resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback) {
      setTimeout(function() {
        onSymbolResolvedCallback({
          name: symbolName,
          ticker: symbolName,
          session: "24x7",  // Must be a non-empty string.
          timezone: "Etc/UTC",
          minmov: 1,
          pricescale: 100,
          has_intraday: true,
          has_seconds: true, 
        });
      }, 0);
    },
      getBars: (symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) => {

        const { from, to, firstDataRequest } = periodParams;

        console.log('[getBars]: Method call', symbolInfo, resolution, new Date(from * 1000), new Date(to * 1000));

        if (firstDataRequest) {

          console.log(`[getBars]: Returning historical data (${historicalData.length} bars)`);

          onHistoryCallback(historicalData, { noData: historicalData.length === 0 });

        } else {

          // For subsequent requests, indicate no additional data

          console.log('[getBars]: No additional historical data available');

          onHistoryCallback([], { noData: true });

        }

      },
      subscribeBars: (symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) => {
        console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);
      },
      unsubscribeBars: (subscriberUID) => {
        console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
      },
    };
</script>


```

## ## subscribeBars Datafeed Imp

[[h_dataprep]] +

```js

// Simple variable to store the active callback

let activeCallback = null;

// Flag to track if streaming has started

let streamingStarted = false;



```

```html
<script>

// Simulate streaming data

    function startStreaming() {

      let index = 0;

      const streamInterval = setInterval(() => {

        if (index < streamingData.length) {

          const newData = streamingData[index++];

          console.log("Streaming new data:", newData);

          // Call the callback directly

          if (activeCallback) {

            activeCallback(newData);

          }

        } else {

          console.log("Streaming completed");

          clearInterval(streamInterval);

        }

      }, 1000); // Stream a new candle every second

    }

</script>
```

### ### Datafeed Imp

```html




<script>
    // Properly attach to window object
    window.Datafeed = {
      onReady: (callback) => callback({ supported_resolutions: ["5S", "10S", "15S", "30S"] }),
      searchSymbols: (userInput, exchange, symbolType, onResultReadyCallback) => {
        console.log('[searchSymbols]: Method call');
      },
      resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback) {
      setTimeout(function() {
        onSymbolResolvedCallback({
          name: symbolName,
          ticker: symbolName,
          session: "24x7",  // Must be a non-empty string.
          timezone: "Etc/UTC",
          minmov: 1,
          pricescale: 100,
          has_intraday: true,
          has_seconds: true, 
        });
      }, 0);
    },
      getBars: (symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) => {
        console.log('[getBars]: Method call', symbolInfo);
        const { from, to, firstDataRequest } = periodParams;
        console.log('[getBars]: Method call', symbolInfo, resolution, new Date(from * 1000), new Date(to * 1000));
        
        console.log('[getBars]: No additional historical data available');

        onHistoryCallback([], { noData: true });

      },

      subscribeBars: (symbolInfo, resolution, onRealtimeCallback, subscriberUID) => {

        console.log('[subscribeBars]: Method call with subscriberUID:', subscriberUID);

        // Store the callback directly

        activeCallback = onRealtimeCallback;

        // Start streaming data if not already started

        if (!streamingStarted && streamingData.length > 0) {

          streamingStarted = true;

          startStreaming();

        }

      },
      unsubscribeBars: (subscriberUID) => {
        console.log('[unsubscribeBars]: Method call with subscriberUID:', subscriberUID);
      },
    };
</script>

```

### ### setUpdate if else block currernt bar update or new create

```html
<!DOCTYPE html>
<html>
<head>
    <title>TradingView Chart with 5S Resolution and Real-Time Updates</title>
</head>
<body>
    <div id="tv_chart_container"></div>

    <!-- Include the charting library -->
    <!-- <script type="text/javascript" src="/charting_library/charting_library.standalone.js"></script> -->

    <script type="text/javascript" src="https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js"></script>
    <!-- Utility Functions and Dynamic In-Memory Data -->
    <script>
      // Convert an ISO date string to a timestamp (milliseconds)
      function isoToMs(isoString) {
          return new Date(isoString).getTime();
      }

      // Generate initial in-memory bar data for the last 10 minutes (one bar every 5 seconds)
      var inMemoryBars = [];
      var now = Date.now();
      var startTime = now - (10 * 60 * 1000);  // 10 minutes ago
      for (var time = startTime; time < now; time += 5000) {
          inMemoryBars.push({
              time: new Date(time).toISOString(),
              open: 100,
              high: 105,
              low: 95,
              close: 100 + Math.random() * 10,
              volume: Math.floor(Math.random() * 1000) + 1000
          });
      }
    </script>
    
    <!-- Datafeed Implementation -->
    <script>
      window.Datafeed = {
        onReady: function(callback) {
          setTimeout(function() {
            callback({
              // Include "5S" for 5‑second resolution support.
              supported_resolutions: ["5S", "1", "5", "15", "30", "60", "D"]
            });
          }, 0);
        },
        resolveSymbol: function(symbolName, onSymbolResolvedCallback, onResolveErrorCallback) {
          setTimeout(function() {
            onSymbolResolvedCallback({
              name: symbolName,
              ticker: symbolName,
              session: "24x7",  // Must be a non-empty string.
              timezone: "Etc/UTC",
              minmov: 1,
              pricescale: 100,
              has_intraday: true,
              has_seconds: true,  
              supported_resolutions: ["5S", "1", "5", "15", "30", "60", "D"]
            });
          }, 0);
        },
        getBars: function(symbolInfo, resolution, periodParams, onHistoryCallback, onErrorCallback) {
          var bars = [];
          // Convert "from" and "to" parameters (in seconds) to milliseconds.
          var periodFromMs = periodParams.from * 1000;
          var periodToMs = periodParams.to * 1000;
          
          inMemoryBars.forEach(function(bar) {
              var barTime = isoToMs(bar.time);
              if (barTime >= periodFromMs && barTime <= periodToMs) {
                  bars.push({
                      time: barTime,
                      open: bar.open,
                      high: bar.high,
                      low: bar.low,
                      close: bar.close,
                      volume: bar.volume
                  });
              }
          });
          
          if (bars.length) {
              onHistoryCallback(bars, { noData: false });
          } else {
              onHistoryCallback([], { noData: true });
          }
        },
        subscribeBars: function(symbolInfo, resolution, onRealtimeCallback, subscriberUID, onResetCacheNeededCallback) {
          // Update the chart every second, even though each bar represents 5 seconds.
          // When a new 5-second period starts, a new bar is pushed; otherwise, the current bar is updated.
          var intervalMs = 1000;  // update every 1 second
          var barDurationMs = 5000; // 5-second bar interval

          // Save the timer ID using the subscriberUID for later unsubscription.
          this._realtimeSubscriber = this._realtimeSubscriber || {};
          this._realtimeSubscriber[subscriberUID] = setInterval(function() {
              var now = Date.now();
              // Calculate the start of the current 5-second period.
              var currentBarStartTime = Math.floor(now / barDurationMs) * barDurationMs;
              
              // Get the latest bar.
              var lastBar = inMemoryBars[inMemoryBars.length - 1];
              var lastBarTime = isoToMs(lastBar.time);
              
              if (currentBarStartTime > lastBarTime) {
                  // A new bar period has started.
                  var newBar = {
                      time: new Date(currentBarStartTime).toISOString(),
                      open: lastBar.close,
                      high: lastBar.close,
                      low: lastBar.close,
                      close: lastBar.close + (Math.random() * 2 - 1), // some slight random variation
                      volume: Math.floor(Math.random() * 100) + 100
                  };
                  inMemoryBars.push(newBar);
                  onRealtimeCallback({
                      time: currentBarStartTime,
                      open: newBar.open,
                      high: newBar.high,
                      low: newBar.low,
                      close: newBar.close,
                      volume: newBar.volume
                  });
              } else {
                  // Update the existing bar.
                  var newPrice = lastBar.close + (Math.random() * 2 - 1);
                  lastBar.high = Math.max(lastBar.high, newPrice);
                  lastBar.low = Math.min(lastBar.low, newPrice);
                  lastBar.close = newPrice;
                  lastBar.volume += Math.floor(Math.random() * 10);
                  onRealtimeCallback({
                      time: currentBarStartTime,
                      open: lastBar.open,
                      high: lastBar.high,
                      low: lastBar.low,
                      close: lastBar.close,
                      volume: lastBar.volume
                  });
              }
          }, intervalMs);
        },
        unsubscribeBars: function(subscriberUID) {
          if (this._realtimeSubscriber && this._realtimeSubscriber[subscriberUID]) {
              clearInterval(this._realtimeSubscriber[subscriberUID]);
              delete this._realtimeSubscriber[subscriberUID];
          }
        }
      };
    </script>
    
    <!-- TradingView Widget Initialization -->
    <script>
      new TradingView.widget({
        // Use "container" (not the deprecated "container_id")
        container: "tv_chart_container",
        datafeed: window.Datafeed,
        library_path: 'https://cdn.jsdelivr.net/gh/parth-royale/cdn@main/charting_library/charting_library.standalone.js',
        symbol: "BTC/USD",
        interval: "5S",  // Default to 5-second intervals.
        timezone: "Asia/Kolkata",
        theme: "dark",
        locale: "en",
        fullscreen: "true",   
        enabled_features: ["dont_show_boolean_study_arguments", "seconds_resolution"],     
        // Note: Studies have been omitted; built-in studies might not support sub‑minute data.
      });
    </script>
</body>
</html>
```





## ## multiTfGetBars Datafeed Imp


## ## multiTfGetBars Datafeed Imp

```html
reqClientSide:

1. chartInit seprate function call in flow when timeframe chage or refresh  after DOM is activ




```

```python

reqServerSide:

	1. wsServer flask-sock ws obj use from outside the decorator function 

```


```html
There are to be made   docs for clientSide and  serverSide  DataFeed Imp
For clientSide multiTf  
For serverSide multiTf  
Alternative
aggregated array and lowestTfarray/fiveSecondCandles and use only setData/getBars

	getBars on firstRequest get all data from fetch /history = CANDLES == hist+arr1
	// need to  knowHow serverSide py Tech like flask-sock outof decorator calling and 
	the geenarate library feature random lib unifrom   


```

```html

<script>
var fiveSecondCandles = [] //base tf array 
var currentTimeframe = '5s' 
var aggregated 
// not using update method or subscibeBars 's onRealtimeCallback

// language no code pseudocode  with sequential flow the single point in seq have the processing in words  not code  with technical detail in words 

function resampleCandles() {

}

function updateChart() {

1. if timeFrame in sec === 5 then aggregated var =  fiveSecondCandles array data
else aggregated var = array returned from resampledCandles function passed 
fiveSecondCandles and    output timeFrame after that 
2.setData method invoked with aggregated array 
mermaid diagram

// based on button click tieframe chages and chart also reinit

function initChart(){
  1. create candlestickSeries
  // 2. preprocess data
  // 3. setData  updateChart() using glbal fiveSecondCandles based on current tf


}
function wsClient(){
const ws = new WebSocket((location.protocol === "https:" ? "wss://" : "ws://") + location.host + "/ws");
  ws.onmessage = function(event) {
    const data = JSON.parse(event.data);
    const candle = data.candle;
    // Update fiveSecondCandles: if the candle's time matches the last candle, update it; otherwise, append.
    if (fiveSecondCandles.length && fiveSecondCandles[fiveSecondCandles.length - 1].time === candle.time) {
      fiveSecondCandles[fiveSecondCandles.length - 1] = candle;
    } else {
      fiveSecondCandles.push(candle);
    }
    updateChart();
}


function main() {

  data = fetch_hist()
  fiveSecondCandles = data
  initChart()
  wsClient() 
}
</script>
```


```txt

timeframeChange  & refreshPage

timeframeChange  : 

refreshPage      :

```

```js
// Resample data into bars for the given timeframe
    function resampleData(data, timeframe) {
      const resampledData = [];
      let currentBar = null;
      const timeframeMs = getTimeframeMs(timeframe);

      for (const row of data) {
        const barTime = Math.floor(row.time / timeframeMs) * timeframeMs;
        if (!currentBar || currentBar.time !== barTime) {
          if (currentBar) {
            resampledData.push(currentBar);
          }
          currentBar = {
            time: barTime,
            open: row.open,
            high: row.high,
            low: row.low,
            close: row.close,
            volume: row.volume
          };
        } else {
          currentBar.high = Math.max(currentBar.high, row.high);
          currentBar.low = Math.min(currentBar.low, row.low);
          currentBar.close = row.close;
          currentBar.volume += row.volume;
        }
      }
      if (currentBar) {
        resampledData.push(currentBar);
      }
      return resampledData;
    }
```

# Used in : 
# [[h_specStory_multiTfAdvChart]]

# Lwcharts

[[h_serverb3.py]]
[[h_serverb3bk.py]]

@lola