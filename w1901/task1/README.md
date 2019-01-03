
### Task1.1模型构建

任务说明：将金融数据集三七分，随机种子2018，调用sklearn包，简单构建逻辑回归、SVM和决策树3个模型并对每一个模型进行评分，评分方式任意，例如准确度和auc值。（在任务1中不需要考虑数据预处理和模型调参）

[文档地址](https://shimo.im/docs/fesneneLOQ08ZI63)

#### sklearn包学习

- 划分数据集sklearn.model_selection.train_test_split
  - [sklearn地址](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)
  - X_train,X_test,y_train,y_test = train_test_split(X, y, test_size=.3, random_state=2018)
  - stratify参数定义按照X还是y的比例分割train和test，一般定义stratify=y
  
- 预测predict和predict_proba
  - predict_proba预测类别的概率值,如果是2分类一般取概率值的第二列（class=1）
  - 有些model没有predict_proba属性，这时候使用决策函数
```python
if hasattr(clf, "predict_proba"):
            prob_pos = clf.predict_proba(X_test)[:, 1]
else:  # use decision function
    prob_pos = clf.decision_function(X_test)
    prob_pos = \
        (prob_pos - prob_pos.min()) / (prob_pos.max() - prob_pos.min())
```

- 
