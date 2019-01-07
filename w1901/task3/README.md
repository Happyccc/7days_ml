### Task1.3 模型评估

记录7个模型（逻辑回归、SVM、决策树、随机森林、GBDT、XGBoost和LightGBM）关于accuracy、precision，recall和F1-score、auc值的评分表格，并画出ROC曲线。

[文档地址](https://shimo.im/docs/NTt9uqcuPhETs6w6)

#### 结果分析

- 测试集上ensemble模型表现得更好，其中XGB的准确率和AUC都为最高；
- 非ensemble模型在没有做特征工程和数据预处理时表现很差；
- SVM的运行时间一般较长，这是制约其在比赛中大量使用的重要原因；
- 由于时间关系，下次对模型进行简单预处理后分析其效果。
