![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506081616147.png)
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506081616209.png)
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506081630800.png)

```python
## 使用 scikit-learn库 构建随机森林分类模型 ##from sklearn.ensemble import RandomForestClassifier  
from sklearn.datasets import make_classification  
from sklearn.model_selection import train_test_split  
from sklearn.metrics import classification_report  
# 首先生成模拟的二分类结局数据 #X, y = make_classification(n_samples=200, n_features=10, n_informative=5, random_state=42) # 返回两个对象：X为自变量，y为结局变量  
'''  
make_classification 是一个用于生成分类问题数据集的函数，常用于机器学习模型的测试和验证。  
n_samples=200: 指定生成的数据集包含 200 个样本。  
n_features=10: 指定生成的数据集包含 10 个特征（自变量）。  
n_informative=5: 指定 10 个特征中有 5 个是与分类任务相关的（即有信息的特征）。其余特征是冗余或无关的，用于模拟真实数据中的噪声。  
random_state=42: 设置随机种子，确保每次运行代码时生成的数据集是相同的（可复现性）。  
X: 一个二维数组，形状为 (200, 10)，表示 200 个样本的 10 个特征。  
y: 一个一维数组，长度为 200，表示每个样本的分类标签（0 或 1）  
这段代码生成的模拟数据集可以用于训练和测试分类模型，例如逻辑回归、随机森林、支持向量机等。  
'''  
# 1. 划分训练集和测试集  
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=0) # 0.3即30%数据作为测试集；random_state=0 确保每次运行结果一致  
# 2. 选择随机森林模型  
rf = RandomForestClassifier(n_estimators=100, random_state=0) # 模型和超参数指定；random_state=0 确保每次运行结果一致  
# 3. 模型训练  
rf.fit(X_train, y_train)  # fit即拟合模型，训练数据为X_train和y_train  
# 4. 模型预测  
y_pred_rf = rf.predict(X_test) # 测试集分类结果预测  
# 5. 模型评估  
print("随机森林分类结果：") # 输出测试集分类结果  
print(classification_report(y_test, y_pred_rf)) # 准确率、召回率、F1分数
```













