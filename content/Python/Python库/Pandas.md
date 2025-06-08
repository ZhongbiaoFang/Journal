![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506072005762.png)
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506082005950.png)

## 创建 Series 和 DataFrame

```python
# 首先导入Pandas库  
import pandas as pd # 建议统一使用 pd 作为别名

# 创建 Series（一维数据结构）：创建一组病人的Temperature数据，指定患者Name为索引  
temps = pd.Series([36.5, 37.0, 36.8], index=["ZhangSan", "LiSi", "WangWu"])  
print("Temperature记录：")  
print(temps)

'''输出：
Temperature记录：
ZhangSan    36.5
LiSi        37.0
WangWu      36.8
dtype: float64
'''
```

```ad-note
title: 什么是Series
collapse: open
pd.Series 是 Pandas 中的一种一维数据结构，类似于 Python 的列表或字典。它可以存储任意类型的数据（如整数、浮点数、字符串等），并且每个数据都有一个对应的索引（index）。
特点：
一维结构：类似于数组或列表。
索引支持：每个元素都有一个唯一的索引，默认从 0 开始，也可以自定义。
数据类型统一：一个 Series 中的所有数据类型必须一致。

```

```python
# 创建 DataFrame（二维表格）  
data = {  
    "Name": ["ZhangSan", "LiSi", "WangWu", "LiSi"],  
    "Gender": ["Male", "Female", "Male", "Female"],  
    "Temperature": [None, 37.0, 36.8, 37.0], # 缺失值  
    "Systolic Pressure": [120, 130, 125, 130]  
} 

# 先创建字典  
df = pd.DataFrame(data) # 通过字典创建DataFrame，每列是一个字段/变量  
print("病人信息表：")  
print(df) # NaN 表示缺失  
'''Output  
病人信息表：  
Name  Gender  Temperature  Systolic Pressure
0  ZhangSan    Male          NaN                120  
1      LiSi   		Female         37.0                130  
2    WangWu    Male         36.8                125  
3      LiSi  		Female         37.0                130  
'''
```

```ad-note
title: 什么是DataFrame
DataFrame 是 Pandas 库中的一种二维数据结构，类似于电子表格或数据库中的表格。它由行和列组成，可以存储不同类型的数据（如数值、字符串、布尔值等）。
特点：
二维结构：行和列组成的表格。
索引支持：既有行索引（index），也有列索引（columns）。
数据类型多样：每列可以存储不同类型的数据。
灵活操作：支持数据选择、过滤、清洗、统计分析等操作。
# ==先创建字典  很重要！==
```python
df = pd.DataFrame(data) # 通过字典创建DataFrame，每列是一个字段/变量  
```

## 保存和读取数据文件 （csv/ excel）+总览 Dataframe 数据情况
```python
df = pd.read_csv("病人信息表.csv")  # 读取CSV文件  
print(df); type(df)  

df = pd.read_excel("病人信息表.xlsx")  # 读取Excel文件  
print(df); type(df)   # 数据类型：pandas.core.frame.DataFrame
```

```Python
# 总览数据情况
print(df.shape) # 行数、列数  
print(df.head()) # 显示前5行  
print(df.info()) # 查看数据结构  
'''  
行数、列数：(4, 4)，即4行4列  
---  
数据结构：  
RangeIndex: 4 entries, 0 to 3  
Data columns (total 4 columns):  
 #   Column             Non-Null Count  Dtype  ---  ------             --------------  -----    
 0   Name               4 non-null      object（文字）  1   Gender             4 non-null      object  
 2   Temperature        3 non-null      float64（浮点型）  
 3   Systolic Pressure  4 non-null      int64（整数）  
dtypes: float64(1), int64(1), object(2)  
memory usage: 260.0+ bytes  
None  
'''
```

## Dataframe 数据选择操作 (df.loc VS df.iloc)
```python
## 4. Dataframe数据选择操作## 注意：需要加“___”  
# 选择单列（Temperature）  
print(df["Temperature"])  
# 选择某行某列：使用 loc（按标签）  
print(df.loc[1, "Name"])  # 第2行的Name（LiSi）  
print(df.loc[:, "Name"])  # 所有行的Name【“：”，即所有】  
# 使用 iloc（index location，按位置）  
print(df.iloc[1, 0])      # 第2行的第1列（LiSi）
```

```ad-note
title: df.loc VS df.iloc
`df.loc` 是 Pandas 中 DataFrame 的标签（label）定位器，用于通过“行标签”和“列标签”来选取、筛选或赋值数据。常见用法如下：
选取某一行某一列的值：df.loc[行标签, 列标签] 例如：df.loc[1, "Name"] 选取第2行（标签为1）“Name”列的值。
选取某一列所有行：df.loc[:, "Name"]
选取多行多列：df.loc[ [0,2], ["Name", "Temperature"] ]
也可用于条件筛选：df.loc[df["Gender"]==1, "Name"]
loc 只能用“标签”索引，不能用数字位置（数字位置用 iloc）

`df.iloc` 是 Pandas 中 DataFrame 的“按位置”索引器，用于通过“行号”和“列号”来选取、筛选或赋值数据。常见用法如下：
选取某一行某一列的值：df.iloc[行号, 列号] 例如：df.iloc[1, 0] 选取第2行第1列的值。
选取某一列所有行：df.iloc[:, 0]
选取多行多列：df.iloc[ [0,2], [1,2] ] 
也可用于切片：df.iloc[0:2, 1:3]
注意：iloc 只能用数字位置（从0开始），不能用标签。与 loc 区别：loc 用标签，iloc 用数字。
```


## Dataframe 数据简单清洗操作
```python
## 5. Dataframe数据简单清洗操作（去重、缺失值、类型转换）##  
# 去掉重复行  
print(df)  
df = df.drop_duplicates() # drop_duplicates() 是 Pandas 提供的一个方法，用于移除 DataFrame 中完全相同的行  
print(df)  
  
# 填补Temperature缺失值为 36.9df["Temperature"] = df["Temperature"].fillna(36.9)  
print(df)  
  
# 将“Gender”列转换为数值分类变量  
df["Gender"].dtype # 'O'：object  
df["Temperature"].dtype # 'float64'：浮点数  
'''  
df["Gender"].dtype 的意思是：查看 DataFrame（df）中 "Gender" 这一列的数据类型（dtype）。  
常见返回值有 object/O（字符串/文本）、int64（整数）、float64（浮点数）等。  
例如，如果 "Gender" 列是字符串（如 "Male"、"Female"），则 dtype 为 object；如果已经转换为数字（如 1、2），则 dtype 为 int64。  
'''  
# 使用 map() 方法将字符串转换为数值  
df["Gender"] = df["Gender"].map({"Male": 1, "Female": 2})  
df["Gender"].dtype # int64  
print(df)  
'''  
这行代码的作用是将 DataFrame 中 "Gender" 列的值从字符串（"Male" 和 "Female"）映射为数值（1 和 2）。具体来说：  
df["Gender"]：表示 DataFrame 中的 "Gender" 列。  
.map({"Male": 1, "Female": 2})：使用字典将 "Male" 替换为 1，将 "Female" 替换为 2。  
这种操作通常用于将分类变量（categorical variable）转换为数值变量（numerical variable），以便后续的机器学习模型或数据分析使用。  
'''
```

## Dataframe 合并与拼接
纵向拼接（行拼接）`pd.concat`：适用于将多张结构相同的表合并成一张
```python
# 示例：两个病人数据表，字段相同  
df1 = pd.DataFrame({  
    "Name": ["ZhangSan", "LiSi"],  
    "Temperature": [36.6, 37.1]  
})  
df2 = pd.DataFrame({  
    "Name": ["WangWu", "赵六"],  
    "Temperature": [36.8, 37.4]  
})  
# 使用 pd.concat() 进行纵向拼接（axis=0）  
df_concat_row = pd.concat([df1, df2], axis=0, ignore_index=True)  
'''  
这行代码的作用是将两个 DataFrame（df1 和 df2）按行（纵向）拼接成一个新的 DataFrame，具体解释如下：  
pd.concat([df1, df2])：使用 Pandas 的 concat 方法，将 df1 和 df2 合并。  
axis=0：指定按行拼接（纵向拼接）。如果是 axis=1，则按列拼接（横向拼接）。
【注意：Pandas的axis=0/1和Numpy.array里的axis=0/1触发的意思是反过来的】
ignore_index=True：重新生成新 DataFrame 的索引，忽略原有的索引（即原有列表的0 1 2行号会重新排版） 
最终结果是一个包含 df1 和 df2 所有行的新 DataFrame，索引会从 0 开始重新排列。  
'''  
print("纵向拼接后的表格：")  
print(df_concat_row)
```

横向拼接（列拼接）`pd.merge`：适用于多个字段扩展到同一组人
```python
# 示例：同一组病人，不同检查结果  
base_info = pd.DataFrame({  
    "Name": ["ZhangSan", "LiSi"],  
    "Age": [30, 28]  
})  
exam_result = pd.DataFrame({  
    "Name": ["LiSi", "ZhangSan"],  
    "血糖": [5.2, 6.1],  
    "血压": [120, 130]  
})  
# 横向拼接：将两个表按列合并（注意行顺序要对齐）  
df_concat_col = pd.merge(base_info, exam_result, on="Name")  
'''  
使用 Pandas 的 merge 方法，将两个 DataFrame 合并。  
on="Name"：指定以 "Name" 列为键（key）进行合并，只有 "Name" 列中匹配的行会被合并。  
如果两个 DataFrame 中 "Name" 列的值不完全匹配，默认只保留匹配的部分（内连接，how="inner"）。  
合并结果：  
如果 base_info 和 exam_result 中 "Name" 列的值有相同的部分，这些行会被合并，其他列的数据会拼接到一起。  
如果需要保留所有行或指定不同的合并方式，可以通过 how 参数设置（如 how="outer"、how="left"、how="right"）。  
这通常用于将不同表格中的信息整合到一起，例如将病人的基本信息和检查结果合并成一张表。  
'''
print("横向拼接后的表格：")  
print(df_concat_col)

'''Output
	Name  Age   血糖   血压
0  ZhangSan   30  6.1  130
1      LiSi   28  5.2  120
'''
```
















