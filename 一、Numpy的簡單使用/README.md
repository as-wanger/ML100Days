# numpy中使用<br>

## 一、建立陣列：`arange()` 或 `linspace()`<br>
> 1 . 建立全零、全一陣列、全指定陣列：`zeros()`、`ones()`、`full()`<br>
> 2 . 隨機0~1陣列：一維、二維：`random()`、`random.random((,))`<br>
> 3 . 隨機常態陣列：`np.random.normal(mean, sd, num)`<br>
> 4 . 隨機區間內陣列：如`np.random.randint(0, 10, (3, 3))`，像`arange()`<br>
> 5 . 建立n維(列)、n個向量(行)的 n乘n 矩陣（即是說秩數，但要注意這是矩陣上的定義）：`eye(n)`<br>

## 二、常用屬性與簡單運算：
> 1 . 給定型狀、給定總數(陣乘列的積)：`.shape`、`.size`<br>
> 2 . 維度數或軸數：`.ndim`<br>
> 3 . 塌縮為一維陣列：`.flatten()`<br>
> 4 . 行列轉置：`.T`<br>
> 其他(暫時放置，待到需要記憶體、虛數)：`.real`、`.imag`、`.data`、`.itemsize`、`.nbytes`、`.strides`、`.index`、`.values`<br>
> `.columns`、`.describe()`、`.info()`、`.quantile()`、`.percentile()`、`.mean()`、`.median()`、`.mode()`、`.std()`、`.var()`<br>

## 三、改動、取部分陣列：
> 1 . 重置：`.reshape(3, 4, order="C")`。C、F、A、K的功用：預設為C，F為從行軸，非數組時AK無用。是數組時、A為照原型態<br>
> 2 . 非零：`.nonzero()`<br>
> 3 . 開條件之傳索引、傳值：`.where()`、`np.array(...)[np.where()]`<br>
> 4 . 排序、排序後索引：`.sort()`、`.argsort()`<br>
其他：`.max()`、`.min()`<br>

## 四、一般運算：
> 1 . 歐拉數(自然數)：`np.exp()`<br>
> 2 . 對數：`np.log(x)`、`np.log2(x)`、`np.log10(x)`、`np.log1p(x)`<br>
> 3 . 矩陣相乘：`np.dot(A, B)`。須記得A是N個向量，B是m個向量，施加A的變換到B的向量上，故結果遵照A的維度與B的向量數<br>
> （即是說A是變換矩陣、B是向量個數）<br>
> 3 . 1 . 變換矩陣在左是遵照函數表示方式：f(x)。向量彼此間具線性代數的相加與相乘性，但變換矩陣進行線性變換的是B的向量<br>
> 其他(易理解或未遇到簡單符號不能解決的問題)：`pow()`、`sqrt()`、`rint()`、`trunc()`、`floor()`、`ceil()`、`fix()`、`abs()`<br>
> `corrcoef()`、`correlate()`、`cov()`、`.histogram()`，但是用stats、sns會比較好用
