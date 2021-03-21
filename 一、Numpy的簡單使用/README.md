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
> 4 . 行列轉置：`.T`(`.transpose()`)<br>
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
>> 3 . 1 . 變換矩陣在左遵照函數表示方式：f(x)。向量彼此間具線性代數的相加與相乘性，但變換矩陣進行線性變換的是B的向量<br>
> 其他(易理解或未遇到簡單符號不能解決的問題)：`cumsum()`、`pow()`、`sqrt()`、`rint()`、`trunc()`、`floor()`、`ceil()`<br>
> `fix()`、`abs()``corrcoef()`、`correlate()`、`cov()`、`.histogram()`，但是用stats、sns會比較好用<br>

## 五、歸檔(NumPy I/O)：
> 1 . 存一陣列、多陣列、取：`save()`(.npy)、`savez()`(.npz)、`load()`<br>
> 2 . `savetxt()`、`loadtxt()`、`genfromtxt()`<br>
>> 2 . 1 . 去除空格、固定間隔：<br>
> from io import StringIO<br>
>> data = u"  1  2  3\n  4  5 67\n890123  4"<br>
>> np.genfromtxt(StringIO(data), delimiter=3)<br>
>> 而delimiter也可以是str、autostrip=True可以去除空格<br>
>> 2 . 2 . 補空值：`filling_values=np.nan`，或是指定missing_values成為array，filling_values同樣格式以一一填補<br>
>> 2 . 3 . 轉換：`trans()`與`converters={2:trans, 3:conversion}` <br>
>> 2 . 4 . 其他：`comments="#"`、`skip_footer`、`skip_header`、`names=True`讀入names或names="..."則可以重新定義<br>
> 
## 六、矩陣運算：
> 1 . 矩陣相乘：`.dot()`(見四、3 .)、`.matmul(A, B)`(二維時與dot相同)，等於 A @ B<br>
> 2 . 內積、外積：`.inner()`(一維＝矩陣相乘，更高維是最後一個軸上的和積，故最後一軸個數得相同。)、`.outer()`(成行成列)<br>
> 3 . 跡：`.trace()`就是對角和<br>
> 4 . 行列式：`.linalg.det()`<br>
> 5 . 反矩陣：`.linalg.inv()`<br>
> 6 . 特徵值(w)、特徵向量(v)：`w, v = np.linalg.eig(A)`<br>
> 7 . 秩：`np.linalg.matrix_rank(A)`<br>
> 8 . 線性求解(向量為代數，維度為條件，組成聯立方程)：`.linalg.solve(a,b)`<br>
> 9 . 單位矩陣、對角矩陣、單對角矩陣：`identity`、`.diag()`、`.diagonal(A, offset=1)`而offset也可以另外設定<br>
> 10. 三角矩陣、上三角矩陣、下三角矩陣：`.tri(3, 5, 1, dtype=int)`、`.triu()`、`tril()`<br>
> 11. 矩陣分解：`.linalg.cholesky()`、`.linalg.qr()`、`.linalg.svd()`<br>
> 
## 七、結構化陣列：因架構與pandas 相似，故略過
