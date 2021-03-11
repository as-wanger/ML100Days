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
>> 4 . 1 連結與建立資料庫、連結物件：`con = sqlite3.connect('檔名.db')`、`c = con.cursor()`<br>
>> 4 . 2 執行指令、確認更動、關閉連結：`c.execute()`、`con.commit()`、`con.close()`<br>
>> 4 . 3 讀取方式：`with open() as file:`、`pd.read_one`
