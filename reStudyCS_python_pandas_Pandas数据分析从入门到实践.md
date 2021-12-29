[<-](../index.html)
# Pandas数据分析从入门到实践

-  来自B站 蚂蚁学Python Pandas数据分析从入门到实践

# 一、 安装

# 二、读文件 read txt mysql excel

## 000001.SZ.csv结构如下
,ts_code,trade_date,open,high,low,close,pre_close,change,pct_chg,vol,amount

0,000001.SZ,20190408,13.9,14.43,13.72,13.96,13.86,0.1,0.7215,1743176.2,2464536.241

1,000001.SZ,20190404,13.43,14.0,13.43,13.86,13.44,0.42,3.125,2034365.0,2796366.353


```python
import numpy as np
import pandas as pd

df = pd.read_csv('000001.SZ.csv')
df.head()
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
      <th>Unnamed: 0</th>
      <th>ts_code</th>
      <th>trade_date</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>000001.SZ</td>
      <td>20190408</td>
      <td>13.90</td>
      <td>14.43</td>
      <td>13.72</td>
      <td>13.96</td>
      <td>13.86</td>
      <td>0.10</td>
      <td>0.7215</td>
      <td>1743176.20</td>
      <td>2464536.241</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>000001.SZ</td>
      <td>20190404</td>
      <td>13.43</td>
      <td>14.00</td>
      <td>13.43</td>
      <td>13.86</td>
      <td>13.44</td>
      <td>0.42</td>
      <td>3.1250</td>
      <td>2034365.00</td>
      <td>2796366.353</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>000001.SZ</td>
      <td>20190403</td>
      <td>13.21</td>
      <td>13.45</td>
      <td>13.15</td>
      <td>13.44</td>
      <td>13.36</td>
      <td>0.08</td>
      <td>0.5988</td>
      <td>792915.79</td>
      <td>1056166.231</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>000001.SZ</td>
      <td>20190402</td>
      <td>13.28</td>
      <td>13.48</td>
      <td>13.23</td>
      <td>13.36</td>
      <td>13.18</td>
      <td>0.18</td>
      <td>1.3657</td>
      <td>1100384.04</td>
      <td>1466040.987</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>000001.SZ</td>
      <td>20190401</td>
      <td>12.83</td>
      <td>13.55</td>
      <td>12.83</td>
      <td>13.18</td>
      <td>12.82</td>
      <td>0.36</td>
      <td>2.8081</td>
      <td>1951401.19</td>
      <td>2588268.668</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dtypes,df.index,df.columns
```




    (Unnamed: 0      int64
     ts_code        object
     trade_date      int64
     open          float64
     high          float64
     low           float64
     close         float64
     pre_close     float64
     change        float64
     pct_chg       float64
     vol           float64
     amount        float64
     dtype: object,
     RangeIndex(start=0, stop=4000, step=1),
     Index(['Unnamed: 0', 'ts_code', 'trade_date', 'open', 'high', 'low', 'close',
            'pre_close', 'change', 'pct_chg', 'vol', 'amount'],
           dtype='object'))



# 三、数据结构
## series 
index values df['a'][['a','b']]
df['low']
df.loc[1]


```python
a = df['low']
a.index,a.values
df['low'][[0,1]]

b = df.loc[1]
b.index,b.values
df.loc[2][['low','close']]
```




    low      13.15
    close    13.44
    Name: 2, dtype: object



## dataframe


```python
df['low']
df[['low','close']]
df.loc[1]
df.loc[1:2]
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
      <th>ts_code</th>
      <th>trade_date</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>000001.SZ</td>
      <td>20190404</td>
      <td>13.43</td>
      <td>14.00</td>
      <td>13.43</td>
      <td>13.86</td>
      <td>13.44</td>
      <td>0.42</td>
      <td>3.1250</td>
      <td>2034365.00</td>
      <td>2796366.353</td>
    </tr>
    <tr>
      <th>2</th>
      <td>000001.SZ</td>
      <td>20190403</td>
      <td>13.21</td>
      <td>13.45</td>
      <td>13.15</td>
      <td>13.44</td>
      <td>13.36</td>
      <td>0.08</td>
      <td>0.5988</td>
      <td>792915.79</td>
      <td>1056166.231</td>
    </tr>
  </tbody>
</table>
</div>



# 四、数据查询
## loc iloc query where
- 查询会发生 *降维* 现象
- 以下：删除列 设置index 排序 修改列数据


```python
df.drop(['Unnamed: 0'],axis=1,inplace=True)
df.set_index(['trade_date'],inplace=True)
df.sort_values('trade_date',inplace=True)
df.loc[:,'ts_code'] = df['ts_code'].str.replace('.SZ','').astype('string')
```

### loc的数值 列表 区间 条件 函数 


```python
df.head()
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20020226</th>
      <td>000001</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
    </tr>
    <tr>
      <th>20020227</th>
      <td>000001</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
    </tr>
    <tr>
      <th>20020228</th>
      <td>000001</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
    </tr>
    <tr>
      <th>20020301</th>
      <td>000001</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
    </tr>
    <tr>
      <th>20020304</th>
      <td>000001</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
    </tr>
  </tbody>
</table>
</div>




```python
#数值
df.loc[20020226,'open']
df.loc[20020226,['open','close']]
#列表
df.loc[[20020226,20020227],'open'] #->series
df.loc[[20020226,20020227],['open']]#->dataframe
df.loc[[20020226,20020227],['open','close']]
#区间
df.loc[20020226:20020228,['open']]
#条件表达式
#bool series
df['pct_chg']>9 
df.loc[df['pct_chg']>9,:]
df.loc[(df['pct_chg']>9) & (df['vol']>2000000),:]
#函数
df.loc[lambda r:(r['pct_chg']>9) & (r.index>=20130101),:]
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>xxx</th>
      <th>chg</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20130114</th>
      <td>000001</td>
      <td>15.49</td>
      <td>17.09</td>
      <td>15.49</td>
      <td>17.09</td>
      <td>15.54</td>
      <td>1.55</td>
      <td>9.97</td>
      <td>939895.90</td>
      <td>1.568842e+06</td>
      <td>0.099743</td>
      <td>0.099743</td>
    </tr>
    <tr>
      <th>20130128</th>
      <td>000001</td>
      <td>19.16</td>
      <td>21.07</td>
      <td>19.16</td>
      <td>21.07</td>
      <td>19.15</td>
      <td>1.92</td>
      <td>10.03</td>
      <td>1163995.24</td>
      <td>2.365203e+06</td>
      <td>0.100261</td>
      <td>0.100261</td>
    </tr>
    <tr>
      <th>20130228</th>
      <td>000001</td>
      <td>21.14</td>
      <td>23.00</td>
      <td>21.03</td>
      <td>23.00</td>
      <td>21.02</td>
      <td>1.98</td>
      <td>9.42</td>
      <td>1119891.72</td>
      <td>2.487831e+06</td>
      <td>0.094196</td>
      <td>0.094196</td>
    </tr>
    <tr>
      <th>20130305</th>
      <td>000001</td>
      <td>21.80</td>
      <td>23.93</td>
      <td>21.79</td>
      <td>23.93</td>
      <td>21.75</td>
      <td>2.18</td>
      <td>10.02</td>
      <td>1168987.27</td>
      <td>2.700253e+06</td>
      <td>0.100230</td>
      <td>0.100230</td>
    </tr>
    <tr>
      <th>20130711</th>
      <td>000001</td>
      <td>9.50</td>
      <td>10.34</td>
      <td>9.50</td>
      <td>10.34</td>
      <td>9.40</td>
      <td>0.94</td>
      <td>10.00</td>
      <td>1733611.47</td>
      <td>1.737228e+06</td>
      <td>0.100000</td>
      <td>0.100000</td>
    </tr>
    <tr>
      <th>20130909</th>
      <td>000001</td>
      <td>11.28</td>
      <td>12.13</td>
      <td>11.28</td>
      <td>12.13</td>
      <td>11.03</td>
      <td>1.10</td>
      <td>9.97</td>
      <td>2204493.84</td>
      <td>2.639382e+06</td>
      <td>0.099728</td>
      <td>0.099728</td>
    </tr>
    <tr>
      <th>20141128</th>
      <td>000001</td>
      <td>11.27</td>
      <td>12.44</td>
      <td>11.18</td>
      <td>12.44</td>
      <td>11.31</td>
      <td>1.13</td>
      <td>9.99</td>
      <td>4844839.36</td>
      <td>5.793392e+06</td>
      <td>0.099912</td>
      <td>0.099912</td>
    </tr>
    <tr>
      <th>20150410</th>
      <td>000001</td>
      <td>18.00</td>
      <td>19.80</td>
      <td>17.85</td>
      <td>19.80</td>
      <td>18.00</td>
      <td>1.80</td>
      <td>10.00</td>
      <td>3340209.79</td>
      <td>6.339649e+06</td>
      <td>0.100000</td>
      <td>0.100000</td>
    </tr>
  </tbody>
</table>
</div>



# 五、新增数据列
## 直接赋值 apply assign 分条件赋值


```python
df.head()
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>xxx</th>
      <th>chg</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20020226</th>
      <td>000001</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
      <td>-0.024857</td>
      <td>-0.024857</td>
    </tr>
    <tr>
      <th>20020227</th>
      <td>000001</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
      <td>0.010784</td>
      <td>0.010784</td>
    </tr>
    <tr>
      <th>20020228</th>
      <td>000001</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
      <td>-0.015519</td>
      <td>-0.015519</td>
    </tr>
    <tr>
      <th>20020301</th>
      <td>000001</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
      <td>0.003941</td>
      <td>0.003941</td>
    </tr>
    <tr>
      <th>20020304</th>
      <td>000001</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
      <td>0.016683</td>
      <td>0.016683</td>
    </tr>
  </tbody>
</table>
</div>




```python
#直接赋值
df.loc[:,'chg'] = df['change']/df['pre_close']
#df['date'] = pd.to_datetime(df['date'],format='%Y%m%d')
#apply
def fun(ser):
    return '+' if ser['change']>=0 else '-'
df.loc[:,'status'] = df.apply(fun,axis=1)
#assign
# !!!return new dataframe object!!!
df2 = df.assign(lar_chg = lambda x:x['high']-x['low'])

#分条件赋值
df['sta2'] = '备注'
df.loc[df['change']>0,'sta3'] = '牛'
df.head()
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>chg</th>
      <th>status</th>
      <th>sta2</th>
      <th>sta3</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20020226</th>
      <td>000001</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
      <td>-0.024857</td>
      <td>-</td>
      <td>备注</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20020227</th>
      <td>000001</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
      <td>0.010784</td>
      <td>+</td>
      <td>备注</td>
      <td>牛</td>
    </tr>
    <tr>
      <th>20020228</th>
      <td>000001</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
      <td>-0.015519</td>
      <td>-</td>
      <td>备注</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20020301</th>
      <td>000001</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
      <td>0.003941</td>
      <td>+</td>
      <td>备注</td>
      <td>牛</td>
    </tr>
    <tr>
      <th>20020304</th>
      <td>000001</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
      <td>0.016683</td>
      <td>+</td>
      <td>备注</td>
      <td>牛</td>
    </tr>
  </tbody>
</table>
</div>



# 六、统计
## 汇总 去重 计数 相关系数 协方差


```python
df.drop(['chg','status','sta2','sta3'],axis=1,inplace=True)
df.head()
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20020226</th>
      <td>000001</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
    </tr>
    <tr>
      <th>20020227</th>
      <td>000001</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
    </tr>
    <tr>
      <th>20020228</th>
      <td>000001</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
    </tr>
    <tr>
      <th>20020301</th>
      <td>000001</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
    </tr>
    <tr>
      <th>20020304</th>
      <td>000001</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
    </tr>
  </tbody>
</table>
</div>




```python
#汇总
df.describe()
df['close'].mean()
df['close'].std()
df['close'].count()
#非数值唯一去重
df['high'].unique()
df['high'].value_counts()
#协方差
df.cov()
df['close'].cov(df['open'])
df['close'].cov(df['open']-df['low'])
#相关系数
df.corr()
df['close'].corr(df['open'])
df['close'].corr(df['open']-df['low'])
```




    0.5377670993423458



# 七、缺失值处理
# 八、settingWithCopyWarning
# 九、数据排序


```python
df.head()
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20020226</th>
      <td>000001</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
    </tr>
    <tr>
      <th>20020227</th>
      <td>000001</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
    </tr>
    <tr>
      <th>20020228</th>
      <td>000001</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
    </tr>
    <tr>
      <th>20020301</th>
      <td>000001</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
    </tr>
    <tr>
      <th>20020304</th>
      <td>000001</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
    </tr>
  </tbody>
</table>
</div>




```python
#数据排序
#series sort
df['open'].sort_values()#series sort 
#df sort
df.sort_values('open')
df.sort_values(['open','high'],ascending=True, inplace=True)
df.sort_values(by=['open','high'],inplace=True)
#分别顺序逆序
df.sort_values(by=['open','high'],ascending=[True,False],inplace=True)
df.head()

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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20050331</th>
      <td>000001</td>
      <td>5.09</td>
      <td>5.23</td>
      <td>5.06</td>
      <td>5.21</td>
      <td>5.10</td>
      <td>0.11</td>
      <td>2.16</td>
      <td>34085.18</td>
      <td>17553.9140</td>
    </tr>
    <tr>
      <th>20050401</th>
      <td>000001</td>
      <td>5.20</td>
      <td>5.73</td>
      <td>5.12</td>
      <td>5.60</td>
      <td>5.21</td>
      <td>0.39</td>
      <td>7.49</td>
      <td>70046.55</td>
      <td>38229.9963</td>
    </tr>
    <tr>
      <th>20050329</th>
      <td>000001</td>
      <td>5.30</td>
      <td>5.37</td>
      <td>5.28</td>
      <td>5.30</td>
      <td>5.30</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>19248.09</td>
      <td>10245.7264</td>
    </tr>
    <tr>
      <th>20050330</th>
      <td>000001</td>
      <td>5.30</td>
      <td>5.30</td>
      <td>5.05</td>
      <td>5.10</td>
      <td>5.30</td>
      <td>-0.20</td>
      <td>-3.77</td>
      <td>42336.71</td>
      <td>21780.4019</td>
    </tr>
    <tr>
      <th>20050324</th>
      <td>000001</td>
      <td>5.37</td>
      <td>5.45</td>
      <td>5.32</td>
      <td>5.40</td>
      <td>5.36</td>
      <td>0.04</td>
      <td>0.75</td>
      <td>53108.20</td>
      <td>28537.9708</td>
    </tr>
  </tbody>
</table>
</div>



# 十、字符串处理

## scores.txt内容如下
张  三|89.5 |90 |98|天成 皇家壹里 4-5-1001

李  四|98 | 120 |118| 成绩优秀 副班长

王五五|99|111|110.5| 体育特长生 


```python
#读入新文件
df2 = pd.read_csv(
    'scores.txt',
    sep = '|',
    names = ['姓名','语文','数学','英语','备注'],
)
df2.head()
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张  三</td>
      <td>89.5</td>
      <td>90</td>
      <td>98.0</td>
      <td>天成 皇家壹里 4-5-1001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李  四</td>
      <td>98.0</td>
      <td>120</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111</td>
      <td>110.5</td>
      <td>体育特长生</td>
    </tr>
  </tbody>
</table>
</div>




```python
#相同
df2.loc[:,'姓名']=df2['姓名'].str.replace(' ','')
df2['姓名']=df2['姓名'].str.replace(' ','')
#属性
df2['几字名']=df2['姓名'].str.len()
# contains startwith
df2['李家人']=df2['姓名'].str.startswith('李')
#链式
df2['姓']=df2['姓名'].str.replace(' ','').str.slice(0,1)
df2.loc[:,'名']=df2['姓名'].str.replace(' ','').str.slice(1,)
#正则表达式
df2['备注']=df2['备注'].str.replace('[\d]','')
df2.head()
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
      <th>几字名</th>
      <th>李家人</th>
      <th>姓</th>
      <th>名</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>89.5</td>
      <td>90</td>
      <td>98.0</td>
      <td>天成 皇家壹里 --</td>
      <td>2</td>
      <td>False</td>
      <td>张</td>
      <td>三</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>98.0</td>
      <td>120</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
      <td>2</td>
      <td>True</td>
      <td>李</td>
      <td>四</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111</td>
      <td>110.5</td>
      <td>体育特长生</td>
      <td>3</td>
      <td>False</td>
      <td>王</td>
      <td>五五</td>
    </tr>
  </tbody>
</table>
</div>



# 十一 axis参数的理解
- 0 代表行 1 代表列 drop时
- 聚合时，表示跨以上for遍历之


```python
df2.head()
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
      <th>几字名</th>
      <th>李家人</th>
      <th>姓</th>
      <th>名</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>89.5</td>
      <td>90</td>
      <td>98.0</td>
      <td>天成 皇家壹里 --</td>
      <td>2</td>
      <td>False</td>
      <td>张</td>
      <td>三</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>98.0</td>
      <td>120</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
      <td>2</td>
      <td>True</td>
      <td>李</td>
      <td>四</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111</td>
      <td>110.5</td>
      <td>体育特长生</td>
      <td>3</td>
      <td>False</td>
      <td>王</td>
      <td>五五</td>
    </tr>
  </tbody>
</table>
</div>




```python
#删除行 等效
df2.drop(0)
df2.drop(0,axis=0)
#删除列
df2.drop('语文',axis=1)
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
      <th>姓名</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
      <th>几字名</th>
      <th>李家人</th>
      <th>姓</th>
      <th>名</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>90</td>
      <td>98.0</td>
      <td>天成 皇家壹里 --</td>
      <td>2</td>
      <td>False</td>
      <td>张</td>
      <td>三</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>120</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
      <td>2</td>
      <td>True</td>
      <td>李</td>
      <td>四</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>111</td>
      <td>110.5</td>
      <td>体育特长生</td>
      <td>3</td>
      <td>False</td>
      <td>王</td>
      <td>五五</td>
    </tr>
  </tbody>
</table>
</div>




```python
#axis=0 求值 沿该轴向滚动遍历，对交叉轴上所有元素运用聚合函数求值
df2.mean(axis=0)
df2.mean(axis=1)
#沿该轴向滚动遍历，参数x为交叉轴上的所有元素，元素个数为交叉轴的长度
df2.apply(lambda x:'%r+%r+%r'%(x[0],x[1],x[2])).head()
df2.apply(lambda x:'%r+%r+%r'%(x[0],x[1],x[2]),axis=1).head()
```




    0      '张三'+89.5+90
    1     '李四'+98.0+120
    2    '王五五'+99.0+111
    dtype: object



# 十二 索引


```python
df.head()
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20020226</th>
      <td>000001</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
    </tr>
    <tr>
      <th>20020227</th>
      <td>000001</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
    </tr>
    <tr>
      <th>20020228</th>
      <td>000001</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
    </tr>
    <tr>
      <th>20020301</th>
      <td>000001</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
    </tr>
    <tr>
      <th>20020304</th>
      <td>000001</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
    </tr>
  </tbody>
</table>
</div>




```python
%timeit df.loc[df.index==20020301]
%timeit df.loc[df['open']==10.40]
df3 = df.set_index('close',drop=False)
df3.head()
```

    1.32 ms ± 171 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    1.41 ms ± 43.8 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    




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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
    </tr>
    <tr>
      <th>close</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10.20</th>
      <td>000001</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
    </tr>
    <tr>
      <th>10.31</th>
      <td>000001</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
    </tr>
    <tr>
      <th>10.15</th>
      <td>000001</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
    </tr>
    <tr>
      <th>10.19</th>
      <td>000001</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
    </tr>
    <tr>
      <th>10.36</th>
      <td>000001</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
    </tr>
  </tbody>
</table>
</div>



## 十三、Merge语法

- DataFrame的Merge相当于SQL的Join

## scores.txt 同上

## Scores2.txt 内容如下


李  四|172CM | 65kg |

王五五|175CM|48KG|

赵  六|165CM |45KG |劳动委员


```python
df_sco1 = pd.read_csv('scores.txt',sep='|',names=['姓名','语文','数学','英语','备注'])
df_sco2 = pd.read_csv('scores2.txt',sep='|',names=['名字','身高','体重','备注'])
df_sco1['姓名']=df_sco1['姓名'].str.replace(' ','')
df_sco2['名字']=df_sco2['名字'].str.replace(' ','')
```


```python
df_sco1.head()
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>89.5</td>
      <td>90</td>
      <td>98.0</td>
      <td>天成 皇家壹里 4-5-1001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>98.0</td>
      <td>120</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111</td>
      <td>110.5</td>
      <td>体育特长生</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_sco2.head()
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
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>李四</td>
      <td>172CM</td>
      <td>65kg</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>王五五</td>
      <td>175CM</td>
      <td>48KG</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>165CM</td>
      <td>45KG</td>
      <td>劳动委员</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
    </tr>
  </tbody>
</table>
</div>




```python
#left_on right_on
#pd.merge(df_sco1,df_sco2,on='姓名',how='outer')
pd.merge(df_sco1,df_sco2,left_on='姓名',right_on='名字',how='outer',suffixes=('A','B'))
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注A</th>
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
      <th>备注B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>89.5</td>
      <td>90.0</td>
      <td>98.0</td>
      <td>天成 皇家壹里 4-5-1001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>98.0</td>
      <td>120.0</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
      <td>李四</td>
      <td>172CM</td>
      <td>65kg</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111.0</td>
      <td>110.5</td>
      <td>体育特长生</td>
      <td>王五五</td>
      <td>175CM</td>
      <td>48KG</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>赵六</td>
      <td>165CM</td>
      <td>45KG</td>
      <td>劳动委员</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>赵六</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
    </tr>
  </tbody>
</table>
</div>



# 十四、合并 concat

- pd.concat(obj,axis,join.ignore_index)

- df.append(other,ignore_index)



```python
pd.concat([df_sco1,df_sco2])
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>89.5</td>
      <td>90.0</td>
      <td>98.0</td>
      <td>天成 皇家壹里 4-5-1001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>98.0</td>
      <td>120.0</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111.0</td>
      <td>110.5</td>
      <td>体育特长生</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>李四</td>
      <td>172CM</td>
      <td>65kg</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>王五五</td>
      <td>175CM</td>
      <td>48KG</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>劳动委员</td>
      <td>赵六</td>
      <td>165CM</td>
      <td>45KG</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
      <td>赵六</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([df_sco1,df_sco2],join='inner')
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
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>天成 皇家壹里 4-5-1001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>成绩优秀 副班长</td>
    </tr>
    <tr>
      <th>2</th>
      <td>体育特长生</td>
    </tr>
    <tr>
      <th>0</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>劳动委员</td>
    </tr>
    <tr>
      <th>3</th>
      <td>家在团结小区</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_sco1.append(df_sco2)
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>89.5</td>
      <td>90.0</td>
      <td>98.0</td>
      <td>天成 皇家壹里 4-5-1001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>98.0</td>
      <td>120.0</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111.0</td>
      <td>110.5</td>
      <td>体育特长生</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>李四</td>
      <td>172CM</td>
      <td>65kg</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>王五五</td>
      <td>175CM</td>
      <td>48KG</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>劳动委员</td>
      <td>赵六</td>
      <td>165CM</td>
      <td>45KG</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
      <td>赵六</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



# 十五、拆分合并Excel文件
# 十六、groupby 分组统计

- 类似SQL select city,max(temp) from city_weahter group by city;
- groupby 数据分组 再应用聚合函数、转换函数

## 分组 使用聚合


```python
#数据预处理
df = pd.read_csv('000001.SZ.csv')
df.drop(['Unnamed: 0'],axis=1,inplace=True)
df.set_index(['trade_date'],inplace=True)
df.sort_values('trade_date',inplace=True)
#加上月 年 数据
df.loc[:,'yearmonth'] = (df.index/100).astype('int32')
df.loc[:,'year'] = (df.index/100/100).astype('int32')
df.loc[:,'month'] = df['yearmonth']-(df['year']*100)

df.head()
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
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>yearmonth</th>
      <th>year</th>
      <th>month</th>
    </tr>
    <tr>
      <th>trade_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20020226</th>
      <td>000001.SZ</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
      <td>200202</td>
      <td>2002</td>
      <td>2</td>
    </tr>
    <tr>
      <th>20020227</th>
      <td>000001.SZ</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
      <td>200202</td>
      <td>2002</td>
      <td>2</td>
    </tr>
    <tr>
      <th>20020228</th>
      <td>000001.SZ</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
      <td>200202</td>
      <td>2002</td>
      <td>2</td>
    </tr>
    <tr>
      <th>20020301</th>
      <td>000001.SZ</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
      <td>200203</td>
      <td>2002</td>
      <td>3</td>
    </tr>
    <tr>
      <th>20020304</th>
      <td>000001.SZ</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
      <td>200203</td>
      <td>2002</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



### 一个列分组


```python
#按年分组 并在年数据里聚合计算
df.groupby('year').sum()
#按年分组 并在年数据里聚合计算
df.groupby('month').mean()
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
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>yearmonth</th>
      <th>year</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>14.530095</td>
      <td>14.825460</td>
      <td>14.266286</td>
      <td>14.547556</td>
      <td>14.534667</td>
      <td>0.012889</td>
      <td>0.208231</td>
      <td>580894.996127</td>
      <td>844799.759243</td>
      <td>201128.619048</td>
      <td>2011.276190</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.401491</td>
      <td>14.676727</td>
      <td>14.167382</td>
      <td>14.426691</td>
      <td>14.405818</td>
      <td>0.020873</td>
      <td>0.196477</td>
      <td>487444.121673</td>
      <td>678270.267715</td>
      <td>201094.000000</td>
      <td>2010.920000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>14.050051</td>
      <td>14.305909</td>
      <td>13.822323</td>
      <td>14.059015</td>
      <td>14.071414</td>
      <td>-0.012399</td>
      <td>-0.034142</td>
      <td>491202.092273</td>
      <td>717821.759882</td>
      <td>201053.000000</td>
      <td>2010.500000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>14.340959</td>
      <td>14.633372</td>
      <td>14.098837</td>
      <td>14.381890</td>
      <td>14.336366</td>
      <td>0.045523</td>
      <td>0.347759</td>
      <td>546381.477355</td>
      <td>828757.370356</td>
      <td>200997.313953</td>
      <td>2009.933140</td>
    </tr>
    <tr>
      <th>5</th>
      <td>14.421786</td>
      <td>14.670552</td>
      <td>14.193214</td>
      <td>14.431558</td>
      <td>14.441364</td>
      <td>-0.009805</td>
      <td>-0.012078</td>
      <td>436813.773149</td>
      <td>648750.957009</td>
      <td>201063.441558</td>
      <td>2010.584416</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13.437816</td>
      <td>13.665063</td>
      <td>13.203038</td>
      <td>13.419747</td>
      <td>13.448228</td>
      <td>-0.028481</td>
      <td>-0.160886</td>
      <td>479926.414494</td>
      <td>692605.139097</td>
      <td>201026.886076</td>
      <td>2010.208861</td>
    </tr>
    <tr>
      <th>7</th>
      <td>13.491399</td>
      <td>13.764315</td>
      <td>13.283411</td>
      <td>13.536618</td>
      <td>13.496064</td>
      <td>0.040554</td>
      <td>0.170256</td>
      <td>551447.929708</td>
      <td>716875.367078</td>
      <td>201014.288630</td>
      <td>2010.072886</td>
    </tr>
    <tr>
      <th>8</th>
      <td>13.812323</td>
      <td>14.057734</td>
      <td>13.589490</td>
      <td>13.819065</td>
      <td>13.837564</td>
      <td>-0.018499</td>
      <td>-0.037379</td>
      <td>436201.828867</td>
      <td>555928.026961</td>
      <td>201013.382436</td>
      <td>2010.053824</td>
    </tr>
    <tr>
      <th>9</th>
      <td>13.579765</td>
      <td>13.788912</td>
      <td>13.362235</td>
      <td>13.564412</td>
      <td>13.582029</td>
      <td>-0.017176</td>
      <td>-0.106894</td>
      <td>371924.521706</td>
      <td>477253.756626</td>
      <td>201003.117647</td>
      <td>2009.941176</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14.143813</td>
      <td>14.438201</td>
      <td>13.914029</td>
      <td>14.168201</td>
      <td>14.123705</td>
      <td>0.044496</td>
      <td>0.166892</td>
      <td>472102.846295</td>
      <td>614200.592490</td>
      <td>201035.899281</td>
      <td>2010.258993</td>
    </tr>
    <tr>
      <th>11</th>
      <td>13.933077</td>
      <td>14.185769</td>
      <td>13.698434</td>
      <td>13.936154</td>
      <td>13.957143</td>
      <td>-0.020989</td>
      <td>0.071548</td>
      <td>543677.344863</td>
      <td>710758.440917</td>
      <td>201014.021978</td>
      <td>2010.030220</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13.660027</td>
      <td>13.905109</td>
      <td>13.459701</td>
      <td>13.682092</td>
      <td>13.663696</td>
      <td>0.018397</td>
      <td>0.108443</td>
      <td>546453.187310</td>
      <td>751905.026304</td>
      <td>201008.739130</td>
      <td>2009.967391</td>
    </tr>
  </tbody>
</table>
</div>



### 多列 grupby


```python
#分组数列作为数据，不作为index，不启用multiIndex
df.groupby(['year','month'],as_index=False).mean()
#multiindex
df.groupby(['year','month']).mean()
df.groupby(['month','year']).mean()
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
      <th></th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>yearmonth</th>
    </tr>
    <tr>
      <th>month</th>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">1</th>
      <th>2003</th>
      <td>10.887000</td>
      <td>11.125000</td>
      <td>10.743500</td>
      <td>10.949000</td>
      <td>10.892000</td>
      <td>0.057000</td>
      <td>0.557500</td>
      <td>1.240784e+05</td>
      <td>1.382769e+05</td>
      <td>200301</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>9.132308</td>
      <td>9.319231</td>
      <td>9.006154</td>
      <td>9.177692</td>
      <td>9.118462</td>
      <td>0.059231</td>
      <td>0.695385</td>
      <td>1.274250e+05</td>
      <td>1.176096e+05</td>
      <td>200401</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>6.391053</td>
      <td>6.452632</td>
      <td>6.261579</td>
      <td>6.352632</td>
      <td>6.380526</td>
      <td>-0.027895</td>
      <td>-0.417368</td>
      <td>3.034601e+04</td>
      <td>1.918823e+04</td>
      <td>200501</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>6.245000</td>
      <td>6.318125</td>
      <td>6.180000</td>
      <td>6.260000</td>
      <td>6.246875</td>
      <td>0.013125</td>
      <td>0.218125</td>
      <td>1.092179e+05</td>
      <td>6.851705e+04</td>
      <td>200601</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>16.443500</td>
      <td>16.878000</td>
      <td>16.045500</td>
      <td>16.494000</td>
      <td>16.261000</td>
      <td>0.233000</td>
      <td>1.485500</td>
      <td>5.096216e+05</td>
      <td>8.391696e+05</td>
      <td>200701</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">12</th>
      <th>2014</th>
      <td>14.223913</td>
      <td>14.869130</td>
      <td>13.820870</td>
      <td>14.405217</td>
      <td>14.257391</td>
      <td>0.147826</td>
      <td>1.147391</td>
      <td>2.927762e+06</td>
      <td>4.189924e+06</td>
      <td>201412</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>12.105652</td>
      <td>12.304348</td>
      <td>11.989130</td>
      <td>12.140435</td>
      <td>12.129565</td>
      <td>0.010870</td>
      <td>0.110435</td>
      <td>7.025689e+05</td>
      <td>8.577838e+05</td>
      <td>201512</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>9.319545</td>
      <td>9.364091</td>
      <td>9.251818</td>
      <td>9.304545</td>
      <td>9.325000</td>
      <td>-0.020455</td>
      <td>-0.216818</td>
      <td>5.918154e+05</td>
      <td>5.554954e+05</td>
      <td>201612</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>13.170476</td>
      <td>13.400000</td>
      <td>12.975714</td>
      <td>13.191905</td>
      <td>13.195714</td>
      <td>-0.003810</td>
      <td>-0.005714</td>
      <td>1.412468e+06</td>
      <td>1.863948e+06</td>
      <td>201712</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>10.026500</td>
      <td>10.099000</td>
      <td>9.910000</td>
      <td>9.979500</td>
      <td>10.028500</td>
      <td>-0.049000</td>
      <td>-0.486650</td>
      <td>5.996672e+05</td>
      <td>5.987081e+05</td>
      <td>201812</td>
    </tr>
  </tbody>
</table>
<p>205 rows × 10 columns</p>
</div>



### 同时多统计数据


```python
df.groupby('month')['close'].agg([np.sum,np.mean])
df.groupby(['year','month'])['close'].agg([np.sum,np.mean])
df.groupby(['year','month'])[['close','open']].agg([np.sum,np.mean])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">close</th>
      <th colspan="2" halign="left">open</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>sum</th>
      <th>mean</th>
      <th>sum</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>year</th>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2002</th>
      <th>2</th>
      <td>30.66</td>
      <td>10.220000</td>
      <td>30.91</td>
      <td>10.303333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>237.51</td>
      <td>11.310000</td>
      <td>236.92</td>
      <td>11.281905</td>
    </tr>
    <tr>
      <th>4</th>
      <td>228.74</td>
      <td>10.892381</td>
      <td>228.22</td>
      <td>10.867619</td>
    </tr>
    <tr>
      <th>5</th>
      <td>191.16</td>
      <td>11.244706</td>
      <td>191.47</td>
      <td>11.262941</td>
    </tr>
    <tr>
      <th>6</th>
      <td>242.13</td>
      <td>12.106500</td>
      <td>240.53</td>
      <td>12.026500</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2018</th>
      <th>12</th>
      <td>199.59</td>
      <td>9.979500</td>
      <td>200.53</td>
      <td>10.026500</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">2019</th>
      <th>1</th>
      <td>225.85</td>
      <td>10.265909</td>
      <td>224.41</td>
      <td>10.200455</td>
    </tr>
    <tr>
      <th>2</th>
      <td>173.63</td>
      <td>11.575333</td>
      <td>172.60</td>
      <td>11.506667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>264.27</td>
      <td>12.584286</td>
      <td>263.53</td>
      <td>12.549048</td>
    </tr>
    <tr>
      <th>4</th>
      <td>67.80</td>
      <td>13.560000</td>
      <td>66.65</td>
      <td>13.330000</td>
    </tr>
  </tbody>
</table>
<p>205 rows × 4 columns</p>
</div>



## for group 类理解流程

- key分组 得到name和group本身（series、dataframe）计算函数 并合并结果



```python
df.groupby('year')['close'].max()
```




    year
    2002    15.68
    2003    13.77
    2004    11.31
    2005     6.94
    2006    14.47
    2007    48.05
    2008    44.08
    2009    26.22
    2010    23.85
    2011    18.87
    2012    17.48
    2013    24.25
    2014    15.84
    2015    19.80
    2016    11.53
    2017    15.10
    2018    14.80
    2019    13.96
    Name: close, dtype: float64



# 十七、分层索引怎么用 multiIndex
## 1.series 分层索引

- df.groupby(['year','month'])['close'].max()
- 产生year month 两级索引的 *series* 
- index 是两级索引的元组 
- unstack 将两级索引变成列，series变成dataframe，一级索引变成index，二级索引变成columns，间谍索引层次
- reset_index 将两层索引变成普通列


```python
dft = df.groupby(['year','month'])['close'].max()
dft.head()
```




    year  month
    2002  2        10.31
          3        11.94
          4        11.50
          5        11.80
          6        15.00
    Name: close, dtype: float64




```python
dft.loc[(2002,3)]
dft.unstack()
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
      <th>month</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2002</th>
      <td>NaN</td>
      <td>10.31</td>
      <td>11.94</td>
      <td>11.50</td>
      <td>11.80</td>
      <td>15.00</td>
      <td>15.15</td>
      <td>15.68</td>
      <td>15.59</td>
      <td>13.54</td>
      <td>13.70</td>
      <td>11.79</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>11.63</td>
      <td>11.42</td>
      <td>11.79</td>
      <td>13.77</td>
      <td>12.80</td>
      <td>12.48</td>
      <td>11.39</td>
      <td>10.95</td>
      <td>10.42</td>
      <td>9.40</td>
      <td>8.69</td>
      <td>9.04</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>9.53</td>
      <td>11.12</td>
      <td>11.31</td>
      <td>10.73</td>
      <td>9.62</td>
      <td>9.94</td>
      <td>8.76</td>
      <td>8.19</td>
      <td>8.93</td>
      <td>8.24</td>
      <td>7.41</td>
      <td>7.09</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>6.59</td>
      <td>6.74</td>
      <td>6.44</td>
      <td>6.94</td>
      <td>6.31</td>
      <td>6.58</td>
      <td>6.07</td>
      <td>6.47</td>
      <td>6.38</td>
      <td>6.34</td>
      <td>5.88</td>
      <td>6.23</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>6.41</td>
      <td>7.03</td>
      <td>6.78</td>
      <td>7.88</td>
      <td>8.78</td>
      <td>7.90</td>
      <td>8.10</td>
      <td>7.28</td>
      <td>8.16</td>
      <td>9.82</td>
      <td>12.88</td>
      <td>14.47</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>20.14</td>
      <td>20.80</td>
      <td>19.95</td>
      <td>25.95</td>
      <td>29.24</td>
      <td>35.40</td>
      <td>36.23</td>
      <td>40.01</td>
      <td>39.98</td>
      <td>48.05</td>
      <td>47.20</td>
      <td>39.80</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>44.08</td>
      <td>37.93</td>
      <td>33.00</td>
      <td>30.00</td>
      <td>29.62</td>
      <td>25.87</td>
      <td>21.80</td>
      <td>21.88</td>
      <td>18.96</td>
      <td>13.99</td>
      <td>11.01</td>
      <td>11.24</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>11.79</td>
      <td>15.15</td>
      <td>16.52</td>
      <td>16.75</td>
      <td>18.18</td>
      <td>22.59</td>
      <td>26.18</td>
      <td>25.85</td>
      <td>21.98</td>
      <td>22.81</td>
      <td>26.22</td>
      <td>25.50</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>23.71</td>
      <td>22.58</td>
      <td>23.85</td>
      <td>23.43</td>
      <td>20.00</td>
      <td>18.53</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18.20</td>
      <td>19.55</td>
      <td>19.14</td>
      <td>16.74</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>16.41</td>
      <td>16.00</td>
      <td>16.74</td>
      <td>18.87</td>
      <td>18.34</td>
      <td>17.43</td>
      <td>17.99</td>
      <td>17.38</td>
      <td>17.06</td>
      <td>17.03</td>
      <td>17.12</td>
      <td>16.05</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>16.78</td>
      <td>17.25</td>
      <td>17.48</td>
      <td>16.86</td>
      <td>16.78</td>
      <td>15.78</td>
      <td>15.28</td>
      <td>15.26</td>
      <td>14.21</td>
      <td>13.51</td>
      <td>13.62</td>
      <td>16.02</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>21.38</td>
      <td>23.00</td>
      <td>24.25</td>
      <td>20.45</td>
      <td>21.60</td>
      <td>21.13</td>
      <td>10.51</td>
      <td>11.00</td>
      <td>13.47</td>
      <td>14.40</td>
      <td>14.09</td>
      <td>13.75</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>12.23</td>
      <td>12.22</td>
      <td>11.04</td>
      <td>11.40</td>
      <td>11.60</td>
      <td>11.78</td>
      <td>10.87</td>
      <td>10.93</td>
      <td>10.57</td>
      <td>11.03</td>
      <td>12.44</td>
      <td>15.84</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>16.02</td>
      <td>14.07</td>
      <td>15.75</td>
      <td>19.80</td>
      <td>16.62</td>
      <td>17.29</td>
      <td>14.86</td>
      <td>12.92</td>
      <td>11.84</td>
      <td>11.52</td>
      <td>12.94</td>
      <td>12.51</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>11.53</td>
      <td>10.29</td>
      <td>10.80</td>
      <td>10.88</td>
      <td>10.72</td>
      <td>10.52</td>
      <td>9.20</td>
      <td>9.68</td>
      <td>9.45</td>
      <td>9.24</td>
      <td>9.63</td>
      <td>9.65</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>9.33</td>
      <td>9.57</td>
      <td>9.52</td>
      <td>9.21</td>
      <td>9.20</td>
      <td>9.43</td>
      <td>11.09</td>
      <td>11.67</td>
      <td>11.72</td>
      <td>11.69</td>
      <td>15.10</td>
      <td>13.66</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>14.80</td>
      <td>14.55</td>
      <td>12.11</td>
      <td>11.86</td>
      <td>11.18</td>
      <td>10.37</td>
      <td>9.42</td>
      <td>10.43</td>
      <td>11.05</td>
      <td>11.29</td>
      <td>11.09</td>
      <td>10.59</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>11.10</td>
      <td>12.55</td>
      <td>13.08</td>
      <td>13.96</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
dft.reset_index()
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
      <th>year</th>
      <th>month</th>
      <th>close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2002</td>
      <td>2</td>
      <td>10.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002</td>
      <td>3</td>
      <td>11.94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002</td>
      <td>4</td>
      <td>11.50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002</td>
      <td>5</td>
      <td>11.80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002</td>
      <td>6</td>
      <td>15.00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>200</th>
      <td>2018</td>
      <td>12</td>
      <td>10.59</td>
    </tr>
    <tr>
      <th>201</th>
      <td>2019</td>
      <td>1</td>
      <td>11.10</td>
    </tr>
    <tr>
      <th>202</th>
      <td>2019</td>
      <td>2</td>
      <td>12.55</td>
    </tr>
    <tr>
      <th>203</th>
      <td>2019</td>
      <td>3</td>
      <td>13.08</td>
    </tr>
    <tr>
      <th>204</th>
      <td>2019</td>
      <td>4</td>
      <td>13.96</td>
    </tr>
  </tbody>
</table>
<p>205 rows × 3 columns</p>
</div>



## 2.Series 多层索引筛选数据

- 只用一级 只用二级 一二联用


```python
dft.head()
```




    year  month
    2002  2        10.31
          3        11.94
          4        11.50
          5        11.80
          6        15.00
    Name: close, dtype: float64




```python
dft.loc[2002]
dft.loc[:,2]
dft.loc[2002,2]
```




    year
    2002    10.31
    2003    11.42
    2004    11.12
    2005     6.74
    2006     7.03
    2007    20.80
    2008    37.93
    2009    15.15
    2010    22.58
    2011    16.00
    2012    17.25
    2013    23.00
    2014    12.22
    2015    14.07
    2016    10.29
    2017     9.57
    2018    14.55
    2019    12.55
    Name: close, dtype: float64



## 3.df的多层索引

- df.set_index(['a','b'],replace=True)
  - 将a b 设为分层索引
    .sort_index(inplace=True) #排序


```python
dft = df.groupby(['year','month'])[['close','open']].max()
```


```python
df.set_index(['year','month'],inplace=True)
df.sort_index(inplace=True)
df.head()
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
      <th></th>
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>yearmonth</th>
    </tr>
    <tr>
      <th>year</th>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2002</th>
      <th>2</th>
      <td>000001.SZ</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>2</th>
      <td>000001.SZ</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>2</th>
      <td>000001.SZ</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>3</th>
      <td>000001.SZ</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
      <td>200203</td>
    </tr>
    <tr>
      <th>3</th>
      <td>000001.SZ</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
      <td>200203</td>
    </tr>
  </tbody>
</table>
</div>



## 4.df多层索引筛选数据

- 元组代表索引 
- 列表表示多个key 同级别索引



```python
df.loc[2002]
df.loc[[(2002,3),(2003,4)]]
df.loc[[(2002,3),(2003,4)]]['close']
df.loc[([2002,2003],[3,4]),:]
df.loc[(slice(None),[3,4]),:]#一级索引的全部
df.reset_index(inplace=True)
df.head()
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
      <th>year</th>
      <th>month</th>
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>yearmonth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002</td>
      <td>3</td>
      <td>000001.SZ</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
      <td>200203</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002</td>
      <td>3</td>
      <td>000001.SZ</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
      <td>200203</td>
    </tr>
  </tbody>
</table>
</div>



# 十八、数据转换函数

- map series上每个值
- apply 
  - series同上 
  - dataframe 轴上series
- applymap 所有数据

## 1.map 字典 函数变换


```python
df_sco2.head()
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
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
      <th>备注</th>
      <th>身高2</th>
      <th>身高3</th>
      <th>名字2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>172CM</td>
      <td>65kg</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>*'172CM '*</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>wang wuwu</td>
      <td>175CM</td>
      <td>48KG</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>*'175CM'*</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>165CM</td>
      <td>45KG</td>
      <td>劳动委员</td>
      <td>NaN</td>
      <td>*'165CM '*</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
      <td>NaN</td>
      <td>*nan*</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
dic = {'王五五':'wang wuwu'}
df_sco2['名字2'] = df_sco2['名字'].str.lower().map(dic)
df_sco2['身高3'] = df_sco2['身高'].map(lambda x:'*%r*'%x)
df_sco2.head()
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
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
      <th>备注</th>
      <th>名字2</th>
      <th>身高3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>李四</td>
      <td>172CM</td>
      <td>65kg</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>*'172CM '*</td>
    </tr>
    <tr>
      <th>1</th>
      <td>王五五</td>
      <td>175CM</td>
      <td>48KG</td>
      <td>NaN</td>
      <td>wang wuwu</td>
      <td>*'175CM'*</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>165CM</td>
      <td>45KG</td>
      <td>劳动委员</td>
      <td>NaN</td>
      <td>*'165CM '*</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
      <td>NaN</td>
      <td>*nan*</td>
    </tr>
  </tbody>
</table>
</div>



## apply

- series.apply(func)

- df.appaly(func,axis0


```python
df_sco2.head()
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
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
      <th>备注</th>
      <th>名字2</th>
      <th>身高3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>李四</td>
      <td>172CM</td>
      <td>65kg</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>*'172CM '*</td>
    </tr>
    <tr>
      <th>1</th>
      <td>王五五</td>
      <td>175CM</td>
      <td>48KG</td>
      <td>NaN</td>
      <td>wang wuwu</td>
      <td>*'175CM'*</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>165CM</td>
      <td>45KG</td>
      <td>劳动委员</td>
      <td>NaN</td>
      <td>*'165CM '*</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
      <td>NaN</td>
      <td>*nan*</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_sco2['名字2'] = df_sco2['名字'].apply(lambda x:x.startswith('赵'))
df_sco2['名字3'] = df_sco2.apply(lambda x:x['名字'].startswith('赵'),axis=1)
df_sco2.head()
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
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
      <th>备注</th>
      <th>名字2</th>
      <th>身高3</th>
      <th>名字3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>李四</td>
      <td>172CM</td>
      <td>65kg</td>
      <td>NaN</td>
      <td>False</td>
      <td>*'172CM '*</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>王五五</td>
      <td>175CM</td>
      <td>48KG</td>
      <td>NaN</td>
      <td>False</td>
      <td>*'175CM'*</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>赵六</td>
      <td>165CM</td>
      <td>45KG</td>
      <td>劳动委员</td>
      <td>True</td>
      <td>*'165CM '*</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>赵六</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>家在团结小区</td>
      <td>True</td>
      <td>*nan*</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
## 3.applymap df中所有值转换
```


```python
df_sco2.applymap(lambda x:'*%r*'%x).head()
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
      <th>名字</th>
      <th>身高</th>
      <th>体重</th>
      <th>备注</th>
      <th>名字2</th>
      <th>身高3</th>
      <th>名字3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>*'李四'*</td>
      <td>*'172CM '*</td>
      <td>*' 65kg '*</td>
      <td>*nan*</td>
      <td>*False*</td>
      <td>*"*'172CM '*"*</td>
      <td>*False*</td>
    </tr>
    <tr>
      <th>1</th>
      <td>*'王五五'*</td>
      <td>*'175CM'*</td>
      <td>*'48KG'*</td>
      <td>*nan*</td>
      <td>*False*</td>
      <td>*"*'175CM'*"*</td>
      <td>*False*</td>
    </tr>
    <tr>
      <th>2</th>
      <td>*'赵六'*</td>
      <td>*'165CM '*</td>
      <td>*'45KG '*</td>
      <td>*'劳动委员'*</td>
      <td>*True*</td>
      <td>*"*'165CM '*"*</td>
      <td>*True*</td>
    </tr>
    <tr>
      <th>3</th>
      <td>*'赵六'*</td>
      <td>*nan*</td>
      <td>*nan*</td>
      <td>*'家在团结小区'*</td>
      <td>*True*</td>
      <td>*'*nan*'*</td>
      <td>*True*</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_sco1.head()
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
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>89.5</td>
      <td>90</td>
      <td>98.0</td>
      <td>天成 皇家壹里 4-5-1001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>98.0</td>
      <td>120</td>
      <td>118.0</td>
      <td>成绩优秀 副班长</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王五五</td>
      <td>99.0</td>
      <td>111</td>
      <td>110.5</td>
      <td>体育特长生</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_sco1.loc[:,['语文','数学','英语']].applymap(lambda x:int(x)).head()
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
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>89</td>
      <td>90</td>
      <td>98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>98</td>
      <td>120</td>
      <td>118</td>
    </tr>
    <tr>
      <th>2</th>
      <td>99</td>
      <td>111</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>



# 十九、每个groupby分组应用apply函数

## 1.分组归一化

- 统计每月最大波动幅度


```python
df.head()
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
      <th>year</th>
      <th>month</th>
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>yearmonth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002</td>
      <td>3</td>
      <td>000001.SZ</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
      <td>200203</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002</td>
      <td>3</td>
      <td>000001.SZ</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
      <td>200203</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['month','year'])['close'].agg([np.min,np.max])
#归一化函数法
def normal(df):
    return df['close'].max()/df['close'].min()-1
df.groupby(['month','year']).apply(normal).unstack().mean(axis=1)
```




    month
    1     0.178797
    2     0.125523
    3     0.138662
    4     0.156706
    5     0.095569
    6     0.246883
    7     0.146618
    8     0.140665
    9     0.143135
    10    0.148805
    11    0.171224
    12    0.134950
    dtype: float64




## 2.分组TopN


```python
df.head()
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
      <th>year</th>
      <th>month</th>
      <th>ts_code</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>pre_close</th>
      <th>change</th>
      <th>pct_chg</th>
      <th>vol</th>
      <th>amount</th>
      <th>yearmonth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.40</td>
      <td>10.45</td>
      <td>10.08</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>-0.26</td>
      <td>-2.49</td>
      <td>45629.29</td>
      <td>46606.9685</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.20</td>
      <td>10.46</td>
      <td>10.20</td>
      <td>10.31</td>
      <td>10.20</td>
      <td>0.11</td>
      <td>1.08</td>
      <td>33362.16</td>
      <td>34486.1929</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002</td>
      <td>2</td>
      <td>000001.SZ</td>
      <td>10.31</td>
      <td>10.33</td>
      <td>10.13</td>
      <td>10.15</td>
      <td>10.31</td>
      <td>-0.16</td>
      <td>-1.55</td>
      <td>27547.67</td>
      <td>28132.6754</td>
      <td>200202</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002</td>
      <td>3</td>
      <td>000001.SZ</td>
      <td>10.15</td>
      <td>10.40</td>
      <td>10.10</td>
      <td>10.19</td>
      <td>10.15</td>
      <td>0.04</td>
      <td>0.39</td>
      <td>34547.67</td>
      <td>35315.7293</td>
      <td>200203</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002</td>
      <td>3</td>
      <td>000001.SZ</td>
      <td>10.19</td>
      <td>10.37</td>
      <td>10.11</td>
      <td>10.36</td>
      <td>10.19</td>
      <td>0.17</td>
      <td>1.67</td>
      <td>21196.51</td>
      <td>21749.7938</td>
      <td>200203</td>
    </tr>
  </tbody>
</table>
</div>




```python
def topN(df,n):
    return df.sort_values(by='close')[['open','close']][-n:]
df.groupby(['month','year']).apply(topN,2)
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
      <th></th>
      <th></th>
      <th>open</th>
      <th>close</th>
    </tr>
    <tr>
      <th>month</th>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">1</th>
      <th rowspan="2" valign="top">2003</th>
      <th>223</th>
      <td>11.60</td>
      <td>11.59</td>
    </tr>
    <tr>
      <th>224</th>
      <td>11.58</td>
      <td>11.63</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2004</th>
      <th>446</th>
      <td>9.40</td>
      <td>9.41</td>
    </tr>
    <tr>
      <th>453</th>
      <td>9.28</td>
      <td>9.53</td>
    </tr>
    <tr>
      <th>2005</th>
      <th>689</th>
      <td>6.53</td>
      <td>6.57</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">12</th>
      <th>2016</th>
      <th>3434</th>
      <td>9.50</td>
      <td>9.65</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2017</th>
      <th>3687</th>
      <td>13.18</td>
      <td>13.54</td>
    </tr>
    <tr>
      <th>3690</th>
      <td>13.26</td>
      <td>13.66</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2018</th>
      <th>3918</th>
      <td>10.57</td>
      <td>10.59</td>
    </tr>
    <tr>
      <th>3917</th>
      <td>10.59</td>
      <td>10.59</td>
    </tr>
  </tbody>
</table>
<p>410 rows × 2 columns</p>
</div>



# 二十、Stack和Pivot实现数据透视

- 列数据变成二维交叉形式，便于分析，称为透视、重塑

# 二十一、附录 
## 1.画图


```python
%matplotlib inline
dfw = df.groupby(['month','year']).apply(normal).unstack()
dfw.head()
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
      <th>year</th>
      <th>2002</th>
      <th>2003</th>
      <th>2004</th>
      <th>2005</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
      <th>2018</th>
      <th>2019</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>0.160679</td>
      <td>0.103009</td>
      <td>0.096506</td>
      <td>0.052545</td>
      <td>0.542113</td>
      <td>0.323724</td>
      <td>0.244984</td>
      <td>0.131202</td>
      <td>0.099866</td>
      <td>0.106860</td>
      <td>0.375804</td>
      <td>0.082301</td>
      <td>0.158351</td>
      <td>0.189886</td>
      <td>0.021906</td>
      <td>0.141975</td>
      <td>0.207835</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.015764</td>
      <td>0.052535</td>
      <td>0.149948</td>
      <td>0.106732</td>
      <td>0.139384</td>
      <td>0.246255</td>
      <td>0.234701</td>
      <td>0.299314</td>
      <td>0.063089</td>
      <td>0.049180</td>
      <td>0.048632</td>
      <td>0.202929</td>
      <td>0.108893</td>
      <td>0.041451</td>
      <td>0.076360</td>
      <td>0.033477</td>
      <td>0.244654</td>
      <td>0.146119</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.171737</td>
      <td>0.092678</td>
      <td>0.090646</td>
      <td>0.262745</td>
      <td>0.097087</td>
      <td>0.139349</td>
      <td>0.324769</td>
      <td>0.222798</td>
      <td>0.069507</td>
      <td>0.065563</td>
      <td>0.122672</td>
      <td>0.211289</td>
      <td>0.093069</td>
      <td>0.177130</td>
      <td>0.113402</td>
      <td>0.048458</td>
      <td>0.112029</td>
      <td>0.080992</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.097328</td>
      <td>0.166949</td>
      <td>0.168845</td>
      <td>0.280443</td>
      <td>0.233177</td>
      <td>0.345954</td>
      <td>0.338688</td>
      <td>0.105611</td>
      <td>0.196018</td>
      <td>0.138805</td>
      <td>0.071156</td>
      <td>0.106003</td>
      <td>0.066417</td>
      <td>0.253165</td>
      <td>0.036190</td>
      <td>0.033670</td>
      <td>0.123106</td>
      <td>0.059181</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.082569</td>
      <td>0.070234</td>
      <td>0.085779</td>
      <td>0.069492</td>
      <td>0.118471</td>
      <td>0.091045</td>
      <td>0.192432</td>
      <td>0.084726</td>
      <td>0.147447</td>
      <td>0.069388</td>
      <td>0.074264</td>
      <td>0.142253</td>
      <td>0.069124</td>
      <td>0.094862</td>
      <td>0.049951</td>
      <td>0.073512</td>
      <td>0.109127</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
dfw.mean(axis=1).plot()
dfw.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x8e7d640>




![png](output_84_1.png)



![png](output_84_2.png)



```python
df = df.to_period('M')#Q A
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-3-75a6083c6a62> in <module>
    ----> 1 df = df.to_period('M')#Q A
    

    d:\ProgramData\Anaconda3\lib\site-packages\pandas\core\frame.py in to_period(self, freq, axis, copy)
       8342         axis = self._get_axis_number(axis)
       8343         if axis == 0:
    -> 8344             new_data.set_axis(1, self.index.to_period(freq=freq))
       8345         elif axis == 1:
       8346             new_data.set_axis(0, self.columns.to_period(freq=freq))
    

    AttributeError: 'RangeIndex' object has no attribute 'to_period'



```python

```
