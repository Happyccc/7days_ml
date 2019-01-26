### Task2.1数据预处理

任务说明：对数据进行探索和分析：
- 数据类型的分析
- 无关特征删除
- 数据类型转换
- 缺失值处理
- ……以及你能想到和借鉴的数据分析处理

[文档地址](https://shimo.im/docs/yrL0ntLtNLUKXl8r)

#### python一些小技巧

- 缺失值填充sklearn.preprocessing.Imputer(missing_values='NaN', strategy='mean', axis=0, verbose=0, copy=True)
  - strategy通常取均值或者中值'median'
  - 处理类别变量的缺失值使用前向或者后向填充data.fillna(method='ffill') 或者method取'bfill'
  
- data.nunique()查看数据框的重复值
- pd.set_option('display.max_columns', None)用于展示全部列

- 数据类型转换三种方法
  - 使用astype()函数进行强制类型转换
  - 自定义函数进行数据类型转换
  - 使用Pandas提供的函数如to_numeric()、to_datetime()
  - [参考文档](https://segmentfault.com/a/1190000014713098)
