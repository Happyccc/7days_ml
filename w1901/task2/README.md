### Task1.2 集成模型构建

构建随机森林、GBDT、XGBoost和LightGBM这4个模型，并对每一个模型进行评分，评分方式任意，例如准确度和auc值。

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
  - XGBClassifier(max_depth=3, learning_rate=0.1, n_estimators=100, silent=True, objective='binary:logistic',
                   booster='gbtree', n_jobs=1, nthread=None, gamma=0, min_child_weight=1, max_delta_step=0,
                   subsample=1, colsample_bytree=1, colsample_bylevel=1, reg_alpha=0, reg_lambda=1,
                   scale_pos_weight=1, base_score=0.5, random_state=0, seed=None, missing=None)
  - 参数说明：
    - booster：使用的基学习器，gbtree, gblinear or dart
    - gamma：惩罚项系数，指定节点分裂所需的最小损失函数下降值，默认0
    - min_child_weight：子节点中最小的样本权重和，默认为1
    - colsample_bytree：特征采样比例
    - colsample_bylevel：对于每个划分在每个水平上的样本采样的比例
    - scale_pos_weight：正样本权重，用于样本平衡
    - importance_type：特征重要性类型，默认为gain，有“gain”, “weight”, “cover”, “total_gain” or “total_cover”

- lgbm包lightgbm.LGBMClassifier
  - [地址](https://lightgbm.readthedocs.io/en/latest/Python-API.html)
  - lightgbm.LGBMClassifier(boosting_type='gbdt', num_leaves=31, max_depth=-1, learning_rate=0.1, n_estimators=100,
                             subsample_for_bin=200000, objective=None, class_weight=None, min_split_gain=0.0,
                             min_child_weight=0.001, min_child_samples=20, subsample=1.0, subsample_freq=0,
                             colsample_bytree=1.0, reg_alpha=0.0, reg_lambda=0.0, random_state=None, n_jobs=-1,
                             silent=True, importance_type='split')
  - 参数说明：
    - objective：目标函数，有‘regression’‘binary’‘multiclass’'lambdarank’
    - min_split_gain：最小分割增益，默认为0
    - min_child_weight：叶子节点的最小权重和，默认1e-3
    - min_child_samples：叶子节点最小样本数，默认为20
    - importance_type：特征重要度类型，'split'表示特征被划分次数，'gain'代表特征划分增益，默认为'split'
    
