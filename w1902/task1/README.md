### Task2.1数据预处理

任务说明：对数据进行探索和分析：
数据类型的分析
无关特征删除
数据类型转换
缺失值处理
……以及你能想到和借鉴的数据分析处理

[文档地址](https://shimo.im/docs/yrL0ntLtNLUKXl8r)

#### python一些小技巧

- 缺失值处理sklearn.preprocessing.Imputer(missing_values='NaN', strategy='mean', axis=0, verbose=0, copy=True)
  - strategy通常取均值或者中值'median'
  - 处理类别变量的缺失值使用前向或者后向填充data.ffill(),data.bfill()
  
- data.nunique()查看数据框的重复值
- pd.set_option('display.max_columns', None)用于展示全部列
