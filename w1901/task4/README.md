### Task1.4模型调优

任务说明：使用网格搜索法对7个模型进行调优（调参时采用五折交叉验证的方式），并进行模型评估，记得展示代码的运行结果~

[文档地址](https://shimo.im/docs/7ISamfEnhLYIXAOd)

#### sklearn包学习

- 数据标准化sklearn.preprocessing.StandardScaler
  - [sklearn地址](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)
  - scaler = sklearn.preprocessing.StandardScaler(copy=True, with_mean=True, with_std=True)
  - 数据归一化和标准化的作用是加速迭代速度（使用优化算法时圆形解平面比椭圆形解平面更快收敛）
  - 数据归一化和标准化对概率/树形模型没有效果，因为它只关心变量的概率分布而不关心变量值，DT和ensemble算法等就属于此类
 
- 调参+交叉验证sklearn.model_selection.GridSearchCV和RandomizedSearchCV
  - [sklearn地址](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)
  - sklearn.model_selection.GridSearchCV(estimator, param_grid, scoring=None, cv='warn')
  - sklearn.model_selection.RandomizedSearchCV(estimator, param_distributions, n_iter=10, scoring=None, cv='warn')
  - 网格搜索查找搜索范围内的所有点来确定最优值，先使用较广的范围和步长确定最优解大致位置，然后逐步缩小范围和步长，来寻求最优解，但消耗较多资源
  - 随机搜索与网格搜索类似，只是在搜索范围内随机取点而非选取所有值，速度更快，但也没办法保证最优值 
  - [贝叶斯优化搜索](https://zhuanlan.zhihu.com/p/29779000)在测试一个新点时候会充分利用之前点的信息，在探索和利用间平衡以防陷入局部最优
  - [Google Vizer](https://github.com/tobegit3hub/advisor)
  
  
 
  
  
