![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506061156178.png)
# 数组 array 相比 list 的优势
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506061157829.png)
```python
# 首先导入NumPy库【第一步导入(import)`numpy库`，定义`numpy`为`np`】  
import numpy as np  
## 1. NumPy 是什么？为什么不用 list？##  
# 普通的 Python list 是这样的：  
temps_list = [36.5, 37.1, 36.8, 37.5]  # 一组病人的Temperature记录  
# NumPy 的 array 是这样的  
temps_np = np.array(temps_list)  
# list看上去和 np.array 差不多对吧？但试试给每个人Temperature+0.5：  
# print(temps_list + 0.5)  # ❌ 会报错：TypeError  
# 而NumPy 的 array 能直接支持“逐个元素加法”  
temps_np = np.array(temps_list)  
print("每位病人调整后的Temperature：", temps_np + 0.5)
# 输出：每位病人调整后的Temperature： [37.  37.6 37.3 38. ]
```

[[docs/plugins/index|index]]
[测试](https://porkbun.com/account/domainsSpeedy)
[[Introduction]]



# 一维数组的创建与访问 
```python
# 可以把 NumPy 的一维数组看作一个“医学观察日记表”  
temps = np.array([36.6, 37.2, 36.8, 37.5])  
# 用索引访问：从 0 开始！0 是第一个病人  
print("第一位病人的Temperature：", temps[0]) # Python中 0 表示“第一个”  
print("最后一位病人的Temperature：", temps[-1])  
# -1 表示“最后一个”，即从最后面开始数，-2 则表示倒数第二个
```

# 二维数组的创建与访问
```python
## 3. 二维数组：存放“多人多项”指标 ### 示例：每位病人记录三个值：Temperature / Systolic Pressure / Diastolic Pressure  
data = np.array([  
    [36.6, 120, 80],   # 病人1  
    [37.2, 130, 85],   # 病人2  
    [38.0, 145, 95]    # 病人3  
])   
# 二维数组就像“Excel表格”：横是病人，竖是指标  
# 用索引访问：data[行, 列]  
print("病人2的Systolic Pressure：", data[1, 1])  # 第二行 第二列  
print("病人3的Temperature：", data[2, 0])  
  
# 输出  
# 病人2的Systolic Pressure： 130.0
# 病人3的Temperature： 38.0
```

# 切片操作
在 Python 中，切片操作的规则是**左闭右开**，即 `start:end` 表示从索引 `start` 开始（包含 `start`），到索引 `end` 结束（不包含 `end`）。因此，[temps[0:2]](vscode-file://vscode-app/Applications/Visual%20Studio%20Code. app/Contents/Resources/app/out/vs/code/electron-sandbox/workbench/workbench. html) 的含义是：
- 从索引 `0` 开始（第一位）。
- 到索引 `2` 结束（但不包含索引 `2`，只包含索引 `1`）。
所以，[temps[0:2]](vscode-file://vscode-app/Applications/Visual%20Studio%20Code. app/Contents/Resources/app/out/vs/code/electron-sandbox/workbench/workbench. html) 只会取索引 `0` 和 `1` 的元素，即第一位和第二位，而不会取索引 `2` 的元素（第三位）。这种左闭右开的规则是 Python 切片操作的标准行为。
```python
## 4. 切片操作：一次取一片，不用一个一个取 

### 一维数组的切片 #
print("第一位和第二位病人的Temperature：", temps[0:2]) 
# temps为上述定义的一维数组list，[0:2]分别取第一位和第二位（即从第一位开始取两个值）  
# 输出：第一位和第二位病人的Temperature： [36.6 37.2]

# 二维数组的切片 #
'''  
解释：  
- data[行范围, 列范围]  
- “ : ” 表示“所有”，例如 data[:, 1] = 所有行，第2列  
'''  
# 拿出前两位病人的全部指标  
print("前两位病人的全部数据：")  
print(data[0:2, :])  # 0:2 表示“从第0行到第1行”（不包含第2行）  
# 拿出所有人的Systolic Pressure（第2列）  
print("所有人的Systolic Pressure：", data[:, 1])  
'''  
输出  
前两位病人的全部数据：  
[[ 36.6 120.   80. ]  
 [ 37.2 130.   85. ]]
 所有人的Systolic Pressure： [120. 130. 145.]
 '''
```

# 广播机制
广播机制：不需要 for 循环，直接操作整组数据，这将*很大程度上加快运算速度*
- 广播机制是 NumPy 最大的魔法之一  
- 不需要写三重 for 循环，也不需要写 list 解析式  
```python
# 示例：每位病人记录三个值：Temperature / Systolic Pressure / Diastolic Pressure
# 二维数组就像“Excel表格”：横是病人，竖是指标
# 用索引访问：data[行, 列]
data = np.array([
[36.6, 120, 80], # 病人1
[37.2, 130, 85], # 病人2
[38.0, 145, 95] # 病人3
])

# 把每个病人的Temperature+0.5、Systolic Pressure-10、Diastolic Pressure不变  
offsets = np.array([0.5, -10, 0])  
# NumPy 会自动“复制”这组偏差到每一行（广播机制）  
adjusted = data + offsets  
print("服药后调整的数据：")  
print(adjusted)  

'''输出：
服药后调整的数据：  
[[ 37.1 110.   80. ]  
 [ 37.7 120.   85. ] 
 [ 38.5 135.   95. ]]
 '''
```

# 数组的常用统计函数
```python
# 首先导入NumPy库【第一步导入(import)`numpy库`，定义`numpy`为`np`】
import numpy as np
```

- **np.array()**
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506061324151.png)
``aixs = 0：按列计算
``aixs = 1：按行计算
```python
# 用索引访问：data[行, 列]
data = np.array([
[36.6, 120, 80], # 病人1
[37.2, 130, 85], # 病人2
[38.0, 145, 95] # 病人3
])
# 计算每项指标的平均值（按列）  
means = np.mean(data, axis=0) # aixs = 0：按列计算；aixs = 1：按行计算  
print("每项指标的平均值（Temperature、Systolic Pressure、Diastolic Pressure）：", means)  
# 其他常用函数：  
print("最高Temperature：", np.max(data[:, 0]))     # Temperature最大值，[:, 0]表示第一列所有数据（即温度的值）  
print("Systolic Pressure标准差：", np.std(data[:, 1]))  # 血压波动  
print("Diastolic Pressure总和：", np.sum(data[:, 2]))    # 所有人Diastolic Pressure总和  
print("患者收缩压的MEAN ± SD：", np.mean(data[:, 1]), "±", np.std(data[:, 1])) # 所有收缩压的平均值±标准差
'''  
每项指标的平均值（Temperature、Systolic Pressure、Diastolic Pressure）： [ 37.26666667 131.66666667  86.66666667]
最高Temperature： 38.0
Systolic Pressure标准差： 10.274023338281626
Diastolic Pressure总和： 260.0
患者收缩压的MEAN ± SD： 131.66666666666666 ± 10.274023338281626
'''
```




























