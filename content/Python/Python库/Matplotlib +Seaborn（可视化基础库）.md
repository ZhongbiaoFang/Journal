# 导入绘图库  
```python
import matplotlib.pyplot as plt  
import seaborn as sns
```

![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506081456465.png)

## 构造模拟数据集
```python
## 构造模拟数据集：8位患者的基本信息 ##data = pd.DataFrame({  
    "Name": ["ZhangSan", "LiSi", "WangWu", "赵六", "钱七", "孙八", "周九", "吴十"],  
    "Gender": ["Male", "Female", "Male", "Female", "Male", "Female", "Male", "Female"],  
    "Temperature": [36.6, 37.2, 36.8, 37.0, 37.1, 36.7, 36.5, 37.3],  
    "Systolic Pressure": [120, 130, 125, 128, 135, 122, 118, 138],  
    "Diastolic Pressure": [80, 85, 82, 84, 88, 78, 76, 90],  
    "BMI": [22.5, 19.8, 24.3, 21.7, 23.1, 20.5, 25.6, 18.9]  
})
```

## 折线图：展示患者编号与Temperature趋势
```python
plt.figure(figsize=(6, 4)) # 开启画布，设置画布大小  
plt.plot(range(1, 9), data["Temperature"], marker="o") # 1-9表示有8个人，Python里默认不包括最后一位。数据调用Temperature。marker="o" 表示在每个数据点上绘制一个圆形标记  
plt.title("Patient Temperature Trend") # 标题  
plt.xlabel("Patient Index") # X轴标签  
plt.ylabel("Temperature (°C)") # Y轴标签  
plt.grid(True) # 呈现网格线，grid：网格  
plt.tight_layout() # 自动调整布局  
plt.savefig('折线图.png') # 保存图像为PNG文件  
plt.show() # 显示图像
```

## 柱状图 `plt.bar`：每位患者的 Systolic Pressure 比较
```python
plt.figure(figsize=(6, 4)) # 开启画布，设置画布大小  
plt.bar(range(1, 9), data["Systolic Pressure"], color="skyblue") # 1-9表示有8个人，Python里默认不包括最后一位。数据调用Systolic Pressure  
plt.title("Systolic Blood Pressure by Patient") # 标题  
plt.xlabel("Patient Index") # X轴标签  
plt.ylabel("Systolic BP (mmHg)") # Y轴标签  
plt.tight_layout() # 自动调整布局  
plt.show() # 显示图像
```

## 散点图 `plt.scatter`：BMI 与 Systolic Pressure 的关系
```python
plt.figure(figsize=(6, 4)) # 开启画布，设置画布大小  
plt.scatter(data["BMI"], data["Systolic Pressure"], color="green") # 绘制散点图，x轴为BMI，y轴为Systolic Pressure  
plt.title("BMI vs. Systolic Blood Pressure") # 标题  
plt.xlabel("BMI") # X轴标签  
plt.ylabel("Systolic BP") # Y轴标签  
plt.tight_layout() # 自动调整布局  
plt.show() # 显示图像
```

## 箱线图 `boxplot`：不同 Gender 患者的 BMI 分布
```python
plt.figure(figsize=(6, 4)) # 开启画布，设置画布大小  
'''  
sns.boxplot(x="Gender", y="BMI", data=data) # sns风格（Seaborn库）  
'''  
grouped_data = [data[data["Gender"] == gender]["BMI"] for gender in data["Gender"].unique()]  # 按性别分组  
'''  
data["Gender"].unique(): 获取 data 数据框中 Gender 列的唯一值（即所有性别的类别，如 "Male" 和 "Female"）。  
data[data["Gender"] == gender]: 通过布尔索引筛选出 Gender 列等于当前性别（gender）的所有行。  
["BMI"]: 从筛选出的数据中提取 BMI 列。  
列表推导式: 遍历 Gender 列的所有唯一值（gender），对每个性别执行上述筛选操作，并将结果存储为一个列表。  
最终结果：grouped_data 是一个列表，其中每个元素是一个 Pandas Series，包含某个性别对应的 BMI 数据。例如：  
grouped_data = [  
    [22.5, 24.3, 25.6],  # 男性 (Male) 的 BMI 数据  
    [19.8, 21.7, 20.5, 18.9]  # 女性 (Female) 的 BMI 数据  
]  
'''  
plt.boxplot(grouped_data, vert=True, patch_artist=True, labels=data["Gender"].unique())  # 绘制分组箱线图  
'''  
作用是绘制分组箱线图，具体解释如下：  
- **`grouped_data`**: 包含按性别分组的 BMI 数据，每个性别对应一个数据组。  
- **`vert=True`**: 设置箱线图为垂直显示（默认值）。  
- **`patch_artist=True`**: 使用填充颜色绘制箱体。  
- **`labels=data["Gender"].unique()`**: 设置每个箱线图的标签，使用 `Gender` 列的唯一值（如 "Male" 和 "Female"）。  
最终效果是展示不同性别的 BMI 数据分布情况，便于比较两组数据的中位数、四分位数和异常值等统计特征。  
'''  
plt.xlabel("Gender") # X轴标签  
plt.title("BMI Distribution by Gender") # 标题  
plt.grid(True) # 呈现网格线  
plt.tight_layout() # 自动调整为紧凑型布局  
plt.show() # 显示图像
```

## 热力图 `heatmap`：数值变量之间的相关性
```python
# 提取数值列计算相关系数矩阵  
data.columns = ['Name', 'gender', 'temperature', 'Systolic', 'Diastolic', "BMI"]  
corr = data[['temperature', 'Systolic', 'Diastolic', "BMI"]].corr()  
'''  
绘制热力图展示数值变量之间的相关性：  
首先，重新命名数据框的列名为 ['Name', 'gender', 'temperature', 'Systolic', 'Diastolic', "BMI"]。  
然后，从数据框中提取数值列（temperature、Systolic、Diastolic、BMI），并计算它们的相关系数矩阵（corr）  
'''  
# 绘图  
plt.figure(figsize=(6, 4))  
sns.heatmap(corr, annot=True, cmap="coolwarm", square=True)  
'''  
使用 Seaborn 的 sns.heatmap 函数绘制热力图，显示这些变量之间的相关性。热力图中：  
annot=True 表示在每个单元格中显示相关系数的数值。  
cmap="coolwarm" 设置颜色映射为冷暖色调。  
square=True 将单元格设置为正方形。  
'''  
plt.title("Correlation Heatmap")  
plt.tight_layout()  
plt.show()
```






