### Task1.2 集成模型构建

任务说明：将金融数据集三七分，随机种子2018，调用sklearn包，简单构建逻辑回归、SVM和决策树3个模型并对每一个模型进行评分，评分方式任意，例如准确度和auc值。（在任务1中不需要考虑数据预处理和模型调参）

[文档地址](https://shimo.im/docs/jse5ZZhdvEQR4siC)

#### 模型包学习

- 随机森林sklearn.ensemble.RandomForestClassifier
  - [sklearn地址](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)
  - RandomForestClassifier(n_estimators='warn', criterion='gini', max_depth=None, min_samples_split=2,
                            min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features='auto',
                            max_leaf_nodes=None, min_impurity_decrease=0.0, min_impurity_split=None,
                            bootstrap=True, oob_score=False, n_jobs=None, random_state=None, verbose=0,
                            warm_start=False, class_weight=None)
  - 参数说明：
    - n_estimators：树的个数，默认取100
    - criterion：评估函数，默认'gini'用于CART算法，还可以取'entropy'信息增益用于ID3和C4.5算法
    - max_depth：树的最大深度，默认'None',表示节点会扩展直到所有叶子节点都是纯的或者所有叶子节点包含的样本少于min_samples_split个为止，一般取3-10
    - min_samples_split：内部节点再划分所需最小样本数，默认为2
    - min_samples_leaf：叶子节点含有的最少样本，默认取1
    - min_weight_fraction_leaf：叶子节点最小的样本权重和，默认为0
    - max_features：寻找最好划分时需要考虑的最大的特征数量或特征数量的比例，默认'auto'(还可以取'sqrt','log2','None'和其他int和float)，此时等价于max_features=sqrt(n_features)
    - max_leaf_nodes：最大叶子节点数，默认为None
    - min_impurity_decrease：节点划分最小的不纯度下降值，默认为0.0
    - min_impurity_split：节点划分最小不纯度，如果节点的不纯度高于该阈值，则分裂，否则为叶子节点，默认为1e-7
    - bootstrap：在建立树时是否用bootstrap采样方法，默认为True
    - oob_score：在评估泛化准确率时是否使用包外样本，默认为False
    - random_state：随机器对象，默认为None
    - warm_start：是否使用前一步的结果继续拟合
    - class_weight：给每个类指定权重，形式是：{class_label: weight}，默认为None
  
- GBDT包sklearn.ensemble.GradientBoostingClassifier
  - [sklearn地址](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html)
  - GradientBoostingClassifier(loss='deviance', learning_rate=0.1, n_estimators=100, subsample=1.0,
                              criterion='friedman_mse', min_samples_split=2, min_samples_leaf=1,
                              min_weight_fraction_leaf=0.0, max_depth=3, min_impurity_decrease=0.0,
                              min_impurity_split=None, init=None, random_state=None, max_features=None,
                              verbose=0, max_leaf_nodes=None, warm_start=False, presort='auto',
                              validation_fraction=0.1, n_iter_no_change=None, tol=0.0001)
  - 参数说明：
    - loss：优化的损失函数，对于输出概率值的分类来说，'deviance'等价于logistic regression，对于损失'exponential'梯度提升使用了AdaBoost算法
    - learning_rate：学习速率，默认0.1
    - n_estimators：boosting次数，默认为100
    - subsample：基学习器使用的子采样比例，默认为1.0，小于1时是随机梯度boosting
    - criterion：评估划分质量的函数，默认为'friedman_mse'为均方误差变体 ,还有均方误差'mse'，平均绝对值偏差'mae'
    - presort：是否对数据进行预排序，默认为'auto'
    - validation_fraction：训练数据中抽出一部分作为早停的验证集，这个参数是抽出的比例，默认为0.1
    - n_iter_no_change：当验证集分数在n_iter_no_change次迭代中没有提高时，停止训练，默认为None
    - tol：早停的容忍度，默认为1e-4

- xgboost包xgboost.XGBClassifier
  - [地址](https://xgboost.readthedocs.io/en/latest/python/python_api.html)
  - metrics.accuracy_score(y_test,y_pred) 准确度
  - metrics.f1_score(y_test,y_pred,average='weighted') F1-score
  - fpr,tpr,thresholds = metrics.roc_curve(y_test,y_proba[:,1]) ROC曲线
  - auc = metrics.roc(fpr,tpr) AUC值
