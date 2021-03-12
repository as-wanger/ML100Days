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

pip install geos <br>
pip install pyproj<br>
pip install basemap <br>

from mpl_toolkits.basemap import Basemap<br>
import matplotlib.pyplot as plt<br>

>> 4 . 1 建立地圖：`map = Basemap()`<br>
>>> 4 . 1 . 1 畫輪廓線：`contour()`<br>
>>> 4 . 1 . 2 畫輪廓線並填滿：`contourf()`<br>
>>> 4 . 1 . 3 在地圖上畫圖：`imshow()`<br>
>>> 4 . 1 . 4 偽色圖：`pcolor()`<br>
>>> 4 . 1 . 5 偽色圖(快速版)：`pcolormesh()`<br>
>>> 4 . 1 . 6 在地圖上畫線繪圖：`plot()`<br>
>>> 4 . 1 . 7 在地圖上畫散點圖：`scatter()`<br>
>>> 4 . 1 . 8 畫向量圖、三維即曲面圖：`quiver()`<br>
>>> 4 . 1 . 8 畫風羽圖：`barbs()`<br>
>>> 4 . 1 . 8 畫大圓航線：`drawgreatcircle()`<br>

>> 4 . 2 設定解析度與範圍：`resolution='x'`。x = c(原始)、l(低)、i(中)、h(高)、f(完整)或None(如果沒有使用邊界)<br>
>>> 4 . 2 . 1 設置經緯度：左下緯度、右上緯度、左下經度、右上經度：`llcrnrlat`、`urcrnrlat`、`llcrnrlon`、`urcrnrlon`<br>
>>> 或是`lat_0`、`lat_1`、`lon_0`、`lon_1` <br>
>>> `llcrnrlat = -90   =  lat_0`<br>
>>> `urcrnrlat = 90    =  lat_1`<br>
>>> `llcrnrlon = -180` = `lon_0 = 0`<br>
>>> `urcrnrlon = 180   =  lon_1`<br>

>> 4 . 3 繪製經緯線(經度：longitude、緯度：latitude，表示方式緯度在前、經度在後)<br>
>> 4 . 3 . 1 方法一<br>
>>> 4 . 3 . 1 . 1 先得知絕對位置並定義：如紐約市40.7127 N、74.0059 W、`NYClat, NTClon = 40.7127, -74.0059`<br>
>>> 4 . 3 . 1 . 2 轉換成x、y軸：`xpt, ypt = map(NYClon, NYClat)`<br>
>>> 4 . 3 . 1 . 3 繪製該座標：`map.plot(xpt, ypt , 'c*', markersize)`<br>
 
>> 4 . 3 . 2 方法二：運用 "itertools" 庫中的 "chain" 模組<br>
>>> 4 . 3 . 2 . 1 設定經度範圍：`lats = map.drawparallels(np.linspace(-90, 90, 13))`<br>
>>> 4 . 3 . 2 . 2 設定緯度範圍：`lons = map.drawmeridians(np.linspace(-180, 180, 13))`<br>
>>> 4 . 3 . 2 . 3 plt.Line2D 實例設置經緯線：<br>

```
lat_lines = chain(*(i[1][0] for i in lats.items()))
lon_lines = chain(*(j[1][0] for j in lons.items()))
all_lines = chain(lat_lines, lon_lines)
map.plot(all_lines)
```
>> 4 . 4 投影：`basemap.supported_projections`，如正射投影：`map = Basemap(projection='ortho', lat_0 = 0, lon_0 = 0)`<br>
>> 蘭伯特圓錐投影：`map = Basemap(projection = 'lcc',width=12000000,height=9000000, 
>> lat_1=45., lat_2=55, lat_0=50, lon_0=-107, resolution=None)`<br>
>> 米勒投影：`map = Basemap(projection='mill',llcrnrlat = -90,llcrnrlon = -180,urcrnrlat = 90,urcrnrlon = 180,
            resolution='h')`<br>
>> 其他：詳見https://en.wikipedia.org/wiki/List_of_map_projections<br>
>> 4 . 5 上色：<br>
>>> 4 . 5 . 1 全部上藍色：`map.drawmapboundary(fill_color = 'aqua')`<br>
>>> 4 . 5 . 2 陸地上珊瑚色、海洋上藍色：`map.fillcontinents(color = 'coral', lake_color = 'aqua')`<br>
>>> 4 . 5 . 3 寶石藍：`map.bluemarble()`<br>

>> 4 . 6 畫海岸線(畫圖)：`map.drawcoastlines()`，可包括`linewidth`、`color`(如'darked'、'b')<br>
>> 4 . 7 畫陰影浮雕圖：`map.shadedrelief(scale=0.2)`<br>
>> 4 . 8 畫國家：`map.drawcountries()`<br>
>> 4 . 9 畫州界：`map.drawstates()`<br>
>> 4 . 10 畫城市：`map.drawcounties()`<br>
>> 4 . 11 顯示：`plt.show()`<br>
>> 4 . 12 儲存：`plt.savefig('test.png')`<br>

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
from mpl_toolkits.mplot3d import Axes3D<br>
> 1 . 創建座標系：`fig = plt.figure()`、`ax = Axes3D(fig)`<br>
> 2 . 創建x、y值：`x=np.linspace(0,10,110)`、`y=np.cos(x * np.pi)`<br>
> 3 . 創建z值並繪圖：ax.plot(x, y, zs = 0.5, zdir = 'z', color = 'black')<br>
> 其中`zdir = 'z'`將資料繪製在z軸、`zs`為資料內容<br>
> 
