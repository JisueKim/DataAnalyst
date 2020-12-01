# [Pandas 기초] 시계열 데이터(timeseries), Timestamp 와 Period

```python
import pandas as pd 
df = pd.read_csv("/Users/jisuekim/Desktop/JSK/data/funda_train.csv")
```


```python
df.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>card_id</th>
      <th>card_company</th>
      <th>transacted_date</th>
      <th>transacted_time</th>
      <th>installment_term</th>
      <th>region</th>
      <th>type_of_business</th>
      <th>amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>b</td>
      <td>2016-06-01</td>
      <td>13:13</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1857.142857</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>h</td>
      <td>2016-06-01</td>
      <td>18:12</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>857.142857</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>2</td>
      <td>c</td>
      <td>2016-06-01</td>
      <td>18:52</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>3</td>
      <td>a</td>
      <td>2016-06-01</td>
      <td>20:22</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>7857.142857</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>4</td>
      <td>c</td>
      <td>2016-06-02</td>
      <td>11:06</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
    </tr>
  </tbody>
</table>
## 1. 시계열 데이터

판다스에서 시계열 자료형은 Timestamp와 Period라는 두가지 타입이 있다.

> Timestamp 자료형은 `to_datetime()`함수로 생성가능하며 날짜형태의 자료형을 시계열 타입으로 변환해준다.
> Period 자료형은 Timestamp(datetime)객체를 다시 기간에 따른 자료형으로 이용하고자 할때 사용한다.

## 2. 자료형의 시계열 객체 변환 : `to_datetime()` , `to_period()`


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 6556613 entries, 0 to 6556612
    Data columns (total 9 columns):
     #   Column            Dtype  
    ---  ------            -----  
     0   store_id          int64  
     1   card_id           int64  
     2   card_company      object 
     3   transacted_date   object 
     4   transacted_time   object 
     5   installment_term  int64  
     6   region            object 
     7   type_of_business  object 
     8   amount            float64
    dtypes: float64(1), int64(3), object(5)
    memory usage: 450.2+ MB

현재 날짜를 나타내는 Date컬럼은 문자형(object)임을 알 수 있다.

`to_datetime()`함수를 이용해서 Date컬럼을 시계열 객체(Timestamp)로 변환해보자.


```python
df['transacted_date_new'] = pd.to_datetime(df['transacted_date'])

df.info()
print('\n')
print(type(df['transacted_date_new'][0]))
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 6556613 entries, 0 to 6556612
    Data columns (total 10 columns):
     #   Column               Dtype         
    ---  ------               -----         
     0   store_id             int64         
     1   card_id              int64         
     2   card_company         object        
     3   transacted_date      object        
     4   transacted_time      object        
     5   installment_term     int64         
     6   region               object        
     7   type_of_business     object        
     8   amount               float64       
     9   transacted_date_new  datetime64[ns]
    dtypes: datetime64[ns](1), float64(1), int64(3), object(5)
    memory usage: 500.2+ MB

    <class 'pandas._libs.tslibs.timestamps.Timestamp'>

이번에는 Timestamp와 Period의 차이를 알아보자.


```python
# Timestamp를 Period로 변환
dates = ['2019-01-01','2020-03-01','2021-06-01']
ts_dates = pd.to_datetime(dates)
print(ts_dates)
print('\n')

# Timestamp를 Period변환
pr_day = ts_dates.to_period(freq='D')   #1일의 기간
print(pr_day)
pr_month = ts_dates.to_period(freq='M') #1개월의 기간
print(pr_month)
pr_year = ts_dates.to_period(freq='A')  #1년의 기간
print(pr_year)
```

    DatetimeIndex(['2019-01-01', '2020-03-01', '2021-06-01'], dtype='datetime64[ns]', freq=None)

    PeriodIndex(['2019-01-01', '2020-03-01', '2021-06-01'], dtype='period[D]', freq='D')
    PeriodIndex(['2019-01', '2020-03', '2021-06'], dtype='period[M]', freq='M')
    PeriodIndex(['2019', '2020', '2021'], dtype='period[A-DEC]', freq='A-DEC')


보는 바와 같이 Period객체는 to_period(freq='기간인수')를 통해 datetime변수에 대해 어떤 기간에 따른 자료형을 생성하고자 할때 주로 활용된다. 이는 바로 아무 자료형에나 사용할 수 없고 datetime타입에 대해 적용가능하다.

## 3. 시계열 데이터 만들기 : `date_range()` , `period_range()`

### 3-1. Timestamp 배열

Timestamp를 배열하는 `date_range()`함수는 파이선의 [내장함수](https://yganalyst.github.io/data_handling/Py_study16/)인 range()함수와 비슷한 개념이다.

다음과 같이 옵션을 설정해주면 원하는 Timestamp(datetime)배열을 얻을 수 있다.


```python
import pandas as pd
ts_ms = pd.date_range(start = '2019-01-01',     # 날짜 범위 시작
                     end = None,                # 날짜 범위 끝
                     periods = 6,               # 생성할 Timestamp 개수
                     freq = 'MS',               # 시간 간격(MS : 월의 시작일)
                     tz = 'Asia/Seoul')         # 시간대(timezone)
print(ts_ms)
```

    DatetimeIndex(['2019-01-01 00:00:00+09:00', '2019-02-01 00:00:00+09:00',
                   '2019-03-01 00:00:00+09:00', '2019-04-01 00:00:00+09:00',
                   '2019-05-01 00:00:00+09:00', '2019-06-01 00:00:00+09:00'],
                  dtype='datetime64[ns, Asia/Seoul]', freq='MS')

2019년01월01일부터 월의 시작일 간격으로 6개를 생성했다.
이렇게 `freq=`옵션을 통해 유연한 배열의 생성이 가능하다.

이번에는 월 간격, 월의 마지막 날 기준(`freq='M'`)으로 생성하기 위한 옵션이다.

```
ts_me = pd.date_range('2019-01-01',
```


```python
ts_me = pd.date_range('2019-01-01',
                     periods = 6,
                     freq = 'M',            #1개월 간격, 월의 마지막날 기준
                     tz = 'Asia/Seoul')   
print(ts_me)
print('\n')


ts_3m = pd.date_range('2019-01-01',
                     periods = 6,
                     freq = '3M',           # 3개월 간격, 월의 마지막 날 기준
                     tz = 'Asia/Seoul')
print(ts_3m)
print('\n')
```

    DatetimeIndex(['2019-01-31 00:00:00+09:00', '2019-02-28 00:00:00+09:00',
                   '2019-03-31 00:00:00+09:00', '2019-04-30 00:00:00+09:00',
                   '2019-05-31 00:00:00+09:00', '2019-06-30 00:00:00+09:00'],
                  dtype='datetime64[ns, Asia/Seoul]', freq='M')

    DatetimeIndex(['2019-01-31 00:00:00+09:00', '2019-04-30 00:00:00+09:00',
                   '2019-07-31 00:00:00+09:00', '2019-10-31 00:00:00+09:00',
                   '2020-01-31 00:00:00+09:00', '2020-04-30 00:00:00+09:00'],
                  dtype='datetime64[ns, Asia/Seoul]', freq='3M')

### 3-2. Period 배열

마찬가지로 Period 배열을 생성해주는 `period_range()`함수를 알아보자.
Timestamp와의 차이는 Period는 기간을 나타내는 자료형 이므로, 배열을 적용할때 `freq=`옵션은 기간의 단위를 의미한다는 점이다.


```python
# 1개월 길이
pr_m = pd.period_range(start = '2019-01-01',
                   	   end = None,
                       periods = 3,
                       freq = 'M')           
print(pr_m)
print('\n')

# 1시간 길이
pr_h = pd.period_range(start = '2019-01-01',
                       end = None,
                       periods = 3,
                       freq = 'H')           
print(pr_h)
print('\n')

# 2시간 길이
pr_2h = pd.period_range(start = '2019-01-01',
                        end = None,
                        periods = 3,
                        freq = '2H')          
print(pr_2h)
```

    PeriodIndex(['2019-01', '2019-02', '2019-03'], dtype='period[M]', freq='M')

    PeriodIndex(['2019-01-01 00:00', '2019-01-01 01:00', '2019-01-01 02:00'], dtype='period[H]', freq='H')

    PeriodIndex(['2019-01-01 00:00', '2019-01-01 02:00', '2019-01-01 04:00'], dtype='period[2H]', freq='2H')

## 4. 시계열데이터 활용

### 4-1. 날짜 데이터 분리 : `dt.year`, `dt.month`, `dt.day`

datetime타입에 적용하는 `dt`속성을 활용해 연(year), 월(month), 일(day)을 날짜에서 분리해보자.


```python
df['Year'] = df['transacted_date_new'].dt.year
df['Month'] = df['transacted_date_new'].dt.month
df['Day'] = df['transacted_date_new'].dt.day
df.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>card_id</th>
      <th>card_company</th>
      <th>transacted_time</th>
      <th>installment_term</th>
      <th>region</th>
      <th>type_of_business</th>
      <th>amount</th>
      <th>transacted_date_new</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>b</td>
      <td>13:13</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1857.142857</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>h</td>
      <td>18:12</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>857.142857</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>2</td>
      <td>c</td>
      <td>18:52</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>3</td>
      <td>a</td>
      <td>20:22</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>7857.142857</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>4</td>
      <td>c</td>
      <td>11:06</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2016-06-02</td>
      <td>2016</td>
      <td>6</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
이번에는 아까 배운 `to_period()`함수를 이용해 표기를 변경해보자


```python
df['Date_yr'] = df['transacted_date_new'].dt.to_period(freq = 'A')  # 연도까지
df['Date_m'] = df['transacted_date_new'].dt.to_period(freq = 'M')   # 연월까지
df.head()
```

### 4-2. 날짜 인덱스 활용

이번에는 시계열 타입을 인덱스로 두고 활용하는 방법에 대해 알아보자.

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>card_id</th>
      <th>card_company</th>
      <th>transacted_time</th>
      <th>installment_term</th>
      <th>region</th>
      <th>type_of_business</th>
      <th>amount</th>
      <th>transacted_date_new</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
      <th>Date_m</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>b</td>
      <td>13:13</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1857.142857</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>h</td>
      <td>18:12</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>857.142857</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>2</td>
      <td>c</td>
      <td>18:52</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>3</td>
      <td>a</td>
      <td>20:22</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>7857.142857</td>
      <td>2016-06-01</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>4</td>
      <td>c</td>
      <td>11:06</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2016-06-02</td>
      <td>2016</td>
      <td>6</td>
      <td>2</td>
      <td>2016</td>
      <td>2016-06</td>
    </tr>
  </tbody>
</table>
시계열 타입이 인덱스인 경우에는, 꼭 인덱스이름과 같지 않아도 특정 연도, 연도(2018), 연월(2018-07), 연월일(2018-07-02) 등과 같이 인덱싱이 가능하다.


```python
df1 = df.copy()
df1.set_index('transacted_date_new', inplace=True)
```


```python
df1['2018-06' : '2018-07']     # 해당기간의 인덱싱
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>card_id</th>
      <th>card_company</th>
      <th>transacted_time</th>
      <th>installment_term</th>
      <th>region</th>
      <th>type_of_business</th>
      <th>amount</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
      <th>Date_m</th>
    </tr>
    <tr>
      <th>transacted_date_new</th>
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
      <th>2018-06-01</th>
      <td>0</td>
      <td>1247</td>
      <td>b</td>
      <td>12:19</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1857.142857</td>
      <td>2018</td>
      <td>6</td>
      <td>1</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-01</th>
      <td>0</td>
      <td>265</td>
      <td>c</td>
      <td>17:17</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2018</td>
      <td>6</td>
      <td>1</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-02</th>
      <td>0</td>
      <td>869</td>
      <td>c</td>
      <td>10:05</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2018</td>
      <td>6</td>
      <td>2</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-02</th>
      <td>0</td>
      <td>741</td>
      <td>b</td>
      <td>14:26</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>14285.714286</td>
      <td>2018</td>
      <td>6</td>
      <td>2</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-02</th>
      <td>0</td>
      <td>1410</td>
      <td>g</td>
      <td>16:18</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1428.571429</td>
      <td>2018</td>
      <td>6</td>
      <td>2</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2018-07-31</th>
      <td>2136</td>
      <td>4659367</td>
      <td>b</td>
      <td>21:00</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>5571.428571</td>
      <td>2018</td>
      <td>7</td>
      <td>31</td>
      <td>2018</td>
      <td>2018-07</td>
    </tr>
    <tr>
      <th>2018-07-31</th>
      <td>2136</td>
      <td>4662422</td>
      <td>d</td>
      <td>22:58</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>8142.857143</td>
      <td>2018</td>
      <td>7</td>
      <td>31</td>
      <td>2018</td>
      <td>2018-07</td>
    </tr>
    <tr>
      <th>2018-07-31</th>
      <td>2136</td>
      <td>4662423</td>
      <td>a</td>
      <td>23:20</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>5142.857143</td>
      <td>2018</td>
      <td>7</td>
      <td>31</td>
      <td>2018</td>
      <td>2018-07</td>
    </tr>
    <tr>
      <th>2018-07-31</th>
      <td>2136</td>
      <td>4662424</td>
      <td>e</td>
      <td>23:44</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>6142.857143</td>
      <td>2018</td>
      <td>7</td>
      <td>31</td>
      <td>2018</td>
      <td>2018-07</td>
    </tr>
    <tr>
      <th>2018-07-31</th>
      <td>2136</td>
      <td>4662425</td>
      <td>d</td>
      <td>23:52</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>6571.428571</td>
      <td>2018</td>
      <td>7</td>
      <td>31</td>
      <td>2018</td>
      <td>2018-07</td>
    </tr>
  </tbody>
</table>
<p>445443 rows × 13 columns</p>

```python
df1.loc['2018-06'] # 연,월 인덱싱
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>card_id</th>
      <th>card_company</th>
      <th>transacted_time</th>
      <th>installment_term</th>
      <th>region</th>
      <th>type_of_business</th>
      <th>amount</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
      <th>Date_m</th>
    </tr>
    <tr>
      <th>transacted_date_new</th>
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
      <th>2018-06-01</th>
      <td>0</td>
      <td>1247</td>
      <td>b</td>
      <td>12:19</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1857.142857</td>
      <td>2018</td>
      <td>6</td>
      <td>1</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-01</th>
      <td>0</td>
      <td>265</td>
      <td>c</td>
      <td>17:17</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2018</td>
      <td>6</td>
      <td>1</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-02</th>
      <td>0</td>
      <td>869</td>
      <td>c</td>
      <td>10:05</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2018</td>
      <td>6</td>
      <td>2</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-02</th>
      <td>0</td>
      <td>741</td>
      <td>b</td>
      <td>14:26</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>14285.714286</td>
      <td>2018</td>
      <td>6</td>
      <td>2</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-02</th>
      <td>0</td>
      <td>1410</td>
      <td>g</td>
      <td>16:18</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1428.571429</td>
      <td>2018</td>
      <td>6</td>
      <td>2</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2018-06-30</th>
      <td>2136</td>
      <td>4662239</td>
      <td>b</td>
      <td>23:15</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>4571.428571</td>
      <td>2018</td>
      <td>6</td>
      <td>30</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-30</th>
      <td>2136</td>
      <td>4662240</td>
      <td>h</td>
      <td>23:23</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>6000.000000</td>
      <td>2018</td>
      <td>6</td>
      <td>30</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-30</th>
      <td>2136</td>
      <td>4662241</td>
      <td>c</td>
      <td>23:34</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>5000.000000</td>
      <td>2018</td>
      <td>6</td>
      <td>30</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-30</th>
      <td>2136</td>
      <td>4662242</td>
      <td>d</td>
      <td>23:54</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>9000.000000</td>
      <td>2018</td>
      <td>6</td>
      <td>30</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
    <tr>
      <th>2018-06-30</th>
      <td>2136</td>
      <td>4662243</td>
      <td>c</td>
      <td>23:55</td>
      <td>0</td>
      <td>제주 제주시</td>
      <td>기타 주점업</td>
      <td>3571.428571</td>
      <td>2018</td>
      <td>6</td>
      <td>30</td>
      <td>2018</td>
      <td>2018-06</td>
    </tr>
  </tbody>
</table>
<p>224308 rows × 13 columns</p>
### 4-3. 오늘과의 날짜 차이 열 만들기

오늘 날짜를 2019-07-18이라고 하고 경과일을 구해보자.


```python
today = pd.to_datetime('2020-12-01')
df1['time-delta'] = today - df1.index
df1.head()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>store_id</th>
      <th>card_id</th>
      <th>card_company</th>
      <th>transacted_time</th>
      <th>installment_term</th>
      <th>region</th>
      <th>type_of_business</th>
      <th>amount</th>
      <th>Year</th>
      <th>Month</th>
      <th>Day</th>
      <th>Date_yr</th>
      <th>Date_m</th>
      <th>time-delta</th>
    </tr>
    <tr>
      <th>transacted_date_new</th>
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
      <th>2016-06-01</th>
      <td>0</td>
      <td>0</td>
      <td>b</td>
      <td>13:13</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>1857.142857</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
      <td>1644 days</td>
    </tr>
    <tr>
      <th>2016-06-01</th>
      <td>0</td>
      <td>1</td>
      <td>h</td>
      <td>18:12</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>857.142857</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
      <td>1644 days</td>
    </tr>
    <tr>
      <th>2016-06-01</th>
      <td>0</td>
      <td>2</td>
      <td>c</td>
      <td>18:52</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
      <td>1644 days</td>
    </tr>
    <tr>
      <th>2016-06-01</th>
      <td>0</td>
      <td>3</td>
      <td>a</td>
      <td>20:22</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>7857.142857</td>
      <td>2016</td>
      <td>6</td>
      <td>1</td>
      <td>2016</td>
      <td>2016-06</td>
      <td>1644 days</td>
    </tr>
    <tr>
      <th>2016-06-02</th>
      <td>0</td>
      <td>4</td>
      <td>c</td>
      <td>11:06</td>
      <td>0</td>
      <td>NaN</td>
      <td>기타 미용업</td>
      <td>2000.000000</td>
      <td>2016</td>
      <td>6</td>
      <td>2</td>
      <td>2016</td>
      <td>2016-06</td>
      <td>1643 days</td>
    </tr>
  </tbody>
</table>
## 4-4. 오늘날짜 : `datetime` 모듈

판다스에 내장된 시계열 자료형들 외에도 datetime이라는 모듈이 존재한다. 이 모듈의 `datetime.now()`함수로 오늘 날짜를 초단위까지 구할 수 있는 재밌는 기능이다.


```python
import datetime
now = datetime.datetime.now()
print(now)
print(now.year)
print(now.month)
print(now.day)
print(now.hour)
print(now.minute)
print(now.second)
print('%s-%s-%s' % (now.year, now.month, now.day))
```

    2020-12-01 20:10:08.795729
    2020
    12
    1
    20
    10
    8
    2020-12-1

## 5.  format 활용한 시계열 데이터 다루기 

8개의 생일 문자열을 이용해보자.  

```python
df = pd.DataFrame({'Birth':['2019-01-01 09:10:00',
                            '2019-01-08 09:20:30',
                            '2019-02-01 10:20:00',
                            '2019-02-02 11:40:50',
                            '2019-02-28 15:10:20',
                            '2019-04-10 19:20:50',
                            '2019-06-30 21:20:50',
                            '2019-07-20 23:30:59']})
```


```python
# object 타입을 datetime64[ns] 타입으로 바꾼다 
df['Birth'] = pd.to_datetime(df['Birth'], format='%Y-%m-%d %H:%M:%S', errors='raise')
```

to_datetime( ) 함수에 첫번째 파라미터로 list를 입력하면 datetimeIndex가 반환되는데, 

Pandas의 Series타입을 입력하면 datetime64형태의 Series타입이 반환된다. (Series타입이 다루기가 더 쉽다)

### Format parameter 

%Y: Year, ex) 2019, 2020       
%m: Month as a zero-padded, ex) 01-12         
%d: Day of the month as a zero-padded, ex) 01-31         
%H: Hour (24-hour clock) as a zero-padded, ex) 01-23       
%M: Minute as a zero-padded, ex) 00-59         
%S: Second as a zero-padded, ex) 00-59           
ex) 2019-09-01 19:30:00 =(Directivs)=> %Y-%m-%d %H:%M:%S             


```python
df['Birth_date']       = df['Birth'].dt.date         # YYYY-MM-DD(문자)
df['Birth_year']       = df['Birth'].dt.year         # 연(4자리숫자)
df['Birth_month']      = df['Birth'].dt.month        # 월(숫자)
df['Birth_month_name'] = df['Birth'].dt.month_name() # 월(문자)

df['Birth_day']        = df['Birth'].dt.day          # 일(숫자)
df['Birth_time']       = df['Birth'].dt.time         # HH:MM:SS(문자)
df['Birth_hour']       = df['Birth'].dt.hour         # 시(숫자)
df['Birth_minute']     = df['Birth'].dt.minute       # 분(숫자)
df['Birth_second']     = df['Birth'].dt.second       # 초(숫자)
df
```



<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Birth</th>
      <th>Birth_date</th>
      <th>Birth_year</th>
      <th>Birth_month</th>
      <th>Birth_month_name</th>
      <th>Birth_day</th>
      <th>Birth_time</th>
      <th>Birth_hour</th>
      <th>Birth_minute</th>
      <th>Birth_second</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-01-01 09:10:00</td>
      <td>2019-01-01</td>
      <td>2019</td>
      <td>1</td>
      <td>January</td>
      <td>1</td>
      <td>09:10:00</td>
      <td>9</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-01-08 09:20:30</td>
      <td>2019-01-08</td>
      <td>2019</td>
      <td>1</td>
      <td>January</td>
      <td>8</td>
      <td>09:20:30</td>
      <td>9</td>
      <td>20</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-02-01 10:20:00</td>
      <td>2019-02-01</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>1</td>
      <td>10:20:00</td>
      <td>10</td>
      <td>20</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-02-02 11:40:50</td>
      <td>2019-02-02</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>2</td>
      <td>11:40:50</td>
      <td>11</td>
      <td>40</td>
      <td>50</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-02-28 15:10:20</td>
      <td>2019-02-28</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>28</td>
      <td>15:10:20</td>
      <td>15</td>
      <td>10</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019-04-10 19:20:50</td>
      <td>2019-04-10</td>
      <td>2019</td>
      <td>4</td>
      <td>April</td>
      <td>10</td>
      <td>19:20:50</td>
      <td>19</td>
      <td>20</td>
      <td>50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019-06-30 21:20:50</td>
      <td>2019-06-30</td>
      <td>2019</td>
      <td>6</td>
      <td>June</td>
      <td>30</td>
      <td>21:20:50</td>
      <td>21</td>
      <td>20</td>
      <td>50</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2019-07-20 23:30:59</td>
      <td>2019-07-20</td>
      <td>2019</td>
      <td>7</td>
      <td>July</td>
      <td>20</td>
      <td>23:30:59</td>
      <td>23</td>
      <td>30</td>
      <td>59</td>
    </tr>
  </tbody>
</table>



```python
df['Birth_quarter']       = df['Birth'].dt.quarter       # 분기(숫자)
df['Birth_weekday_name']  = df['Birth'].dt.day_name()  # 요일이름(문자) (=day_name())
df['Birth_weekday']       = df['Birth'].dt.weekday       # 요일숫자(0-월, 1-화) (=dayofweek)
df['Birth_weekofyear']    = df['Birth'].dt.weekofyear    # 연 기준 몇주째(숫자) (=week)
df['Birth_dayofyear']     = df['Birth'].dt.dayofyear     # 연 기준 몇일째(숫자)
df['Birth_days_in_month'] = df['Birth'].dt.days_in_month # 월 일수(숫자) (=daysinmonth)
df
```



<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Birth</th>
      <th>Birth_date</th>
      <th>Birth_year</th>
      <th>Birth_month</th>
      <th>Birth_month_name</th>
      <th>Birth_day</th>
      <th>Birth_time</th>
      <th>Birth_hour</th>
      <th>Birth_minute</th>
      <th>Birth_second</th>
      <th>Birth_quarter</th>
      <th>Birth_weekday_name</th>
      <th>Birth_weekday</th>
      <th>Birth_weekofyear</th>
      <th>Birth_dayofyear</th>
      <th>Birth_days_in_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-01-01 09:10:00</td>
      <td>2019-01-01</td>
      <td>2019</td>
      <td>1</td>
      <td>January</td>
      <td>1</td>
      <td>09:10:00</td>
      <td>9</td>
      <td>10</td>
      <td>0</td>
      <td>1</td>
      <td>Tuesday</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-01-08 09:20:30</td>
      <td>2019-01-08</td>
      <td>2019</td>
      <td>1</td>
      <td>January</td>
      <td>8</td>
      <td>09:20:30</td>
      <td>9</td>
      <td>20</td>
      <td>30</td>
      <td>1</td>
      <td>Tuesday</td>
      <td>1</td>
      <td>2</td>
      <td>8</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-02-01 10:20:00</td>
      <td>2019-02-01</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>1</td>
      <td>10:20:00</td>
      <td>10</td>
      <td>20</td>
      <td>0</td>
      <td>1</td>
      <td>Friday</td>
      <td>4</td>
      <td>5</td>
      <td>32</td>
      <td>28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-02-02 11:40:50</td>
      <td>2019-02-02</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>2</td>
      <td>11:40:50</td>
      <td>11</td>
      <td>40</td>
      <td>50</td>
      <td>1</td>
      <td>Saturday</td>
      <td>5</td>
      <td>5</td>
      <td>33</td>
      <td>28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-02-28 15:10:20</td>
      <td>2019-02-28</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>28</td>
      <td>15:10:20</td>
      <td>15</td>
      <td>10</td>
      <td>20</td>
      <td>1</td>
      <td>Thursday</td>
      <td>3</td>
      <td>9</td>
      <td>59</td>
      <td>28</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019-04-10 19:20:50</td>
      <td>2019-04-10</td>
      <td>2019</td>
      <td>4</td>
      <td>April</td>
      <td>10</td>
      <td>19:20:50</td>
      <td>19</td>
      <td>20</td>
      <td>50</td>
      <td>2</td>
      <td>Wednesday</td>
      <td>2</td>
      <td>15</td>
      <td>100</td>
      <td>30</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019-06-30 21:20:50</td>
      <td>2019-06-30</td>
      <td>2019</td>
      <td>6</td>
      <td>June</td>
      <td>30</td>
      <td>21:20:50</td>
      <td>21</td>
      <td>20</td>
      <td>50</td>
      <td>2</td>
      <td>Sunday</td>
      <td>6</td>
      <td>26</td>
      <td>181</td>
      <td>30</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2019-07-20 23:30:59</td>
      <td>2019-07-20</td>
      <td>2019</td>
      <td>7</td>
      <td>July</td>
      <td>20</td>
      <td>23:30:59</td>
      <td>23</td>
      <td>30</td>
      <td>59</td>
      <td>3</td>
      <td>Saturday</td>
      <td>5</td>
      <td>29</td>
      <td>201</td>
      <td>31</td>
    </tr>
  </tbody>
</table>



```python
df['Birth_is_leap_year']     = df['Birth'].dt.is_leap_year     # 윤년 여부
df['Birth_is_month_start']   = df['Birth'].dt.is_month_start   # 월 시작일 여부
df['Birth_is_month_end']     = df['Birth'].dt.is_month_end     # 월 마지막일 여부
df['Birth_is_quarter_start'] = df['Birth'].dt.is_quarter_start # 분기 시작일 여부
df['Birth_is_quarter_end']   = df['Birth'].dt.is_quarter_end   # 분기 마지막일 여부
df['Birth_is_year_start']    = df['Birth'].dt.is_year_start    # 연 시작일 여부
df['Birth_is_year_end']      = df['Birth'].dt.is_year_end      # 연 마지막일 여부
df
```



<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Birth</th>
      <th>Birth_date</th>
      <th>Birth_year</th>
      <th>Birth_month</th>
      <th>Birth_month_name</th>
      <th>Birth_day</th>
      <th>Birth_time</th>
      <th>Birth_hour</th>
      <th>Birth_minute</th>
      <th>Birth_second</th>
      <th>...</th>
      <th>Birth_weekofyear</th>
      <th>Birth_dayofyear</th>
      <th>Birth_days_in_month</th>
      <th>Birth_is_leap_year</th>
      <th>Birth_is_month_start</th>
      <th>Birth_is_month_end</th>
      <th>Birth_is_quarter_start</th>
      <th>Birth_is_quarter_end</th>
      <th>Birth_is_year_start</th>
      <th>Birth_is_year_end</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-01-01 09:10:00</td>
      <td>2019-01-01</td>
      <td>2019</td>
      <td>1</td>
      <td>January</td>
      <td>1</td>
      <td>09:10:00</td>
      <td>9</td>
      <td>10</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>1</td>
      <td>31</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-01-08 09:20:30</td>
      <td>2019-01-08</td>
      <td>2019</td>
      <td>1</td>
      <td>January</td>
      <td>8</td>
      <td>09:20:30</td>
      <td>9</td>
      <td>20</td>
      <td>30</td>
      <td>...</td>
      <td>2</td>
      <td>8</td>
      <td>31</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-02-01 10:20:00</td>
      <td>2019-02-01</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>1</td>
      <td>10:20:00</td>
      <td>10</td>
      <td>20</td>
      <td>0</td>
      <td>...</td>
      <td>5</td>
      <td>32</td>
      <td>28</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-02-02 11:40:50</td>
      <td>2019-02-02</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>2</td>
      <td>11:40:50</td>
      <td>11</td>
      <td>40</td>
      <td>50</td>
      <td>...</td>
      <td>5</td>
      <td>33</td>
      <td>28</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-02-28 15:10:20</td>
      <td>2019-02-28</td>
      <td>2019</td>
      <td>2</td>
      <td>February</td>
      <td>28</td>
      <td>15:10:20</td>
      <td>15</td>
      <td>10</td>
      <td>20</td>
      <td>...</td>
      <td>9</td>
      <td>59</td>
      <td>28</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019-04-10 19:20:50</td>
      <td>2019-04-10</td>
      <td>2019</td>
      <td>4</td>
      <td>April</td>
      <td>10</td>
      <td>19:20:50</td>
      <td>19</td>
      <td>20</td>
      <td>50</td>
      <td>...</td>
      <td>15</td>
      <td>100</td>
      <td>30</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2019-06-30 21:20:50</td>
      <td>2019-06-30</td>
      <td>2019</td>
      <td>6</td>
      <td>June</td>
      <td>30</td>
      <td>21:20:50</td>
      <td>21</td>
      <td>20</td>
      <td>50</td>
      <td>...</td>
      <td>26</td>
      <td>181</td>
      <td>30</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2019-07-20 23:30:59</td>
      <td>2019-07-20</td>
      <td>2019</td>
      <td>7</td>
      <td>July</td>
      <td>20</td>
      <td>23:30:59</td>
      <td>23</td>
      <td>30</td>
      <td>59</td>
      <td>...</td>
      <td>29</td>
      <td>201</td>
      <td>31</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 23 columns</p>
</div>




```python

```
