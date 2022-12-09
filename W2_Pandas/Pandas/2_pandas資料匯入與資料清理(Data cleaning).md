## 2_pandas資料匯入與資料清理(Data cleaning)
- [經典:Python 資料分析, 2/e](https://www.tenlong.com.tw/products/9789864769254)
  - [GITHUB](https://github.com/wesm/pydata-book) 
  - [中譯](https://github.com/LearnXu/pydata-notebook/tree/master/)
  - 第六章 資料載入、儲存和檔案格式
  - 第七章 資料整理和前處理
- [Pandas 資料分析實戰：使用 Python 進行高效能資料處理及分析 (Learning pandas : High-performance data manipulation and analysis in Python, 2/e) Michael Heydt ](https://www.tenlong.com.tw/products/9789864343898)
  - [GITHUB](https://github.com/PacktPublishing/Learning-Pandas-Second-Edition) 
  - [Ch9](https://github.com/PacktPublishing/Learning-Pandas-Second-Edition/blob/master/Chapter09/09_Accessing_Data.ipynb)
  - Chapter 9：存取資料
  - 9.2 處理CSV及文字/表格格式的資料
  - 9.3 讀寫Excel格式資料
  - 9.4 讀寫JSON檔案
  - 9.5 從網站讀取HTML資料


## 整體架構

![Pandas_IO.PNG](./Pandas_IO.png)

## 延伸學習

- [Pandas讀寫MySQL資料庫](https://codertw.com/%E8%B3%87%E6%96%99%E5%BA%AB/16156/)
- [使用Python從Mysql抓取每日股價資料與使用pandas進行分析](https://sites.google.com/site/zsgititit/home/python-cheng-shi-she-ji/shi-yongpython-congmysql-zhua-qu-mei-ri-gu-jia-zi-liao-yu-shi-yongpandas-jin-xing-fen-xi)
- [如何用Pandas連接到PostgreSQL資料庫讀寫數據](https://medium.com/@phoebehuang.pcs04g/use-pandas-link-to-postgresql-6cfc24a930f1)

## 1_讀寫CSV檔案 
- see 9.2 處理CSV及文字/表格格式的資料 
- [pandas.read_table](https://pandas.pydata.org/docs/reference/api/pandas.read_table.html)
- 讀取CSV [pandas.read_csv()](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html)
  - 熟悉各種讀取參數用法  [pandas.read_csv参数详解](https://www.cnblogs.com/datablog/p/6127000.html)
  - index_col:指定使用某欄位當作索引
  - nrows：僅讀取⼀定的⾏數
  - skiprows：跳過⼀定的⾏數
  - skipfooter：尾部有固定的⾏數永不讀取
  - skip_blank_lines：空⾏跳過
- 寫入CSV [pandas.DataFrame.to_csv()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html#pandas-dataframe-to-csv)

#### 先下載遠端資料到Google Colab 
```
!wget https://raw.githubusercontent.com/PacktPublishing/Learning-Pandas-Second-Edition/master/data/msft.csv
```
#### 檢視資料
```
!head -n 5 msft.csv 
```
#### Reading a CSV into a DataFrame
```
msft = pd.read_csv("./msft.csv")
msft[:5]
```

#### Specifying the index column when reading a CSV file
```python
# use column 0 as the index
msft = pd.read_csv("./msft.csv", index_col=0)
msft[:5]
```

```python
df3 = pd.read_csv("./msft.csv", usecols=['Date', 'Close'])
df3[:5]
```
#### 寫入CSV Saving a DataFrame to a CSV ==> [pandas.DataFrame.to_csv()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html#pandas-dataframe-to-csv)
```PYTHON
# read in data only in the Date and Close columns
# and index by the Date column
df2 = pd.read_csv("./msft.csv", 
                  usecols=['Date', 'Close'], 
                  index_col=['Date'])
df2[:5]
```
```python
# save df2 to a new csv file
# also specify naming the index as date
df2.to_csv("./msft_A999168.csv", index_label='date')
```
```
# view the start of the file just saved
!head -n 5 ./msft_A999168.csv
```

### 各式csv的讀取 
- 去除頭部說明文字
- 去除底部說明文字
- 讀取部分欄位
- 讀取部分資料
  - [參考程式 GITHUB](https://github.com/PacktPublishing/Learning-Pandas-Second-Edition) 

### 2_讀寫excel檔案 Reading and writing data in Excel format
- [下載excel檔案](https://github.com/PacktPublishing/Learning-Pandas-Second-Edition/blob/master/data/stocks.xlsx)
- 再upload到Google Colab
- xlsx vs xls 檔案差異
- 讀取excel [pandas.read_excel()](https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html)
  - 熟悉各種讀取參數用法  
  - [(最新Pandas.read_excel()全参数详解（案例实操，如何利用python导入excel）)](https://zhuanlan.zhihu.com/p/142972462)
  - [[Pandas教學]5個實用的Pandas讀取Excel檔案資料技巧](https://www.learncodewithmike.com/2020/12/read-excel-file-using-pandas.html)
  - [Python pandas.ExcelWriter用法及代碼示例](https://vimsky.com/zh-tw/examples/usage/python-pandas.ExcelWriter.html)

- 寫入excel [pandas.DataFrame.to_excel()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_excel.html)
  - [Python pandas.DataFrame.to_excel用法及代碼示例](https://vimsky.com/zh-tw/examples/usage/python-pandas.DataFrame.to_excel.html)

#### 讀取excel檔
```python
df = pd.read_excel("./stocks.xlsx")
df[:5]
```

### 讀取不同試算表
```python
# read from the aapl worksheet
aapl = pd.read_excel("./stocks.xlsx", sheet_name='aapl')
aapl[:5]
```

#### 寫入到excel檔
```python
# save to an .XLS file, in worksheet 'Sheet1'
df.to_excel("./stocks2.xls")
```


### 3_讀寫 JSON 檔案
- [JSON](https://zh.wikipedia.org/wiki/JSON)
- XML vs JSON
- Reading and writing JSON files
- 範例來源:https://github.com/PacktPublishing/Pandas-Cookbook-Second-Edition/blob/master/Chapter03/c3-code.ipynb
```python

# 建立DataFrame 
fname = ['Paul', 'John', 'Richard', 'George']
lname = ['McCartney', 'Lennon', 'Starkey', 'Harrison']
birth = [1942, 1940, 1940, 1943]
people = {'first': fname, 'last': lname, 'birth': birth}
beatles = pd.DataFrame(people)

# 編碼成json格式
import json
encoded = json.dumps(people)
encoded

# 使用loads()載入 json檔 == > 回傳一個dict
json.loads(encoded)

# 使用read_json()讀取 json檔
beatles = pd.read_json(encoded)
beatles

# 使用to_json()加上orient參數輸出不同格式的 json檔
# orient參數 == > 設定不同輸出格式
# orient='records'
# orient='split'
# orient='index'
# orient='values'
# orient='table'
# 請驗證其資料讀取時呈現的結果

records = beatles.to_json(orient='records')
records
pd.read_json(records,orient='records)

```
- [pandas.read_json](https://pandas.pydata.org/docs/reference/api/pandas.read_json.html#pandas-read-json)
- [pandas.DataFrame.to_json](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_json.html)

### 4_讀取網頁表格資料 
- [pandas.read_html()](https://pandas.pydata.org/docs/reference/api/pandas.read_html.html)
  - [[Pandas教學]掌握Pandas DataFrame讀取網頁表格的實作技巧](https://www.learncodewithmike.com/2020/11/read-html-table-using-pandas.html)  
- [pandas.DataFrame.to_html](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_html.html)
  - [[Pandas教學]利用Pandas套件的to_html方法在網頁快速顯示資料分析結果](https://www.learncodewithmike.com/2021/07/pandas-to-html.html) 
```python
url ='https://en.wikipedia.org/wiki/The_Beatles_discography'
dfs = pd.read_html(url)
len(dfs)
dfs[0]
dfs[1]
```

## 5_存取資料庫資料
- 使用SQLite3
- 先下載[stocks.sqlite](https://github.com/PacktPublishing/Learning-Pandas-Second-Edition/blob/master/data/stocks.sqlite)並上傳到colab 
- 或是先執行 !wget https://github.com/PacktPublishing/Learning-Pandas-Second-Edition/blob/master/data/stocks.sqlite?raw=true
```
# reference SQLite
import sqlite3

# read in the stock data from CSV
msft = pd.read_csv("https://raw.githubusercontent.com/PacktPublishing/Learning-Pandas-Second-Edition/master/data/msft.csv")
msft["Symbol"]="MSFT"
aapl = pd.read_csv("https://raw.githubusercontent.com/PacktPublishing/Learning-Pandas-Second-Edition/master/data/aapl.csv")
aapl["Symbol"]="AAPL"

# create connection
connection = sqlite3.connect("data/stocks.sqlite")
# .to_sql() will create SQL to store the DataFrame
# in the specified table.  if_exists specifies
# what to do if the table already exists
msft.to_sql("STOCK_DATA", connection, if_exists="replace")
aapl.to_sql("STOCK_DATA", connection, if_exists="append")

# commit the SQL and close the connection
connection.commit()
connection.close()
```
- 連線到資料庫並執行SQL查詢
```
# connect to the database file
connection = sqlite3.connect("./stocks.sqlite")

# query all records in STOCK_DATA
# returns a DataFrame
# inde_col specifies which column to make the DataFrame index
stocks = pd.io.sql.read_sql("SELECT * FROM STOCK_DATA;", 
                             connection, index_col='index')

# close the connection
connection.close()

# report the head of the data retrieved
stocks[:5]
```
