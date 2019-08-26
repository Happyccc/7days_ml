## mutate/summarise/select/filter/rename & all/if/at 等范围动词

[参考文档](http://www.rebeccabarter.com/blog/2019-01-23_scoped-verbs/)

#### 相似方法
- sapply
```r
sapply(df, function(x) sum(is.na(x))
```
- purrr::map
```r
df %>% map_dbl(function(x) sum(is.na(x))
df %>% map_dbl(~sum(is.na(.x)))
```

#### _if类

- select_if
```r
df %>% select_if(is.numeric)

## more complex logical statements
df %>% select_if(~sum(is.na(.x)) >0)
```
