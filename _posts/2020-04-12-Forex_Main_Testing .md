---
layout: post
title: Forex Analysis using Python
date: 2020-04-12 00:00:00 +0300
description: Basic exploratory analysis of EUR / USD data using python. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: # add tag
---

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import datetime as dt
```


```python
data = pd.read_csv("/content/drive/My Drive/EURUSD_Candlestick_1_M_BID_01.01.2020-02.01.2020.csv")
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Local time</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01.01.2020 00:00:00.000 GMT+1100</td>
      <td>1.12307</td>
      <td>1.12321</td>
      <td>1.12305</td>
      <td>1.12313</td>
      <td>211.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01.01.2020 00:01:00.000 GMT+1100</td>
      <td>1.12314</td>
      <td>1.12321</td>
      <td>1.12310</td>
      <td>1.12314</td>
      <td>119.96</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01.01.2020 00:02:00.000 GMT+1100</td>
      <td>1.12313</td>
      <td>1.12322</td>
      <td>1.12311</td>
      <td>1.12320</td>
      <td>131.04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01.01.2020 00:03:00.000 GMT+1100</td>
      <td>1.12320</td>
      <td>1.12320</td>
      <td>1.12301</td>
      <td>1.12301</td>
      <td>161.16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01.01.2020 00:04:00.000 GMT+1100</td>
      <td>1.12301</td>
      <td>1.12306</td>
      <td>1.12290</td>
      <td>1.12290</td>
      <td>109.39</td>
    </tr>
  </tbody>
</table>
</div>






```python
data["Local time"] = pd.to_datetime(data["Local time"])
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Local time</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-01 00:00:00-11:00</td>
      <td>1.12307</td>
      <td>1.12321</td>
      <td>1.12305</td>
      <td>1.12313</td>
      <td>211.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-01 00:01:00-11:00</td>
      <td>1.12314</td>
      <td>1.12321</td>
      <td>1.12310</td>
      <td>1.12314</td>
      <td>119.96</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-01 00:02:00-11:00</td>
      <td>1.12313</td>
      <td>1.12322</td>
      <td>1.12311</td>
      <td>1.12320</td>
      <td>131.04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-01 00:03:00-11:00</td>
      <td>1.12320</td>
      <td>1.12320</td>
      <td>1.12301</td>
      <td>1.12301</td>
      <td>161.16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-01 00:04:00-11:00</td>
      <td>1.12301</td>
      <td>1.12306</td>
      <td>1.12290</td>
      <td>1.12290</td>
      <td>109.39</td>
    </tr>
  </tbody>
</table>
</div>




```python
data["price_change"] = abs(data.Close - data.Close.shift(5))*10000
data.head(11)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Local time</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>price_change</th>
      <th>Close_open</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-01 00:00:00-11:00</td>
      <td>1.12307</td>
      <td>1.12321</td>
      <td>1.12305</td>
      <td>1.12313</td>
      <td>211.50</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-01 00:01:00-11:00</td>
      <td>1.12314</td>
      <td>1.12321</td>
      <td>1.12310</td>
      <td>1.12314</td>
      <td>119.96</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-01 00:02:00-11:00</td>
      <td>1.12313</td>
      <td>1.12322</td>
      <td>1.12311</td>
      <td>1.12320</td>
      <td>131.04</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-01 00:03:00-11:00</td>
      <td>1.12320</td>
      <td>1.12320</td>
      <td>1.12301</td>
      <td>1.12301</td>
      <td>161.16</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-01 00:04:00-11:00</td>
      <td>1.12301</td>
      <td>1.12306</td>
      <td>1.12290</td>
      <td>1.12290</td>
      <td>109.39</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2020-01-01 00:05:00-11:00</td>
      <td>1.12291</td>
      <td>1.12299</td>
      <td>1.12289</td>
      <td>1.12290</td>
      <td>98.78</td>
      <td>2.3</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2020-01-01 00:06:00-11:00</td>
      <td>1.12292</td>
      <td>1.12296</td>
      <td>1.12291</td>
      <td>1.12291</td>
      <td>75.55</td>
      <td>2.3</td>
      <td>2.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2020-01-01 00:07:00-11:00</td>
      <td>1.12291</td>
      <td>1.12305</td>
      <td>1.12290</td>
      <td>1.12301</td>
      <td>108.44</td>
      <td>1.9</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2020-01-01 00:08:00-11:00</td>
      <td>1.12302</td>
      <td>1.12310</td>
      <td>1.12302</td>
      <td>1.12309</td>
      <td>147.11</td>
      <td>0.8</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2020-01-01 00:09:00-11:00</td>
      <td>1.12310</td>
      <td>1.12320</td>
      <td>1.12306</td>
      <td>1.12306</td>
      <td>99.04</td>
      <td>1.6</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020-01-01 00:10:00-11:00</td>
      <td>1.12306</td>
      <td>1.12319</td>
      <td>1.12305</td>
      <td>1.12316</td>
      <td>112.29</td>
      <td>2.6</td>
      <td>2.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.hist(data.price_change, bins=5, rwidth=50)
plt.grid(True)
```



![png]({{site.baseurl}}/assets/img/output_5_1.png)



```python
data.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>price_change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2880.000000</td>
      <td>2880.000000</td>
      <td>2880.000000</td>
      <td>2880.000000</td>
      <td>2880.000000</td>
      <td>2875.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.121116</td>
      <td>1.121139</td>
      <td>1.121093</td>
      <td>1.121114</td>
      <td>42.756497</td>
      <td>6.256696</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.000871</td>
      <td>0.000881</td>
      <td>0.000860</td>
      <td>0.000871</td>
      <td>71.687594</td>
      <td>10.872843</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.118340</td>
      <td>1.118450</td>
      <td>1.118290</td>
      <td>1.118340</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.120760</td>
      <td>1.120760</td>
      <td>1.120760</td>
      <td>1.120760</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.120760</td>
      <td>1.120760</td>
      <td>1.120760</td>
      <td>1.120760</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.121610</td>
      <td>1.121630</td>
      <td>1.121590</td>
      <td>1.121610</td>
      <td>63.165000</td>
      <td>9.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.123910</td>
      <td>1.123910</td>
      <td>1.123800</td>
      <td>1.123890</td>
      <td>1028.520000</td>
      <td>80.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
data["Close_open"] = abs(data.Close - data.Open.shift(5)) * 10000
```


```python
data1 = data[5:]
```


```python
data1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Local time</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>price_change</th>
      <th>Close_open</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>2020-01-01 00:05:00-11:00</td>
      <td>1.12291</td>
      <td>1.12299</td>
      <td>1.12289</td>
      <td>1.12290</td>
      <td>98.78</td>
      <td>23.0</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2020-01-01 00:06:00-11:00</td>
      <td>1.12292</td>
      <td>1.12296</td>
      <td>1.12291</td>
      <td>1.12291</td>
      <td>75.55</td>
      <td>23.0</td>
      <td>2.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2020-01-01 00:07:00-11:00</td>
      <td>1.12291</td>
      <td>1.12305</td>
      <td>1.12290</td>
      <td>1.12301</td>
      <td>108.44</td>
      <td>19.0</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2020-01-01 00:08:00-11:00</td>
      <td>1.12302</td>
      <td>1.12310</td>
      <td>1.12302</td>
      <td>1.12309</td>
      <td>147.11</td>
      <td>8.0</td>
      <td>1.1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2020-01-01 00:09:00-11:00</td>
      <td>1.12310</td>
      <td>1.12320</td>
      <td>1.12306</td>
      <td>1.12306</td>
      <td>99.04</td>
      <td>16.0</td>
      <td>0.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
data1.corr()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>price_change</th>
      <th>Close_open</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Open</th>
      <td>1.000000</td>
      <td>0.998601</td>
      <td>0.998310</td>
      <td>0.997626</td>
      <td>0.204556</td>
      <td>0.210262</td>
      <td>0.092992</td>
    </tr>
    <tr>
      <th>High</th>
      <td>0.998601</td>
      <td>1.000000</td>
      <td>0.996683</td>
      <td>0.998380</td>
      <td>0.233578</td>
      <td>0.233510</td>
      <td>0.111613</td>
    </tr>
    <tr>
      <th>Low</th>
      <td>0.998310</td>
      <td>0.996683</td>
      <td>1.000000</td>
      <td>0.998568</td>
      <td>0.168343</td>
      <td>0.180726</td>
      <td>0.071696</td>
    </tr>
    <tr>
      <th>Close</th>
      <td>0.997626</td>
      <td>0.998380</td>
      <td>0.998568</td>
      <td>1.000000</td>
      <td>0.199497</td>
      <td>0.204080</td>
      <td>0.090815</td>
    </tr>
    <tr>
      <th>Volume</th>
      <td>0.204556</td>
      <td>0.233578</td>
      <td>0.168343</td>
      <td>0.199497</td>
      <td>1.000000</td>
      <td>0.641241</td>
      <td>0.482832</td>
    </tr>
    <tr>
      <th>price_change</th>
      <td>0.210262</td>
      <td>0.233510</td>
      <td>0.180726</td>
      <td>0.204080</td>
      <td>0.641241</td>
      <td>1.000000</td>
      <td>0.447109</td>
    </tr>
    <tr>
      <th>Close_open</th>
      <td>0.092992</td>
      <td>0.111613</td>
      <td>0.071696</td>
      <td>0.090815</td>
      <td>0.482832</td>
      <td>0.447109</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>


