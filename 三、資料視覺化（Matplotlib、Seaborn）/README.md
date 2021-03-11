import matplotlib.pyplot as plt(一張圖)<br>
* 透過控制 figure (`*`.SVG)和 axis (資料維度) 來操作。<br>
* 其中 figure 和全域 pyplot 部分屬性相同。例如： fig.text() 對應到 plt.fig_text()<br>

import seaborn as sns<br>
import Bokeh<br>
import Basemap<br>
## 一、不同資料視覺化套件
> 1 . matplotlib (靜態的套件)：基礎 2D 及 3D 可視化<br>
>> 1 . 1 plt.plot( [x], y, [fmt], `*`, data=None, kwargs)<br>
>> [fmt]為格式字串，由顏色字元、風格字元和標記字元組成，包括點線的顏色、點的形狀、線的形狀<br>
>> kwargs表示更多組變數<br>
>> 如`plot(x, y, data = data, color='green', marker='o', linestyle='dashed', linewidth=2, markersize=12, alpha=0.5)`<br>
>> alpha是透明度，分類另外查<br>

> 2 . Seaborn (靜態的套件)：基礎 2D 及 3D 可視化，針對的點主要是資料挖掘和機器學習中的變數特徵選取<br>
> seaborn 可以用短小的代碼去繪製描述更多維度資料的可視化效果圖。(x, y可互換)<br>
>> 2 . 1 取得線上資料：`sns.load_dataset('titanic')`<br>
>> 2 . 2 散點圖關聯圖：`sns.relplot(x, y, hue="colA", style="colB", data=data, size, kind)`<br>
>> 2 . 3 箱型圖：`sns.boxplot(data=data, orient='h')`，其中`orient`是方向，可以把極端值顯現出來<br>
>> 2 . 4 條帶圖：`sns.stripplot(x(一般性資料), y, data=data)`，其中`jitter=True or 0~1`為橫向加變異(抖動)<br>
>> `dodge=True`可分離<br>
>> 2 . 5 蠕蟲圖：`sns.swarmplot(x(一般性資料), y, data=data)`，可替代條帶圖+抖動<br>
>> 2 . 6 `distplot`：`sns.distplot(x, bins=20, kde=False, rug=True)`，kde提供和密度曲線，rug為軸鬚圖<br>
>> 2 . 7 長條圖：`sns.barplot`、直方圖：`sns.histplot`<br>
>> 2 . 8 分出子圖直方圖：`g = sns.FacetGrid(data=data, col='colA')`、`g.map(plt.hist,"colB")`、`label`<br>
>> 其他：`color`、`palette`(調色板名稱)、`size`(標記大小)、`edgecolor`(邊緣顏色)、`linewidth`<br>
>> `xlabelsize`、`ylabelsize`、`grid`<br>
>> 2 . 9 小提琴圖：`sns.violinplot`<br>
>> 2 . 10 不定圖：`data.plot(kind='bar')`，或是`pie`...，另外`stack=True`可以分顏色疊加<br>
>> 或是`data.catplot(kind='bar')`<br>
>> 2 . 11 熱點圖：`sns.heatmap(df.corr())`。除其他以外，`vmin`與`center`與`vmax`決定顏色範圍、`cmap`取用套件顏色<br>
>> `annot`在格內顯示資料、`fmt`顯示資料格式、`annot_kws`設定數字的大小顏色字型、`cbar`設定是否設置顏色刻度條<br>
>> `cbar_kws`為顏色刻度條型設定、`cbar_ax`為顏色度條位置設定、`ax`設定座標軸、`square`設定形狀、`mask`為是否顯示某個矩陣<br>
>> 2 . 12 加入作圖：`sns.jointplot('colA', 'colB', data=data, kind='reg')`做迴歸圖<br>
>> 2 . 13 對角圖：`sns.PairGrid(data, diag_sharey=False)`，其中`diag_sharey=True`(預設)<br>
>> 詳見**diag_sharey.ipynb**。對角線上都會參考相同的 Y 座標值<br>
>> `data.map_upper()`、`data.map_lower()`、`data.map_diag()`可以決定對角以上、以下、對角本身跑哪種圖<br>
>> 也可用`map_offdiag()`決定非對角全部<br>
>> 其他：https://www.twblogs.net/a/5c2601bbbd9eee16b3db8708<br>

> 3 . Bokeh (動態的套件，類似於 D3.js)：交互資訊可視化，不需編輯 HTML 與 JavaScript 便能製作網頁前端視覺化<br>
> 用於做瀏覽器端交互可視化的庫，實現分析師與數據的交互。<br>
> 當bokeh會預設連BokehJS cdn，讓BokehJS驅動於local python env<br>

from bokeh.resources import INLINE <br>
bokeh.io.output_notebook(INLINE)<br>

> 跳轉出 html：`output_file(data.html)`<br>
> 跳轉出 jupyter：`output_notebook(data.ipynb)`<br>

from bokeh.plotting import figure, output_file, show<br>
from bokeh.models import widgets<br>
from bokeh.io import output_notebook<br>

套用內建的模型<br>
from bokeh.themes import built_in_themes<br>
導入輸出的繪製套件<br>
from bokeh.io import curdoc<br>

>> 3 . 1 創建空畫板、直線：`p = figure()`(加上`height`、`width`)、`p.line([1,2,3,4,5], [5,4,3,2,1])`<br>
>> `p.circle(data, size, color)`、`tools='pan,reset,save'`、`title`、`show(p)`<br>
>> `toolbar_location="below"`、`toolbar_sticky=False`<br>
>> 3 . 2 網頁元件與互動圖表<br>
from IPython.display import IFrame<br>
>> IFrame('https://demo.bokeh.org/sliders', width=900, height=500)<br>
>>> 3 . 2 . 1 

> 4 . Basemap：地圖可視化，以上三者效果不佳<br>

## 二、製作繪圖板
> 1 . `plt.subplot(a, b, c)`，a 代表 x 軸的分割、b 代表 y 軸的分割、c 代表子版的編號數<br>
> 每個繪圖前先建立好plt.subplot(a, b, c)，最後會輸出在一起<br>
> 2 . for i in range(8):<br>
> ax = fig.add_subplot(2, 4, i)，產生 2乘4 的子圖形<br>
> 3 . 設定圖案大小：`fig = plt.figure(figsize(4,2))`<br>
> 4 . 同時指定 figure 和 axes：`fig, ax = plt.subplots()`，須注意這邊是axes<br>
>> 4 . 1 Figure，畫布，即整個母圖：`fig = plt.figure`<br>
>> 4 . 2 Axes，每個子圖：<br>
>> 4 . 3 Axis，xy座標軸：ax.xaxis/ax.yaxis<br>
>> 其他figure參數：`num=figure名稱`、`figsize=[6.4, 4.8]`(預設)、`dpi=100`(預設)、`facecolor='w'`(white)<br>
>> `frameon=`(是否繪製輪廓)、`edgecolor='w'`(是否繪製輪廓顏色)(white)、`Figureclass=None`(是否使用 figure 模板)(預設不用)<br>
>> 'clear=False'(同時figure是否取代)(預設)

> 5 . 防止圖疊在一起：`plt.tight_layout()`，其中`rect=[0,0,1,1]`(預設)可指定範圍

## 三、其他
> 1 . `plt.axes`的使用：`plt.axes([x偏移1,y偏移1,x偏移2,y偏移2])`<br>
> 2 . `plt.text`的使用：`plt.text(0.5,0.5, 'axes([0.2,0.2,.3,.3])',ha='center',va='center',size=16,alpha=.5)`<br>
> 表示在繪圖板 x(0~1)、y(0~1)位置，字為`axes([0.2,0.2,.3,.3])`，ha 與 va 分別可以是上中下、左中右<br>
> 3 . 標籤刻度、字體大小：`plt.xticks([範圍],fontsize=20)`，`[範圍]`可改成`np.linspace( , , )`，y軸改成`plt.yticks`<br>
> 或在建立刻度與軸名`set_xticklabels`<br>
> 4 . 格線：`plt.grid(True)`<br>

## 四、3D繪圖板
from mpl_toolkits.mplot3d import Axes3D
> 1 . 創建座標系：`fig = plt.figure()`、`ax = Axes3D(fig)`
> 2 . 創建x、y值：`x=np.linspace(0,10,110)`、`y=np.cos(x * np.pi)`
> 3 . 創建z值並繪圖：ax.plot(x, y, zs = 0.5, zdir = 'z', color = 'black')
> 其中`zdir = 'z'`將資料繪製在z軸、`zs`為資料內容
> 
