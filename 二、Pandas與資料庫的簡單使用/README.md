## 一、讀取與輸出結構性資料
> import pandas as pd<br>
> 1 . CSV：`pd.read_csv`，可不用精確檔案位址，但讀取檔案要在同資料夾
>> 1 . 1 讀取資料並選部分行：pd.read_csv=('檔名.csv',`usercols=['列名']`)<br>
>> 或是pd.read_csv=('檔名.csv', hearder=0, `names=['列名']`)<br>
>> 1 . 2 輸出：data.to_csv=('檔名.csv')<br>

> 2 . Excel：`pd.read_excel`，使用 XLRD 或 OpenPyXL 套件，必須精確檔案位址
>> 2 . 1 讀取資料頁面：pd.read_excel=(`'檔名.xlsx'`,sheet_name='頁面名')，且同樣可用1 . 1<br>
>> 2 . 2 輸出並更改頁面名：data.to_excel=(`'檔名.xlsx'`, sheet_name='頁面名')<br>

> 3 . JSON：`pd.read_json`
>> 3 . 1 讀取資料：pd.read_json=(`'檔名.json'`)<br>
>> 3 . 2 輸出：data.to_json=(`'檔名.json'`)<br>

> 4 . SQL資料庫：`import sqlite3`
>> 4 . 1 方法一<br>
>>> 4 . 1 . 1 連結與建立資料庫、連結物件：`con = sqlite3.connect('檔名.db')`、`c = con.cursor()`<br>
>>> 4 . 1 . 2 執行指令、建立資料表：`c.execute()`、`'CREATE TABLE if not exists table_name();'`，內容則查照`資料庫order.txt`<br>
>>> 4 . 1 . 3 確認更動、關閉連結：`con.commit()`、`con.close()`<br>

>> 4 . 2 方法二<br>
>>> 4 . 2 . 1 讀取方式：`with open() as file:`、`data2 = pd.read_one`<br>
>>> 4 . 2 . 2 連結與建立資料庫、輸出：`con2 = sqlite3.connect('檔名.sqlite')`、`data2.to_sql(con2, if_exists='replace')`<br>
>>> 如果data2是excel則要補上頁面名<br>
>>> 4 . 2 . 3 確認更動、關閉連結：`con2.commit()`、`con2.close()`<br>

>> 4 . 3 搜尋<br>
>>> 4 . 3 . 1 連結資料庫、搜尋：`con3 = sqlite3.connect('檔名.sqlite')`<br>
>>> `data3 = pd.io.sql.read_sql("select * from boston", con3)`<br>
>>> 4 . 3 . 2 關閉連結：`con3.close()`<br>

## 二、資料簡單操作
> 1 . 指定欄位名稱為索引（不能建立）：`set_index('欄位名稱')`或`set_index(['欄位名稱1','欄位名稱2'])`，而後可用`.index`查詢<br>
> 2 . 重新命名：`.rename()`，注意指定時不是用`replace(,)`，而是用dict的`{key:value}`呈現，這邊包含在`columns=`內<br>
> 3 . 增加資料
>> 3 . 1 增加欄位：`data['欄位名']`、`data.insert('欄位名')`<br>
>> 3 . 2 增加列資料(最後一列)：`data.append(pd.DataFrame([col1,col2...],columns=data.columns))`<br>
>> 或是`data.append({key1:value1,key2:value2...})`，但要配`ignore_index=True`<br>

> 4 . 刪除資料
>> 4 . 1 刪除欄位、回傳刪除欄位、回傳刪除後剩餘欄位：`del data['欄位名']`、`data.pop('欄位名')`、`data.drop('欄位名')`<br>
>> 4 . 2 刪除列資料：`data.drop(對應index)`<br>

> 5 . 指定範圍資料(回傳True資料)：`data[]`、`data.loc[](可併選欄位)`、`data.iloc[](可併選欄位)`<br>
> 包含`data[(data.欄位1>10)&(data.欄位2<20)]`<br>
> 6 . 串聯：`.concat()`，其中`axis=0`(預設)是列延長、`axis=1`是行延長(相似於`numpy.concatenate()`)<br>
> `join='outer'`(預設)是聯集、`join='inner'`是交集<br>
> 7 . 合併、聯結：`.merge()`或`.join()``how=inner`、`how=outer`、`how=left`、`how=right`，可對應前一行做合併<br>
> 重複欄名時merge會自動分，join需要指名`lsuffix='A', rsuffix='B'`<br>

## 三、類別資料
> 1 . 順序性
> from sklearn.preprocessing import LabelEncoder，須注意其實LabelEncoder()<br>
> 編碼：`data['new'] = LabelEncoder().fit_transform(data['A'].values)`<br>
> 反查編碼(還原)：`data['new'] = LabelEncoder().inverse_transform(data['A'].values)`<br>
> 2 . 一般性
> `.get_dummies(data[['欄位']])`，取得欄位內各種類別、分為新行，配合`pd.concat([,]),axis=1`把新資料併在舊資料右邊
> 此為One-hot Encoding(一位有效編碼)，只有0跟1

## 四、資料前處理
> 1 . 缺失值補值：`.fillna()`，如補A欄位平均值：`data.fillna(data.A.mean())` 或 前一值、後一值：`.fillna(method=ffill)`、`.fillna(method=bfill)`
