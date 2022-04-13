```python
class TickerPlot():
    
    def __init__(self, start=None, end=None):
        import datetime, time
        
        if end is None:
            end = datetime.datetime.today()
        if start is None:
            start = datetime.datetime(2010,1,1)
        
        self.start = start
        self.end = end
        
    def plot(self, ticker, metric=None):
        import datetime as dt
        import matplotlib.pyplot as plt
        import pandas as pd
        from matplotlib import style
        from pip._internal import main
        
        try:
            import yfinance
        except: 
            main(['install', 'yfinance'])
            import yfinance   

        try:
            import pandas_datareader.data as web
        except: 
            main(['install', 'pandas_datareader'])
            import pandas_datareader.data as web
        
        style.use('ggplot')
        r = yfinance.Ticker(ticker)
        history = r.history(start=self.start, end=self.end, interval="1d", frequency="1d")
        df = pd.DataFrame(history)
        df.insert(0, 'symbol', ticker)
        df = df.dropna(subset=['Close'])
        df = df.reset_index()
        df = df.rename(columns={ "Date": "date", 
                           "High": "high",
                           "Low": "low",
                           "Open": "open",
                           "Close": "close",
                           "Volume": "volume"})
        df = df[['symbol', 'date', 'high', 'low', 'open', 'close', 'volume']]
        df = df.set_index('symbol')
        df['date'] = pd.to_datetime(df['date'])
        if metric is None:
            df.plot(x='date')
            plt.show()
        else:
            try:
                if type(metric) is list:
                    metric.append('date')
                else:
                    metric = [metric, 'date']
                df[metric].plot(x='date')
                plt.show()
            except:
                print("Metric '", metric, "' could not be found!")
                
```


```python
import datetime as dt
start = dt.datetime(2000, 1, 1)
end = dt.datetime(2016, 12, 31)
```


```python
plotter = TickerPlot(start=start, end=end)
plotter.plot('TSLA')
```


![png](output_2_0.png)



```python
plotter.plot('MSFT')
```


![png](output_3_0.png)



```python
plotter.plot('GOOG', metric='close')
```


![png](output_4_0.png)



```python
plotter.plot('GOOG')
```


![png](output_5_0.png)



```python
plotter.plot('AAPL', metric=['close', 'open'])
```


![png](output_6_0.png)



```python
plotter.plot('COKE', metric=['high', 'low'])
```


![png](output_7_0.png)


## Jonathan Doolittle
