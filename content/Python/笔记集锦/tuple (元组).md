```python
# 1.6. 元组 tuple：不可变的有序集合，通常用于表示固定结构的数据  
height_weight = (172, 68)   # 一个人的身高(cm) 和 体重(kg)，组成元组  
diabetes_weight = ("yes", 68) # 一个人是否患糖尿病 和 体重(kg)，组成元组  
# 访问元组中的元素（索引从0开始）  
print("身高：", height_weight[0], "cm")  
print("体重：", diabetes_weight[0], diabetes_weight[1], "kg")  
# 查看变量类型  
type(height_weight)  
type(diabetes_weight)  
# 尝试修改→tuple变量是无法修改的！所以会报错  
# height_weight[0] = 175
```
身高： 172 cm
体重： yes 68 kg
Out: tuple







