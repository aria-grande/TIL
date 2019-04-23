# 매출액을 예측하는 모델을 만들어보자.

## 목적
- 숫자를 맞춰보는 짜릿함을 느껴보자.
- 어떤 요인이 매출에 큰 기여를 하는지 알아보자.

## 필요한 것
- 데이터(csv)
- Jupyter
- 모델 기법에 대한 지식
  - sales forecast는 time series 모델인데 어떤 방법을 사용해서 구축하는게 좋을까? Linear Regression일까? 무엇일까?

## 1. 데이터
매출에 요인을 주는 요소들을 우선 찾아보자. 대충 생각해봤을 때에는 요일과 휴일 여부, 날씨, 마케팅 효과 등이 있을 것 같다.

일단 기본적인 데이터만 가지고 model을 만들어보자.

|날짜|매출액|요일(wday)|휴일여부|휴일이름|
|:--:|---|---------|-----|-----|
|2019-04-01|1000000|1|False||
|2019-04-02|1200000|2|False||
|2019-04-03|980000|3|False||
|2019-04-04|900000|4|False||
|2019-04-05|1100000|5|False||
|2019-04-06|1400000|6|True|Sat|

예측하고자 하는 y는 매출액, 요일이나 휴일 여부는 변수인 x1, x2가 될 수 있겠다.

### 1.1. 데이터 reading
데이터를 읽고 scattering 해보자.
```python
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker

data_file_name = './data/settle_report.csv'

data = pd.read_csv(data_file_name)
data.head()

x = data['date']
y = data['sales']

fix, ax = plt.subplots()
ax.yaxis.set_major_formatter(ticker.FuncFormatter(lambda x, p: format(int(x), ',')))

plt.xlabel('date')
plt.ylabel('sales')
plt.scatter(x, y)
plt.show()
```


## 참고
- https://res.mdpi.com/data/data-04-00015/article_deploy/data-04-00015-v2.pdf?filename=&attachment=1
```
Sales prediction is rather a regression problem than a time series problem. The use of regression
approaches for sales forecasting can often give us better results compared to time series methods.
```
