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
> seaborn 可以用短小的代碼去繪製描述更多維度資料的可視化效果圖。<br>
> 3 . Bokeh (動態的套件，類似於 D3.js)：交互資訊可視化，不需編輯 HTML 與 JavaScript 便能製作網頁前端視覺化<br>
> 用於做瀏覽器端交互可視化的庫，實現分析師與數據的交互。<br>
> 4 . Basemap：地圖可視化，以上三者效果不佳<br>
