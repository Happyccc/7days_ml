## mutate/summarise/select/filter/rename & all/if/at 等范围动词

[参考文档](http://www.rebeccabarter.com/blog/2019-01-23_scoped-verbs/)

#### 相似方法
- 1、sapply
```r
sapply(df, function(x) sum(is.na(x))
```
- 2、purrr::map
```r
df %>% map_dbl(function(x) sum(is.na(x))
df %>% map_dbl(~sum(is.na(.x)))
```

#### _if类

