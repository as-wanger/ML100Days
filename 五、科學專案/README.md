## 一、導論
根據資料、數據上的限制與環境需求為客戶選擇一個最合適的「計算模型」，解答「數理」問題<br>
讓客戶得以根據該解法，轉譯出背後的商業價值：`拆解問題 → 組織問題 → 解決問題`<br>
1 . 領域範疇<br>
2 . 四種分析型態：描述型(現況)，診斷型(因果關係)、預測型(預測)與建議型(規劃)<br>
3 . 實作流程<br>
> 定義問題與目標 → 確認資料與分析任務 → 設計、蒐集資料 → 探索性資料分析與資料清理 → 特徵工程 → <br>
>  → 建立預測模型並評價 → 解釋意義 → 表達、部屬以決策<br>

> 3 . 3 探索性資料分析<br>
>> 3 . 3 . 1 確認資料型態<br>
>> 3 . 3 . 2 每一個欄位的意義，分布<br>
>> 3 . 3 . 3 檢測 異常值 和 缺失值<br>
>> 3 . 3 . 4 發掘 特徵變數 之間的關係，如特徵變數與目標變數、特徵變數彼此之間的關係<br>
>> 3 . 3 . 5 測試基本的假設<br>
>> 3 . 3 . 6 提取或找出 重要的特徵變數（即特徵工程）<br>
>> 3 . 3 . 7 初步選擇合適的模型<br>
>> 
## 二、內容
1 . 遺失值：遺失值處理的精髓就在於`不能影響整體的估計`，讓`程式順利執行`，讓已有的別的屬性的值能發揮作用。<br>
`填補數與已有的數的分佈、特徵應符合`，`不能`因為處理的變更導致估計值`變化`。<br>
> 1 . 1 分類
>> 1 . 1 . 1 完全隨機缺失（Missing completely at random）：樣本數缺失、資料從500少一行變499等<br>
>> 1 . 1 . 2 條件隨機缺失（Missing at random）：女性體重遺失影響女性體重分佈與推算變數(如BMI)<br>
>> 1 . 1 . 3 非隨機缺失（Missing not an random）：特定變數與特定樣本有關，如蛋雞週齡就是比肉雞高出許多<br>
>> 1 . 1 . 4 或進修部學生有收入、日間部學生沒有<br>

2 . 異常值：離群值，可分為偽異常(正常反映業務狀態或隱藏地用於檢測是否被盜用)、真異常(真的反應異常分佈狀態)<br>
> 2 . 1 發生原因：數據輸入錯誤(人工出錯)、測量誤差(錯誤測量儀器)、故意離群(人為規避或偏誤)、抽樣錯誤、自然異常值<br>
> 2 . 2 無須處理：反映真實結果、(特定性)異常檢測模型、包容異常值的資料模型(失耐)<br>
> 2 . 3 判別方法：簡單統計如`data.describe()`、三倍標準差：`outliers_z_score(data['欄位'],3)`<br>
> 盒鬚圖抓離群值：`outliers_iqr(data['欄位'],1.5)`<br>
> 2 . 4 處理方法：刪除、數據轉換、聚類(以決策數收斂)、加權平均、替換、分離處理<br>
> 其他：https://zh.wikipedia.org/wiki/%E5%BC%82%E5%B8%B8%E6%A3%80%E6%B5%8B<br>

> 3 . 2 處理<br>
>> 3 . 2 . 1 刪除<br>
>> 刪除過多缺失、分類複雜會不會探討之變數或樣本<br>
>> 3 . 2 . 2 補值<br>
>> 零、固定值(如平均數、中位數、眾數)、前往後、後往前或(內插法、迴歸或機器學習)等預測方法<br>

> 4 . 1 變數關係
> from scipy import stats
>> 4 . 1 . 1 連續 vs 連續：`stats.pearsonr(data,data2)`<br>
>> 4 . 1 . 2 離散 vs 連續：Cramer's V 係數：卡方檢定的結果來運算出一個可以估算離散型變數的相關性的指標。<br>
>>> 4 . 1 . 2 . 1 交叉表：`contable = pd.crosstab(data,data2)`<br>
>>> 自由度：`df = min(contable.shape[0], contable.shape[1]) - 1`<br>
>>> `crosstab, res = researchpy.crosstab(data, data2, test="chi-square")`<br>
>>> 4 . 1 . 2 . 2 value：`res.loc[2,"results"]`，查表判斷相關性的高中低<br>

>> 4 . 1 . 3 離散 vs 離散：`Cohen's ds`、`Point biserial’s correlation`或`eta-squared`(以eta-squared為例)<br>
>> 使用 pingouin ：import pingouin as pg<br>
>>> 4 . 1 . 3 . 1 建立ANOVA_Table：`aov = pg.anova(dv="變數1", between="變數2", data=data, detailed=True)`<br>
>>> 4 . 1 . 3 . 2 etaSq：`aov.SS[0] / (aov.SS[0]+aov.SS[1])`，查表判斷相關性的高中低<br>
 
3 . 問題排除<br>
> 3 . 1 重複問題：`data.duplicated()`<br>
> 3 . 2 補值：`data['colA'].fillna()`，內容可以是`method='ffill','bfill','pad'`(時間相關) or `data['colA'].mean()`<br>
>> 3 . 2 . 1 應用預測模型補值：K-Nearest Neighbor(KNN)無須機率分配的假設下的演算法<br>
>> 以距離預測值最近的 k 個值來估計預測值<br>
>> 三步驟：計算距離、尋找最近 k 組數值、類別型態資料以多數決。距離可用<br>
>> 歐幾里得距離(Euclidean distance，差的平方和後再開根號)或曼哈頓距離(Manhattan distance，差的絕對值)<br>
>>> 3 . 2 . 1 . 1 如非連續型，如3 . 5 . 2 修改資料型態去處理<br>
>>> from sklearn.impute import KNNImputer
>>> 3 . 2 . 1 . 2 計算資料倆倆之間距離：`KNNImputer(missing_values=nan, n_neighbors=5, weights='uniform'`<br>
>>> `, metric='nan_euclidean', copy=True, add_indicator=False)`，`weights`為權重，也可是`distance`<br>
>>> 3 . 2 . 1 . 3 from sklearn.metrics.pairwise import nan_euclidean_distances <br>
>>> `display(pd.DataFrame(nan_euclidean_distances(data)))`<br>
>>> 3 . 2 . 1 . 4 KNN補值：設定k值(參照點個數)：`value_neighbor=1`<br>
>>> 3 . 2 . 1 . 5 KNN初始化：`imputer = KNNImputer(n_neighbors=value_neighbor)`<br>
>>> pd.DataFrame(imputer.fit_transform(data))<br>
>> 3 . 2 . 2 對補值評價：以均方誤差(Mean-Square Error)評估，即 (i=1...n_sigma(Ei) - mean) / n 的平方<br>
>> 分子為變異數兩種表示方式之一<br>

> 3 . 3 判斷 測試資料集和訓練資料集欄位變數是否有差異性：`print(len(data.columns) == len(data2.columns))`<br>
> 但不管有無出現False，還是要分別看一下以免誤打誤撞<br>
> 3 . 4 判斷 測試資料集是否有遺失值：`data.isnull().any()`、`data.isnull().any().sum()`<br>
> 3 . 5 修改資料型別<br>
>> 3 . 5 . 1 顯示資料資訊：`data.info()`<br>
>> 3 . 5 . 2 修改資料型態：`data['欄位'] = data['欄位'].astype('新型態')`，如類別型轉離散型，後以LabelEncoder轉連續型<br>
> 3 . 6 查看某欄位值的特性：`data[欄位'].value_counts()`、`data[欄位'].unique()`<br>

4 . 製圖
> 4 . 1 計數：`sns.countplot(data['欄位'], hue=['欄位2'])`(欄位2是一般性資料)<br>
> 4 . 2 分出子圖：`g = sns.FacetGrid(data=data, col='colA')`、`g.map(plt.distplot,'colB', kde=False)`<br>
 
5 . 特徵
> 5 . 1 在矩陣，A乘vector = λI乘vector，表示變換後矩陣找到特殊向量，使vector被A矩陣變換後矩陣中的向量僅受伸縮影響<br>
> 即為特徵向量，伸縮倍數為特徵值。<br>
> 即(A - λI)乘vector = 0，vector要是非零向量，`A在扣除λ倍的單位矩陣後，行列式為零`<br>
> 5 . 2 在原始資料集中有變化性，憑藉特徵把目標做清楚的分類與預測，才能稱為好的特徵。<br>
> 5 . 3 特徵工程：有衍生（透過探索性分析，了解資料、目標關係，產生特徵）<br>
> 或添加（現有資料以外，外部數據導入，為模型帶來突破）<br>
> 找出變異性資料？分為連續、離散型。<br>
> 連續：四分位數、全距、百分位數、標準差、變異數。<br>
> 離散：類別數量統計<br>
> 
> 而從相關性來看，高度就可以是獨立的特徵；中低度表示"可能"需要轉換，那麼後者如何萃取特徵？<br>
>> 5 . 3 . 1 衍生可分為ICR：指示器變量(Indicator)、資料組合(Combination)、資料重新定義(Reshape)<br>
>>> 5 . 3 . 1 . 1 　I：生成新資料，運用.apply(lambda x:....if...else...)做變數轉換<br>
>>> 或是先def一個函數，data["新欄位"] = data["舊欄位"].apply(該函數)<br>
>>> 5 . 3 . 1 . 2 　C：如BMI(身高/體重^2)、飼料轉換率(飼料/體增重)<br>
>>> 生長效率因子（體重(kg) * 存活率 * 100/飼料轉換率 * 生長日齡）<br>
>>> 5 . 3 . 1 . 3 　R：如偵測頻率（時雨量比10分鐘及時雨量好，沒有時間遞延問題）<br>
>>> 、連續轉分類年齡轉幼童、青少年、老人)、合併稀疏資料、定義類別資料距離（幼童、青少年、老人轉1、2、3）<br>
>>> 或重新定義類別資料距離（1、2、3再轉1、4、9），如<br>
>>> `list={key1:value1...}`、`data['新欄位'] = data['欄位'].map(list)`(分類)<br>
>>> 
>>> 、數值到分類的映射：先`def f(x)`好一個函數，而後`data['新欄位'] = data['欄位'].apply(f)`<br>
>>> 、創造虛擬資料（？：取決於機器學習算法，如果是以距離來量測資料的遠近<br>
>>> ，則需將類別特徵轉換到虛擬變量中去，稱作 one-hot encoding。），又如使用`pd.get_dummies()`<br>

> 5 . 4 如何選出好特徵：具有變化性、預測性、辨識力<br>
> 即使拉出特徵，特徵還是需要選擇，使模型泛化能力更好、避免過擬合、提高特徵與目標的解釋力<br>
> 選取方法：`sklearn.feature_selection`裡的函數<br>
>> 5 . 4 . 1 **過濾法**(Filter)：把具變化性以及與目標變數相關的特徵，挑選出具變化性以及中高度相關的特徵，方法包含<br>
>>> 5 . 4 . 1 . 1 移除低變異數的特徵：<br>
>>>> 5 . 4 . 1 . 1 . 1 標準化（最大最小值）<br>
>>>> 5 . 4 . 1 . 1 . 2 設定變異數的過濾門檻，保留超過100的變異數：`filter=VarianceThreshold(threshold=(100))`<br>
>>>> `data_f = filter.fit_transform(data['特徵'])`<br>
>>>> 計算每個特徵變異數(list)：`filter.variances_`<br>
>>>> 確認哪些會留下：`filter.get_support(True)`<br>
>>>> 須注意資料間變異數本來就有差，門檻可能不公平，故先經過標準化(z值)會比較準確(結果不相同)<br>
>>>> 5 . 4 . 1 . 1 . 3 透過函數做計算，過濾<br>
>>>> 5 . 4 . 1 . 1 . 4 確定哪一些特徵留下來<br>
>>> 5 . 4 . 1 . 2 單變量特徵選取（Univariate Feature Selection）：<br>
>>>> 5 . 4 . 1 . 2 . 1 目標變數為離散型，採用卡方檢定(兩類, chi2)或ANOVA檢定(多類, f_classif)<br>
>>>> 目標變數為連續型，可採用 f_regression <br>
>>>> 5 . 4 . 1 . 2 . 2 `from sklearn.feature_selection import SelectBest, f_regression`<br>
>>>> 5 . 4 . 1 . 2 . 2 資料問題排除後，定義好`x=data['colA','colB'...]`、`y=data['欄位']`<br>
>>>> 5 . 4 . 1 . 2 . 2 `x_new = SelectPercentile(chi2, percentile=50).fit_transform(x, y)`、`x_new.shape`<br>

>> 5 . 4 . 2 **包裝法**(Wrapper)：特徵選擇看作是搜索問題，根據某一種評量標準，每次選擇某些特徵或排除某些特徵<br>
>> 常用的方法為遞歸特徵消除(RFE)。根據離散或連續，選擇帶有 `coef_ `和`feature_importances_`的模型 <br>
>> from sklearn.datasets import make_firedman1<br>
>> from sklearn.feature_selection import RFE<br>
>> from sklearn.svm import SVR<br>
>>> 5 . 4 . 2 . 1 資料處理後，根據離散或連續，如離散型：`SVC(kernel='linear')`<br>
>>> 最後要選擇留下多少特徵：`n_features_to_select`、每部刪除多少特徵：`Step`
>>> 一樣資料問題排除後，定義好`x=data['colA','colB'...]`、`y=data['欄位']`<br>
>>> `estimator = SVC(kernel='linear')`、`selector = RFE(estimator, n_features_to_select=2, step=1)`<br>
>>> 每一步都依不同的特徵組合建立模型，判斷最終要選擇那些特徵：`selector = selector.fit(x, y)`<br>
>>> 透過`support_`呈現包裝法搭配 SVC 下，選擇最好的特徵，用 True 來表示：`selector.support_`<br>
>>> 排行：(1 代表被選重的特徵，2 代表次之重要的特徵，依此類推)`selector.ranking_`<br>
>>> 排序：`x.loc[:,selector.support_].columns.tolist()`<br>

>> 5 . 4 . 3 **嵌入法**(Embedded)：採用建模演算法內的特徵選取方法，得到某些特徵的權重係數<br>
>> 根據係數的重要性來選擇特徵，但必須有演算法的先備知識 **PASS**
