#### ‘Not Available’ / Missing Values '不可用' / 缺失值


**Description 描述**
NA is a logical constant of length 1 which contains a missing value indicator. NA can be coerced to any other vector type except raw. There are also constants NA\_integer\_, NA\_real\_, NA\_complex\_ and NA\_character\_ of the other atomic vector types which support missing values: all of these are reserved words in the R language.
**NA是长度为1的逻辑常数，它包含一个缺失值指示符。NA可以强制转换到任何其他向量类型，除了raw类型。常数NA \_integer\_，NA\_real\_，NA\_complex\_和Na\_character\_等其他原子向量类型也支持缺失值：所有这些都是在R语言中的保留关键字。**

The generic function is.na indicates which elements are missing.
**通用函数is.na返回哪个元素是缺失的。**

The generic function is.na<- sets elements to NA.
**通用函数is.na<-可以设置元素为NA。**

The generic function anyNA implements any(is.na(x)) in a possibly faster way (especially for atomic vectors).
**通用函数anyNA可以以更快的速度运行代码any(is.na(x))（特别是对原子向量之时）**

**Usage 用法**
```r
NA
is.na(x)
anyNA(x, recursive = FALSE)
```
```r
## S3 method for class 'data.frame'
## S3 方法对于类型'data.frame'
is.na(x)
```
```r
is.na(x) <- value
```
**Arguments 参数**

|     |      |
|-----|------|
|x|an R object to be tested: the default method for is.na handles atomic vectors, lists and pairlists: that for anyNA also handles NULL.**传入一个需要测试的R对象：is.na默认的方法是处理原子向量、列表和成对列表：anyNA也处理NULL。**|
|recursive|logical: should anyNA be applied recursively to lists and pairlists?**逻辑值：anyNA是否会分别应用于列表和成对列表？**|
|value|a suitable index vector for use with x.**一个合适的使用x的索引向量。**|

**Details 详细说明**
The NA of character type is distinct from the string "NA". Programmers who need to specify an explicit missing string should use NA\_character\_ (rather than "NA") or set elements to NA using is.na<-.
**字符类型NA与字符串“NA”不同。程序员需要指定一个明确的缺失字符串应使用NA\_character\_（而不是“NA”）或设置元素NA使用is.na<-。**

is.na and anyNA are generic: you can write methods to handle specific classes of objects, see InternalMethods.
**is.na和anyNA是一般使用的：你可以写方法来处理具体的对象类，参见InternalMethods。**

Function is.na<- may provide a safer way to set missingness. It behaves differently for factors, for example.
**函数is.na<-可以提供一种更安全的方式来设置缺失值。比如说，它对于factors类型来说表现不同。**

Numerical computations using NA will normally result in NA: a possible exception is where NaN is also involved, in which case either might result. Logical computations treat NA as a missing TRUE/FALSE value, and so may return TRUE or FALSE if the expression does not depend on the NA operand.
**使用NA做数值计算通常会导致NA：一个可能的例外是NaN也会出现其中，在这种情况下，可能会导致其中一种结果。逻辑计算将NA视为丢失的真/假值，因此如果表达式不依赖于NA，则返回TRUE或FALSE。**

The default method for anyNA handles atomic vectors without a class and NULL. It calls any(is.na(x) on objects with classes and for recursive = FALSE, on lists and pairlists.
**anyNA的默认方法处理不含class或者NULL的原子向量。它调用any(is.na(x)在类对象上如列表或成对列表，而参数recursive = FALSE。**

**Value 返回值**
The default method for is.na applied to an atomic vector returns a logical vector of the same length as its argument x, containing TRUE for those elements marked NA or, for numeric or complex vectors, NaN, and FALSE otherwise. (A complex value is regarded as NA if either its real or imaginary part is NA or NaN.) dim, dimnames and names attributes are copied to the result.
**对于is.na应用于原子向量默认的方法返回一个与自变量x长度相同的逻辑向量，对那些元素标记是NA的元素显示TRUE，或者对于数字或复杂的向量，显示NaN，否则显示为假。（一个复数值即如果实数部分或者虚数部分是NA或NaN会被视为NA。）dim，dimnames和名称属性会复制到结果中。**

The default methods also work for lists and pairlists:
For is.na, elementwise the result is false unless that element is a length-one atomic vector and the single element of that vector is regarded as NA or NaN (note that any is.na method for the class of the element is ignored).
**默认的方法也适用于列表和成对列表：
对于is.na对应元素的结果是false的，除非该元素是长度为一原子向量，且该向量的单一元素是NA或NaN（注意任何is.na方法对元素的类都被忽略）。**
anyNA(recursive = FALSE) works the same way as is.na;
**anyNA(recursive = FALSE)与is.na运行起来是一样的。**
anyNA(recursive = TRUE) applies anyNA (with method dispatch) to each element.
**anyNA(recursive = TRUE)对每一个元素使用了anyNA（方法的分配）。**

The data frame method for is.na returns a logical matrix with the same dimensions as the data frame, and with dimnames taken from the row and column names of the data frame.
**data frame类型使用is.na会返回拥有和data frame同样维度的逻辑矩阵，并且行和列的名字也是和data frame一样的。
**

anyNA(NULL) is false: is.na(NULL) is logical(0) with a warning.
**anyNA(NULL)是false：is.na(NULL)是有一个警告的logical(0)。**

**References 参考文献**
Becker, R. A., Chambers, J. M. and Wilks, A. R. (1988) The New S Language. Wadsworth & Brooks/Cole.

Chambers, J. M. (1998) Programming with Data. A Guide to the S Language. Springer.

**See Also 相似函数**
NaN, is.nan, etc., and the utility function complete.cases.
**NaN，is.nan，等等，以及效用函数complete.cases。**

na.action, na.omit, na.fail on how methods can be tuned to deal with missing values.
**na.action，na.omit，na.fail用于如何来处理缺失值。**

**Examples 例子**
```r
is.na(c(1, NA))        #> FALSE  TRUE
is.na(paste(c(1, NA))) #> FALSE FALSE
(xx <- c(0:4))
is.na(xx) <- c(2, 4)
xx                     #> 0 NA  2 NA  4
anyNA(xx) # TRUE
```
```r
# Some logical operations do not return NA
# 一些逻辑运算不会返回NA
c(TRUE, FALSE) & NA
c(TRUE, FALSE) | NA
```
```r
## Measure speed difference in a favourable case:
## 使用一个顺利的例子测量速度的不同
## the difference depends on the platform, on most ca 3x.
## 不同由平台决定，大多数是3x。
x <- 1:10000; x[5000] <- NaN  # coerces x to be double # 强制转换x成double型
if(require("microbenchmark")) { # does not work reliably on all platforms # 不是在所有平台都能可靠地运行
  print(microbenchmark(any(is.na(x)), anyNA(x)))
} else {
  nSim <- 2^13
  print(rbind(is.na = system.time(replicate(nSim, any(is.na(x)))),
              anyNA = system.time(replicate(nSim, anyNA(x)))))
}
```
```r
## anyNA() can work recursively with list()s:
## anyNA()可以分别作用于list()s
LL <- list(1:5, c(NA, 5:8), c("A","NA"), c("a", NA_character_))
L2 <- LL[c(1,3)]
sapply(LL, anyNA); c(anyNA(LL), anyNA(LL, TRUE))
sapply(L2, anyNA); c(anyNA(L2), anyNA(L2, TRUE))
```
```r
## ... lists, and hence data frames, too:
## ... 列表， 因此也data frames
dN <- dd <- USJudgeRatings; dN[3,6] <- NA
anyNA(dd) # FALSE
anyNA(dN) # TRUE
```
