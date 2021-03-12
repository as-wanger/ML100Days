import matplotlib.pyplot as plt<br>
import numpy as np<br>
import pandas as pd<br>
from scipy import stats<br>
import math as mt<br>
import statistics<br>
import seaborn as sns<br>

## 一、母體與樣本
> 1 . 採樣：從母體裡取出一部分，以小博大、見微知著，如每校每班進行抽樣，代表全台蒐集該年級學生的資料樣態<br>
> 2 . 語法：python內建的statistics、numpy與stats<br>
> 3 . 基本推算變數：平均數、中位數、眾數，將由資料的離散程度、峰度(kurtosis)與偏度(skewness)影響<br>
> `np.mean()`、`np.median()`、`stats.mode()`、`stats.kurtosis()`、`stats.skewness()`<br>
>> 3 . 1 資料離散程度：標準差、變異數、四分位距、百分位數(如PR值)等<br>
>> `np.std()`、`np.var()`<br>
