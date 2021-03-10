# numpy中使用<br>

## 一、建立陣列：`arange()` 或 `linspace()`<br>
> 1 . 建立全零、全一陣列、全指定陣列：`zeros()`、`ones()`、`full()`<br>
> 2 . 隨機0~1陣列：一維、二維：`random()`、`random.random((,))`<br>
> 3 . 隨機常態陣列：`np.random.normal(mean, sd, num)`<br>
> 4 . 隨機區間內陣列：如`np.random.randint(0, 10, (3, 3))`，像`arange()`<br>
> 5 . 建立n維(列)、n個向量(行)的 n乘n 矩陣（即是說秩數，但要注意這是矩陣上的定義）：`eye(n)`<br>

## 二、常用屬性：
> 1 . 給定型狀、給定總數(陣乘列的積)：`.shape`、`.size`<br>
> 2 . 維度數或軸數：`.ndim`<br>
> 3 . 塌縮為一維陣列：`.flatten()`<br>
> 4 . 行列轉置：`.T`<br>
> 其他(暫時放置，待到需要記憶體、虛數)：`.real`、`.imag`、`.data`、`.itemsize`、`.nbytes`、`.strides`

## 三、改動、取部分陣列：
> 1 . 重置：`.reshape(3, 4, order="C")`，其中C、F、A、K表示排序方式(預設為C，F為從行軸，非數組時AK無用。是數組時、A為照原型態)
> 2 . 
