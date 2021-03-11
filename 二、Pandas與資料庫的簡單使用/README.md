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
> `.get_dummies(data[['欄位']])`，取得欄位內各種類別、分為新行，配合`pd.concat([,]),axis=1`把新資料併在舊資料右邊`<br>
> 此為One-hot Encoding(一位有效編碼)，只有0跟1`<br>

## 四、資料前處理
> 1 . 缺失值補值：`.fillna()`，如補A欄位平均值：`data.fillna(data.A.mean())`、前一值：`.fillna(method=ffill)`<br>
> 或 後一值：`.fillna(method=bfill)`<br>

## 五、資料視覺化 in pandas
> 1 . 折線圖：`.plot()`，會自動把y作為index、x作為values，可以在建立資料時順便建立表名：`names='test'`，會直接成為圖名<br>
> 或是`.plot(title='test')`來加上圖名<br>
> 2 . 圓餅圖：`.plot.pie()`，<br>
> 3 . 長條圖：`.plot.bar()`，較適合用pd.Dataframe(...,columns=list('ab...'))<br>
> 4 . 盒鬚圖、箱型圖：`.boxplot()`<br>
> 5 . 散佈圖：`.plot.scatter()`<br>
> 
## 六、計算：大多與numpy差不多
> 1 . 自定義：`data.apply(lambda x : x**0.5*10)`，即自定義函數f(x) = x開根號後乘10<br>
> 其他：`data.corr()`<br>
> 
## 七、撰寫樞紐分析表
> 1 . 欄位轉索引(-1,+1)：`data.stack()`可多次堆疊，`data.stack().stack()`<br>
> 2 . 索引轉欄位(+1,-1)：`data.unstack()`<br>
> ----------變換方式像是微波爐一樣，但是每個小分子（要轉換的小元素）都轉同個方向----------<br>
> 3 . 欄位名稱轉欄位值：`.melt()`，其中`id_vars`是保留的列名，`value_vars`是需轉換的列名(剩下都要轉就可省略)<br>
> 4 . 重新組織資料：`.pivot(index='colA', columns='colB', values='colc')`即取用自cola、colb、colc內的不同資料來做成新表<br>
> 要是values多一個就會建立多一倍colb內種類的列數<br>
> 5 . 重組+計算：`.pivot_table(index='colA', columns='colB', values='colc', aggfunc=np.mean)`<br>
> 可將新索引、新列相同的值進行運算<br>

## 八、分群+計算
> 1 . 分群計算：`groupby('欄位').運算`，對欄位內資料分群並 "準備運算"，可接之前numpy提過的`mean()`、`std()`、`describe()`等<br>
> 否則要指定欄位內資料的某群還要`data.loc[data.欄位 == '一般性資料其中一類']`單獨拉出資料<br>
> 因此 `groupby('欄位').運算` 相當於進行了spilt、apply與combine的動作，<br>
> 2 . 多欄位或多運算：多欄位如`groupby(['colA','colB'])`裡面就有多索引<br>
> 而多運算則用.`agg()`，如`groupby('欄位').agg(['mean','std'])`<br>
> 3 . D15用法實例：利用`groupby('欄位').agg(['mean','std'])`拉出資料用，以`data['欄位'].loc['某個索引名']`來選定該格的值<br>

## 九、時間序列(時間類別(Timestamp可以進行加減)
> 1 . 補上或覆寫時間(範圍內索引長一樣)：`data.to_period()`<br>
> 其中`freq='Y'`。Y為年、Q為季、M為月、W為星期、D為日、H為小時，T為分鐘、S為秒<br>
> 2 . 建立時間於索引(同時在建立新表)：`pd.Series([1,2], index = pd.period_range('2018-01-01', freq='Y', periods=2))`<br>
> 3 . 改變時間頻率(減少頻率用)：`data.resample().asfreq()`，即重採樣與作為頻率的組合，可以指定如'5min'<br>
> data.asfreq()也可以但就不會重新採樣<br>
> 4 . 找範圍內時間索引的資料：`data[2020-01-01:2021-01-01]`<br>
> 5 . 移動時間(要跟建立時的頻率相同)：`data.shift(int,freq='')`，如果沒有`freq=''`索引就不會動(前面nan後面顯示不到)<br>
> 6 . 資料類別：直接'2020-01-01'是str，pd.Timestamp(年,月,日)就是時間類別(Timestamp('2020-01-01 00:00:00'))<br>
>> 6 . 1 時間轉字串：`data.strftime('%y-%m-%d')`<br>
>> 6 . 2 字串轉時間：`pd.to_datetime(str)`<br>

> 7 . 回傳時間頻率：`data.year`, `data.month`, `data,day`, `date.day_name()`, `date.weekofyear`、`pd.offsets.BDay()`
> 
## 十、運算速度與記憶體占用
> ```
> start.time() = time.time()
> 內容
> end.time() = time.time()
> end.time() - start.time()

> `data.momory_usage(deep=True).sum()`
> 
> 1 . 檔型速度： npy&npz > pkl > hdf > csv　　　>>>　　　xlsx<br>
> 2 . EX1 分群計算速度：`groupby().agg()` >　`groupby().agg(lambda x : ...)` > `groupby().transform()` > <br>
> `groupby().transform(lambda x : ...)`，原則上用python內建會跑比較快<br>
> 3 . EX2 判斷速度：data['new'] = `data.colA.isin(range(60,100))` > `data.colA.apply(iambda x : x >= 60)` > <br>
> `data.colA >=60`<br>
> 4 . 降字元：`data.apply(pd.to_numeric, downcast='unsigned')`，並用`data.apply(pd.value_counts)`檢查有無遺漏
