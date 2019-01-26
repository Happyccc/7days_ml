### Task2.1数据预处理

任务说明：对数据进行探索和分析：
数据类型的分析
无关特征删除
数据类型转换
缺失值处理
……以及你能想到和借鉴的数据分析处理

[文档地址](https://shimo.im/docs/yrL0ntLtNLUKXl8r)

#### sklearn包学习

- 划分数据集sklearn.model_selection.train_test_split
  - [sklearn地址](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)
  - X_train,X_test,y_train,y_test = train_test_split(X, y, test_size=.3, random_state=2018)
  - stratify参数定义按照X还是y的比例分割train和test，一般定义stratify=y
  
- 预测predict和predict_proba
  - predict_proba预测类别的概率值,如果是2分类一般取概率值的第二列（class=1）
  - 有些model如SVC要在参数中申明才能使用predict_proba，如SVC中要加入probability=True参数
  - 有些model没有predict_proba属性，这时候使用决策函数
```python
if hasattr(clf, "predict_proba"):
            prob_pos = clf.predict_proba(X_test)[:, 1]
else:  # use decision function
    prob_pos = clf.decision_function(X_test)
    prob_pos = \
        (prob_pos - prob_pos.min()) / (prob_pos.max() - prob_pos.min())
```

- 模型评估sklearn.metrics
  - [sklearn模型评估地址](https://scikit-learn.org/stable/modules/model_evaluation.html#classification-metrics)
  - metrics.accuracy_score(y_test,y_pred) 准确度
  - metrics.f1_score(y_test,y_pred,average='weighted') F1-score
  - fpr,tpr,thresholds = metrics.roc_curve(y_test,y_proba[:,1]) ROC曲线
  - auc = metrics.roc(fpr,tpr) AUC值
