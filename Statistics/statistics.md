# 불확실성에 대한 학문, 통계학 

 일부 데이터만으로 모집단으로 분석하는 과정은 당연히 불확실성(uncertainty)를 발생시킨다. 데이터 수집하는 방법에서부터 분석과정, 결과도출까지의 모든 과정은 불확실성을 줄이는 일일 것이다. 수많은 데이터를 통해 어떠한 통찰을 얻고 의사결정자를 설득하는 과정에서 데이터를 요약하고 주요 변수를 가려낼 수 있는 통계적 사고가 필요할 것이다. 

## 평균 (mean) 과 중간값 (median) 

* Central tendency 

  1. **mean** : oultlier sensitive tendency & **median** : ordinal, robust (non-sensitive of outliers)   

  2. **skewness** : right or left skewed (경사가 완만한 곳을 기준으로 판단)

     ____________________

     Many textbooks teach a rule of thumb stating that the mean is right of the median under right skew, and left of the median under left skew. This rule fails with surprising frequency. It can fail in multimodal distributions, or in distributions where one tail is long but the other is heavy. Most commonly, though, the rule fails in discrete distributions where the areas to the left and right of the median are not equal. Such distributions not only contradict the textbook relationship between mean, median, and skew, they also contradict the textbook interpretation of the median.

     출처 :  https://en.wikipedia.org/wiki/Skewness

     __________________

     예 ) Left-skewed : mean < median  인데,  mean > median  일 때,  skewness 계산 시  negative skewness  갖는 경우에 multimodal distribution(다봉분포) 가능성 -> 왜도 판단 시에는 히스토그램, 왜도측정값 등을 적극활용 

     

## Quantile, Quartile, IQR & Range 

* Dispersion 

  1. n - quantile : 2 - quantile = median & 4 - quantile = quartile 

  2. quartile : Q1(25%), Q2(50%), Q3(75%) or fist, median(second), third quartile 

  3. Range & IQR(inter-quartile range) : range = Max - Min (outlier sensitive tendency)

     IQR = Q3 - Q1 (Max 값이 바뀌더라도 변하지 않는다)

     







