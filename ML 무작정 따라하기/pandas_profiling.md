

# Pandas_Profiling  for quick data analysis.

 [Pandas Profiling ](https://github.com/pandas-profiling/pandas-profiling)is probably the easiest way to do EDA quickly (although there are many other alternatives such as [SweetViz](https://github.com/fbdesignpro/sweetviz) ), the downside of using Pandas Profiling is that it can be slow to give you very in-depth analysis, even when not needed.

 For each column the following statistics - if relevant for the column type - are presented in an interactive HTML report :

- **Type inference**: detect the types of columns in a dataframe.
- **Essentials**: type, unique values, missing values
- **Quantile statistics** like minimum value, Q1, median, Q3, maximum, range, interquartile range
- **Descriptive statistics** like mean, mode, standard deviation, sum, median absolute deviation, coefficient of variation, kurtosis, skewness
- **Most frequent values**
- **Histogram**
- **Correlations** highlighting of highly correlated variables, Spearman, Pearson and Kendall matrices
- **Missing values** matrix, count, heatmap and dendrogram of missing values
- **Text analysis** learn about categories (Uppercase, Space), scripts (Latin, Cyrillic) and blocks (ASCII) of text data.
- **File and Image analysis** extract file sizes, creation dates and dimensions and scan for truncated images or those containing EXIF information.

### Installation (using PIP)


```python
! pip install https://github.com/pandas-profiling/pandas-profiling/archive/master.zip
```


```python
import pandas_profiling as pp
import pandas as pd 
import numpy as np 
from pandas_profiling import ProfileReport
```


```python
df = pd.read_csv('/content/sample_data/train.csv')
```


```python
pp.ProfileReport(df)
```

### Descriptive statistics 

 For this stage I like to look at just a few key points:

- I look at the count to see if I have a significant amount of missing values for each specific feature. If there are many missing values for a certain feature I might want to discard it.

![image-20201119200633479](/Users/jisuekim/Library/Application Support/typora-user-images/image-20201119200633479.png)

- I look at the unique values (for categorical this will show up as NaN for pandas describe, but in Pandas Profiling we can see the distinct count). If a feature has only 1 unique value it will not help my model, so I discard it.

- I look at the ranges of the values. If the max or min of a feature is significantly different from the mean and from the 75% / 25%, I might want to look into this further to understand if these values make sense in their context.

![image-20201119195840023](/Users/jisuekim/Desktop/DataAnalyst/images/image-20201119195840023.png)

![image-20201119200042249](/Users/jisuekim/Desktop/DataAnalyst/images/image-20201119200042249.png)

![image-20201119200135857](/Users/jisuekim/Desktop/DataAnalyst/images/image-20201119200135857.png)


### References
[1] [Pandas Profiling](https://github.com/pandas-profiling/pandas-profiling)

[2] ["Exploratory Data Analysis (EDA) — Don’t ask how, ask what" by tamar Chinn](https://medium.com/towards-artificial-intelligence/exploratory-data-analysis-eda-dont-ask-how-ask-what-2e29703fb24a) 

