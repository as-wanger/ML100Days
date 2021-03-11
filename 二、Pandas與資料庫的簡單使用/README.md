## 一、讀取結構性資料
> import pandas as pd<br>
> 1 . CSV：`pd.read_csv`，可不用精確檔案位址，但讀取檔案要在同資料夾<br>
>> 1 . 1 讀取資料並選部分行：pd.read_csv=('檔名.csv',`usercols=['列名']`)<br>
>> 或是pd.read_csv=('檔名.csv', hearder=0, `names=['列名']`)<br>
>> 1 . 2 輸出：data.to_csv=('檔名.csv')<br>

> 2 . Excel：`pd.read_excel`，使用 XLRD 或 OpenPyXL 套件，必須精確檔案位址<br>
>> 2 . 1 讀取資料頁面：pd.read_excel=(`'檔名.xlsx'`,sheet_name='頁面名')，且同樣可用1 . 1<br>
>> 2 . 2 輸出並更改頁面名：data.to_excel=(`'檔名.xlsx'`, sheet_name='頁面名')<br>

> 3 . JSON：`pd.read_json`<br>
>> 3 . 1 讀取資料：pd.read_json=(`'檔名.json'`)<br>
>> 3 . 2 輸出：data.to_json=(`'檔名.json'`)<br>

> 4 . SQL資料庫：`import sqlite3`
>> 4 . 1 方法一
>> 4 . 1 . 1 連結與建立資料庫、連結物件：`con = sqlite3.connect('檔名.db')`、`c = con.cursor()`<br>
>> 4 . 1 . 2 執行指令、建立資料表：`c.execute()`、`'CREATE TABLE if not exists table_name();'`，內容則查照`資料庫order.txt`<br>
>> 4 . 1 . 3 確認更動、關閉連結：`con.commit()`、`con.close()`<br>
>> 4 . 2 方法二
>> 4 . 2 . 1 讀取方式：`with open() as file:`、`data2 = pd.read_one`<br>
>> 4 . 2 . 2 連結與建立資料庫、輸出：`con2 = sqlite3.connect('檔名.sqlite')`、`data2.to_sql(con2, if_exists='replace')`<br>
>> 如果data2是excel則要補上頁面名<br>
>> 4 . 2 . 3 確認更動、關閉連結：`con2.commit()`、`con2.close()`<br>
>> 4 . 3 搜尋
>> 4 . 3 . 1 連結資料庫、搜尋：`con3 = sqlite3.connect('檔名.sqlite')`、`data3 = pd.io.sql.read_sql("select * from boston", con3)`
>> 4 . 3 . 2 關閉連結：`con3.close()`
