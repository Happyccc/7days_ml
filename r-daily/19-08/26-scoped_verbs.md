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

_if allows you to perform an operation on variables that satisfy some logical criteria such as is.numeric() or is.character()

- select_if
```r
df %>% select_if(is.numeric)

## more complex logical statements
df %>% select_if(~sum(is.na(.x)) >0)
```

- rename_if
```r
df %>% rename_if(is.numeric, ~paste0("num_",.x))
```

- mutate_if
```r
df %>% mutate_if(~sum(is.na(.x)>0, 
        ~if_else(is.na(.x),"missing",as.character(.x)))
```

- summarise_if
```r
mode <- function(x) names(sort(table(x)))[1]
df %>% summarise_if(is.character, mode)

df %>% group_by(species) %>%
  summarise_if(is.numeric, mean, na.rm = TRUE)
```

#### _at类

vars()函数选择变量：可以直接写变量字符名，也可以使用select选择器
- select helper:
 - starts_with()
 - ends_with()
 - contains()
 - matches()
 - one_of()
 - num_range(): select(num_range("V", 1:3))--V1, V2, V3
 
funs()函数可定义多个函数，～ 一般只用于一个函数

- select/select_at
```r
df %>% select(matches("date"))
```

- filter_at
```r
library(nycflights13)
## 筛选出所有以wind开头的且所有值都是缺失值的行
weather %>% filter_at(vars(starts_with("wind")), all_vars(is.na(.)))
```

- rename_at
```r
## 将所有含有av的列名替换成AV
df %>% rename_at(vars(contains("av")), ~gsub("av","AV", .x))
```

- mutate_at
```r
df %>% mutate(start_date = mdy_hms(start_date), end_date = mdy_hms(end_date))
df %>% mutate_at(vars(start_date,end_date), mdy_hms)
df %>% mutate_at(vars(ends_with("_date")), mdy_hms)
```

- summarise_at
```r
df %>% summarise_at(vars(contains("interacted")), ~sum(.x == "Yes"))
df %>% summarise_at(vars(-z), funs(min,max))
```

#### _all类

- rename_all
```r
## 将所有列名中的"_"替换成"."
df %>% rename_all(~gsub("_", ".", .x))
```

- filter_all
```r
library(nycflights13)
weather %>% filter_all(any_vars(is.na(.)))
```

- mutate_all
```r
## 将所有元素*25，再四舍五入
df %>% mutate_all(as.numeric)
df %>% mutate_all(~ round(. *25))
df %>% mutate_all(funs(half = . / 2, double = . * 2))  # 新增_half列和_double列
df %>% transmute_all(funs(half = . / 2, double = . * 2)) # 新增_half列和_double列,且去除原先列

```

- summarise_all
```r
## 计算每列非重复entry个数
df %>% summarise_all(n_distinct)

## 计算按species分组的均值、偏差和变异系数
df %>% group_by(species) %>%
  summarise_all(funs(mean,sd,cv = sd(.)/mean(.)))
```

