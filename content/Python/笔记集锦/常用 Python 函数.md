函数是==用于组织代码的结构化方式，它将一组操作封装起来，以便重复使用和提高代码的可读性==。函数可以接受输入（参数），执行特定任务，并返回输出（结果）。
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506051849466.png)
### 函数的特点：
1. **封装性**：将一组代码逻辑封装在一个函数中，避免重复代码。
2. **可复用性**：定义一次，可以在多个地方调用。
3. **可维护性**：通过函数划分代码逻辑，便于维护和调试。
### 函数的定义和调用：
```python
# 示例：定义一个函数，用于根据身高和体重计算BMI  
def calculate_bmi(height_cm, weight_kg):  
    """  
    参数：  
        height_cm：身高（厘米）  
        weight_kg：体重（千克）  
    返回：        计算后的 BMI 值（浮点数，保留两位小数）  
    """    height_m = height_cm / 100  # 转换为米  
    bmi = weight_kg / (height_m ** 2)  
    return round(bmi, 2)  # 返回保留两位小数的 BMI  
# 调用函数，传入两个参数  
bmi_result_1 = calculate_bmi(165, 65)  
bmi_result_2 = calculate_bmi(177, 81)  
# 输出结果  
print("计算得到的个体1的BMI值为：", bmi_result_1)  
print("计算得到的个体2的BMI值为：", bmi_result_2)
```
#### 定义函数：
使用 `def` 关键字定义函数，语法如下：
```python
def 函数名(参数):
    函数体
    return 返回值
```

#### 示例：
```python
def add_numbers(a, b):
    """计算两个数的和"""
    return a + b

# 调用函数
result = add_numbers(3, 5)
print("结果是：", result)  # 输出：结果是：8
```

### 函数的组成：
1. **函数名**：用于标识函数，应该具有描述性。
2. **参数**：函数的输入，可以是多个。
3. **函数体**：执行的代码逻辑。
4. **返回值**：通过 `return` 返回结果。

### 函数的优势：
- 提高代码的可读性和复用性。
- 便于调试和扩展。
- 支持模块化编程。