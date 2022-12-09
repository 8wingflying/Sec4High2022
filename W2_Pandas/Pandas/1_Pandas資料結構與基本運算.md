## 1_pandas的資料結構(Data Structures) ==> series vs DataFrame


### 1_1_series的運算 see [CHAPTER 5 Getting Started with pandas](https://github.com/LearnXu/pydata-notebook/blob/master/Chapter-05/5.1%20Introduction%20to%20pandas%20Data%20Structures%EF%BC%88pandas%E7%9A%84%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%89.ipynb)
- 建立series
  - 使用pandas.Series()建立 series
  - 使用字典資料型態建立pandas.Series() 
- 搜尋滿足條件的資料


#### (1)使用[pandas.Series()](https://pandas.pydata.org/docs/reference/api/pandas.Series.html) 建立Series
```python
obj = pd.Series([41, 27, -25, 13,21])
obj
```


```python
obj.values
```


```python
obj.index
```

```python
obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
obj2
```
```python
obj2.values
```


```python
obj2.index
```

#### 透過index(索引)進行搜尋

```python
obj2['a']
```


```python
obj2[['c', 'a', 'd']]
```
#### 透過index(索引)進行設定

```python
obj2['d'] = 6
```


```python
obj2[['c', 'a', 'd']]
```
#### 更多運算
```python
obj2[obj2 > 0]
```


```python
obj2 * 2
```

```python
import numpy as np
np.exp(obj2)
```

#### 使用字典資料型態建立pandas.Series() 
```python
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon':16000, 'Utah': 5000}

obj3 = pd.Series(sdata)
obj3
```


```python
states = ['California', 'Ohio', 'Oregon', 'Texas']

obj4 = pd.Series(sdata, index=states)
obj4
```
#### 使用pandas的isnull和notnull函數檢測MISSING Value(缺失資料)
```python
pd.isnull(obj4)
```


```python
pd.notnull(obj4)
```

```python
obj4.isnull()
```

#### Series自動排序(Data alignment features)
- Series自動按index label來排序


```python
obj3
```

```python
obj4
```


```python
obj3 + obj4
```

#### series  `name屬性`的運用
- series自身和它的index都有一個叫name的屬性

```python
obj4.name = 'population'

obj4.index.name = 'state'

obj4
```
#### 更改 series的index

```python
obj
obj.index = ['Bob', 'Steve', 'Jeff', 'Ryan']
obj

```
#### 加分作業:研讀底下參考資料並完成實務演練

[Pandas 資料分析實戰：使用 Python 進行高效能資料處理及分析 (Learning pandas : High-performance data manipulation and analysis in Python, 2/e) Michael Heydt ](https://www.tenlong.com.tw/products/9789864343898)
  - [GITHUB](https://github.com/PacktPublishing/Learning-Pandas-Second-Edition) 
  - Chapter 3：用序列表示單變數資料
    - 3.1 設定pandas
    - 3.2 建立序列
    - 3.3 .index及.values屬性
    - 3.4 序列的大小及形狀
    - 3.5 在序列建立時指定索引
    - 3.6 頭、尾、選取
    - 3.7 以索引標籤或位置提取序列值
    - 3.8 把序列切割成子集合
    - 3.9 利用索引標籤實現對齊
    - 3.10 執行布林選擇
    - 3.11 將序列重新索引
    - 3.12 原地修改序列


## 1_2_DataFrame的運算 see [CHAPTER 5 Getting Started with pandas](https://github.com/LearnXu/pydata-notebook/blob/master/Chapter-05/5.1%20Introduction%20to%20pandas%20Data%20Structures%EF%BC%88pandas%E7%9A%84%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%89.ipynb)
- 建立DataFrame

- 搜尋滿足條件的資料

### (1)建立DataFrame: 使用python dict 資料型態 + dict裡的value是list 資料型態
```python
data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'], 
        'year': [2000, 2001, 2002, 2001, 2002, 2003], 
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

frame = pd.DataFrame(data)

frame
```

### 顯示資料的技術
```python
frame.head()
```


```python
pd.DataFrame(data, columns=['year', 'state', 'pop'])
```
### missing value
```python
frame2 = pd.DataFrame(data, columns=['year', 'state', 'pop', 'debt'], 
                      index=['one', 'two', 'three', 'four', 'five', 'six'])
frame2

frame2.columns
```

## 資料提取
- 提取一column(列)
- 提取一row(行)

### 從DataFrame提取一列(底下兩種提取方法)== > 回傳給你一個series
```python
frame2['state']
frame2.year
```
### 從DataFrame提取一row(行)

```python
frame2.loc['three']
```
### 資料變更(賦值)的幾種範例
```python
frame2['debt'] = 16.5
frame2
```

```python
frame2['debt'] = np.arange(6.)
frame2
```

```python
val = pd.Series([-1.2, -1.5, -1.7], index=['two', 'four', 'five'])
frame2['debt'] = val
frame2
## 特別注意結果
```

```python
frame2['eastern'] = frame2.state == 'Ohio'
frame2
```

#### 刪除資料
```python
del frame2['eastern']

frame2.columns
```

### (2)建立Data Frame的情境 == >
```python
pop = {'Nevada': {2001: 2.4, 2002: 2.9},
       'Ohio': {2000: 1.5, 2001: 1.7, 2002: 3.6}}

frame3 = pd.DataFrame(pop)
frame3
```

```python

```
### (3)建立Data Frame的情境 == > 使用python dict + series

```python
pdata = {'Ohio': frame3['Ohio'][:-1],
         'Nevada': frame3['Nevada'][:2]}
pd.DataFrame(pdata)
```


```python
frame3.index.name = 'year'; frame3.columns.name = 'state'
frame3
frame3.values
frame2.values
```
#### 加分作業:研讀底下參考資料並完成實務演練

[Pandas 資料分析實戰：使用 Python 進行高效能資料處理及分析 (Learning pandas : High-performance data manipulation and analysis in Python, 2/e) Michael Heydt ](https://www.tenlong.com.tw/products/9789864343898)
  - [GITHUB](https://github.com/PacktPublishing/Learning-Pandas-Second-Edition) 
  - Chapter 4：用資料框表示表格及多變數資料
    - 4.1 設定pandas
    - 4.2 建立資料框物件
    - 4.3 存取資料框的資料
    - 4.4 利用布林選擇選取列
    - 4.5 跨越行與列進行選取
  - Chapter 5：操控資料框結構
    - 5.1 設定pandas
    - 行columns的各種運算
      - 5.2 重新命名行Renaming columns
      - 5.3 利用[]及.insert()增加新行
      - 5.4 利用擴展增加新行
      - 5.5 利用串連增加新行
      - 5.6 改變行的順序
      - 5.7 取代行的內容
      - 5.8 刪除行
    - 列columns的各種運算
      - 5.9 附加新列
      - 5.10 列的串連
      - 5.11 經由擴展增加及取代列
      - 5.12 使用.drop()移除列
      - 5.13 利用布林選擇移除列
      - 5.14 使用切割移除列
