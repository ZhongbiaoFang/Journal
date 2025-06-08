# 2025 年 6 月
##  2025.06.05—2025.06.06
- [ ] **Python 编程环境搭建**（Python 3.13.4，PyCharm，VScode Python 插件）
	- [Mac 版本最新安装教程]( https://www.bilibili.com/video/BV1rkwpe8ESS/?spm_id_from=333.337.search-card.all.click&vd_source=ed454fb5abc4ece541f1de7a074d0004 )
	- [Windows 版本](https://www.bilibili.com/video/BV1gGccemEeg?spm_id_from=333.788.recommend_more_video.-1&vd_source=ed454fb5abc4ece541f1de7a074d0004)
	- pip 安装 **Python 库** [[Pip 安装包注意事项]]
- [ ] **Python 基础语法学习** 
	- *学习目标：理解 Python 的基本语法结构、控制语句和函数编写，为后续数据分析打下基础*。
	- 学习内容：
		- 1. 变量与数据类型 （int, float, str, bool, list, dict, tuple）
		- 2. 运算符与表达式
		- 3. 注释与代码规范
		- 4. 条件语句 （if /elif / else）
		- 5. 循环语句（for，while）
		- 6. 函数的定义与调用
---
- [ ] ==后续学习计划==：学习数据分析中必须掌握的 Python 库
	- 数据基础操作及可视化： `Numpy`, `Pandas`, `Matplotlib + Seaborn`
	- 机器学习模型库：`scikit-learn + scikit-survival`

## 2025.06.07-2025.06.08
- [ ] 学习 Python 数据基础操作库 `Numpy` 和 `Pandas`
	- `Numpy`：
		- Numpy 在临床预测模型的数据处理中扮演**基础设施角色**，主要负责**数值计算/转换**。适合处理**大规模临床数据集**（如电子病历、影像数据）。
		- 目前初步学习 Numpy 库的内容包括：
			- 一维、二维数据集的创建
			- 库中常用统计函数的应用：例如一键计算整列患者血压的平均值±标准差
	- `Pandas`
		- Pandas 是以 NumPy 为基础构建的 Python 核心数据分析库，专攻**表格型数据（结构化数据）的高效处理**。在临床预测模型中，它与 NumPy 深度协同，形成“Pandas 负责数据整合与清洗 → NumPy 驱动数值计算 → 机器学习建模”的高效模式
		- 目前初步学习 Pandas 库的内容包括：
			- 高效读取和写入常用数据格式（如 CSV、Excel），将患者ID、诊断编码、实验室指标等整合为统一表格
			- 数据简单清洗操作：包括数据整合拼接、数据简单清洗操作（一键去除重复行、填补缺失数据等）
			- 数据转化：将 DataFrame 转为 NumPy 数组供 Scikit-learn 库进行机器学习分析
- [ ] 学习 Python 数据可视化库 `Matplotlib` 和`Seaborn`
	- Matplotlib 和 Seaborn 是 Python 中最核心的可视化库，二者在功能上互补，常用于临床数据的探索性分析、结果呈现及模型评估。其可以直接调用 Pandas 转化后的数据进行图像绘制。Seaborn 支持更美观高级的图像绘制，可绘制更适用于文章发表的统计图。
	- 目前初步学习可视化库的内容，包括基础折线图、柱状图、散点图、箱线图、热图的绘制 ![image.png|575](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506082010037.png)
- [ ] ==后续学习计划==：机器学习模型库 `scikit-learn + scikit-survival` 










