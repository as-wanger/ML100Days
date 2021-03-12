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
>> 3 . 2 變異數：描述變數的離散程度、與期望值（期望無差異時的平均數）的距離<br>
>> 簡單說是誤差的平方和/總個數，變異數/期望值為分散指數，標準差/期望值為變異係數<br>

## 二、機率(Probability)
> 1 . 名詞：pdf、pmf、cdf、cmf<br>
> pmf：機率質量函數（probability mass function）。後面變數：(k, low, high, loc=0)<br>
> ppf：百分點函數（Percent point function）。後面變數：(q, low, high, loc=0)<br>
> cdf：累積分佈函數(cumulative distribution function)，又稱分佈函數。後面變數：(k, low, high, loc=0)<br>
> rvs：隨機變量（Random variates）後面變數：(low, high, loc=0, size=1, random_state=None)<br>
> Probability 恆等於一，其他的變化為 possibility 又稱 probability density
> 
> 2 . 離散分配<br>
> 2 . 1 離散均勻分配（randint），骰子、錢幣等均勻機率工具的簡單結果<br>
> low=1; high=7 ;r = np.arange(low,high)或是[1,2,3,4,5,6]<br>
> 機率質量函數：`stats.randint.pmf(r,low,high)`，每項機率"占比"的陣列，p0+...+pn = 1<br>
> 累積機率函數：`stats.randint.cdf(r,low,high)`，機率累加"占比"的陣列，p0+...+pn = 1<br>
> 如果 `a = stats.randint.cdf(r,low,high)`； k = stats.randint.ppf(a , low, high)時，k=r，但詳細點則應該是<br>
> k = np.arange(randint.ppf(0.01, low, high),randint.ppf(0.99, low, high))時，k=r<br>
> 樣本點：`X = stats.randint.rvs(low,high,size)`，隨機出現所有屬於r的次數，size是總次數，使用plt.hist(X,bins);plt.show()可顯示圖型 <br>
> 統計量計算：`stats.randint.stats(low,high,moments='mvks')`呈現該數值的平均數、變異數；moments='mvks'再加上偏度和峰度<br>
> 
> 2 . 2 伯努利分配（bernoulli），發生與不發生的機率<br>
> p = 0.4; r=np.arange(0,2)或[0,1]即[不發生，發生]<br>
> stats.bernoulli.pmf(r,p)，兩個bin的機率，即[不發生機率，發生機率]<br>
> b = stats.bernoulli.cdf(r,p)，一樣累加=1； k = stats.bernoulli.ppf(b , p)時，k=r<br>
> X = stats.bernoulli.rvs(p,size)，兩個bin的次數，size是總次數，使用plt.hist(X,bins)<br>
> stats.bernoulli.stats(r,p,moments='mvks')，隨機變數的平均數、變異數、偏度和峰度。<br>
> 
> 2 . 3 二項分配（binom），樹狀圖的拓展，p=0.5為該發生的機率密度(probability density=possibility)，p=q為均勻二項分配<br>
> `p = 0.5; n = 重複次數; r = 出現次數`<br>
> `stats.binom.pmf(r,n,p)`，各個箱子的機率，類常態分佈<br>
> `c = stats.binom.cdf(r,n,p)`，一樣累加=1； k = stats.randint.ppf(c ,n ,p)時，k=r<br>
> `stats.binom.rvs(n,p,size)`，r個bin的次數，size是總次數<br>
> `stats.binom.stats(r,p,moments='mvks')`，固定參數的平均數（即期望值）、變異數、偏度和峰度。<br>
> 當 p = 常數， q = 1-p 時，變異數為 pq/n<br>
> 
> 2 . 4 負二項分配（nbinom）(發生 p 或不發生 q 出現k次，共重複n次，算是一種事後檢討)<br>
> 套自由度的觀念，最後一項沒有自由，必須乘上該機率(看發生就乘 k/n，看不發生就乘 (k-n)/n)<br>
> 也就是換個角度，看最後一項被限制的二項分配<br>
> `p = 0.5; n = 重複次數; k = 出現次數`<br>
> `stats.nbinom.pmf(k,n,p)`<br>
> `c = stats.nbinom.cdf(k,n,p)`<br>
> `stats.nbinom.rvs(n,p,size)`<br>
> `stats.nbinom.stats(k,p,moments='mvks')`<br>
> 
> 2 . 5 超幾何分配(取後不放回)<br>
> 上述的`n = 重複次數; k = 出現次數`被限制為總個數N與部分個數K，此時發生不會是一個先驗或先設定的值<br>
> 需要通過比例計算以得知 p 與 q ，此時想要抽樣出的符合總抽樣個數n與部分抽樣個數k<br>
> 也就是有三個函數要運算，分別是：`k/K`乘`(n-k)/(N-K)`除`n/N`，p 與 q 約分掉，就剩下三者組合的運算，`p = K/N `(用不到)<br>
> `stats.hypergeom.pmf(k,N,K,n, loc)` = `stats.hypergeom.pmf(loc - k,N,K,n)`<br>
> `c = stats.hypergeom.cdf`<br>
> `stats.hypergeom.rvs`<br>
> `stats.hypergeom.stats`<br>
