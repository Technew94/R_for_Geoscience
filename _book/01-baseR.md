# (PART\*) Base R 

# Base R you have to know 

## 安装与配置


## R? 是啥，干啥用的？

1992年，奥克兰大学的两位统计学大佬Ross Ihaka和Robert Gentleman为了给学生授课方便，两人一商量，市面上统计软件太烂，咱自己弄一个多好，大佬果然不一般，几句话的事就敲定了一个软件。大佬长这样：

![*Ross Ihaka and Robert Gentleman, the creators of R.*](images/creators.jpg)

R内置了很多的基础函数，像求和、比较大小等等，在我刚接触R是我非常疑惑，除了这些耳熟能详的函数外，R到底内置了多少函数呢？有的时候自己傻傻的写函数想要实现某些功能，到头来却发现R中有现成的可以用，真是浪费时间和精力。[The R Base Package](https://stat.ethz.ch/R-manual/R-devel/library/base/html/00Index.html) 会是你的好帮手。

平时在小红书，微博，B站等经常看到有人做数据分析师等，他们掌握的语言工具并不止一种，R，Python，stata等都是需要用到的，但对于入门级选手来说，R是最友好的，也是最容易让你产生成就感的。

## Vector(向量)

Vector是R中的一种基础数据结构，它包含相同类型的元素。数据类型可以是逻辑、整数、双精度、字符、复杂或原始。

举个例子，现在我们有1到5，5个整数，想要把他们组成一个向量应该怎么操作呢？

```r
x <- c(1,2,3,4,5)
x
#> [1] 1 2 3 4 5
```
这里我们用`c()`函数来把1，2，3，4，5组合起来，然后通过`<-`这个符号把这个值赋给`x`，这样就把一个简单的向量给构建完成了。请仔细体会这句话的涵义，先把第一要做的事情`组合1，2，3，4，5`完成，然后再赋值给一个变量`x`，请牢记这里的思路，这对后续R的运算是十分有帮助的。
当然了，大家刚接触R心里肯定会有疑问，这个`c()`到底是干啥的，这个函数除了这么简单的组合起一个向量，还能做点别的不？这里就讲到一个非常重要的点，即查阅！学东西得会学，不能说是看了这本书讲了这样做，你能模仿下来，换本书举了个不一样的例子你就懵了，那相当于啥也没学，净看作者耍贫嘴去了。所以当对一个函数不了解或者想要刨根问底时，`??`小问号就排上用场了，我们在`Console`中输入`??c()`，右侧的Help页面就会弹出来关于该函数的帮助文档，请记住任何人都不会比函数开发者更加了解自己的函数是干啥的，同理以后若遇到新的函数你就知道该怎么做了。

当然了，R也是一门语言，和其他语言一样，也是各种符号骚操作满天飞，不过不必惊慌，常用的也就那么几个，大神们也只是用的多了，脑子里记得的比我们更多一些，你与大神的差距真的就只是练的用的太少了（其实大神也是需要google的）。那这里就介绍本书的第一个符号`:`,中文里我们用作冒号，在R中我们可以理解为`到`，打个样给你看看，还是以上面的构造向量为例，

```r
x <- c(1:5)
x
#> [1] 1 2 3 4 5
```

开头我们讲了，vector有很多不同的类型，那么我们在看到一个向量时怎么去看看它到底是啥类型呢？这时候需要用到`typeof()`这个函数，

```r
typeof(x)
#> [1] "integer"
```
除了类型之外，向量还有另外一个十分重要的特征就是长度（length）,`length()`可以用来查看向量长度，

```r
length(x)
#> [1] 5
```
自己动手输入数值还是挺麻烦的，R中的`seq()`可以帮助我们更快的创造一个向量，打个样，

```r
seq(1, 9, 0.5)
#>  [1] 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0 5.5 6.0 6.5 7.0 7.5
#> [15] 8.0 8.5 9.0
```
很神奇有没有，爱心算的你很快就知道了这行代码的意思是从1到9每间隔0.5输出一个值，但是为啥要这3个数字这么排列呢？这时候就得小问号`??`上场了，在Console中输入  
`??seq`  
此时看到右侧`Help`界面的你心里默默念了一句什么鬼，能理解，换谁谁也蒙圈，啥呀都是，乱七八糟的这，莫慌，仔细看是不是这些蓝色的都有一个规律，就是里面都有一个`::`这个符号，两个小冒号连在一起，啥意思呢？`包::函数`，`package::function`，第一个就是cli这个包里的ansi_regex函数的意思，第二个就是cli这个包里的ansi_strip函数的意思。所以我们要找的应该是`base::seq`这个函数，为啥呢，看后面那句解释啊，sequence generation，这不写的生成随机数嘛。  
点击进去以后一看还是有点懵，莫慌，一步步来，首先看`Description`知道这个函数是用来构造随机数的。然后`Usage`,`seq(...)`这个的意思就是告诉你，你要用我生成随机数，格式就是这样的`seq`开头，跟着个`()`,括号里呢就要开始放条件了，都有啥条件呢，咱们来看下面的`Arguments`,`from`说白了就是从几开始，`to`就是到哪个数结束，`by`就是前面俩数的间隔是多少，就这么简单。看到这之后心里就有个初步印象了，然后蹦过中间段直接到最后的`Example`，直接贴心的给你放上几个例子，每个开发者都是生怕你不会用我的包啊，就差现场给你讲咋用了，于我而言也是一样的，把例子每一个都运行一遍，看看每一步都产生了啥结果，运行几次然后再回头对照上面的解释文档，也就差不多掌握了这个函数的基本用法了。

看到这我们再来放上其他几个数据类型的vector，

```r
# Vector of logical values
log_values <- c(TRUE, FALSE, TRUE, FALSE)

log_values
#> [1]  TRUE FALSE  TRUE FALSE
```
忘了讲，`#`井号键这个小符号挺好用，干啥的呢，注释掉一句话，说人话就是我这句话写在这了，但R你别给我运行，这句话就是提醒自己下面的代码是要干啥的，防止自己以后再回来看到自己写的东西一整个懵住，现在我也一直保持这个习惯，因为每天看的东西很多，回看过去的东西时经常会忘记当时为啥要这么写，还是挺有用处的，好记性不如烂笔头嘛！
回到正文，上面的就是所谓的逻辑型向量，同理我们再构造一个字符型的，

```r
fruits <- c("banana", "apple", "orange", "mango", "lemon", "50")
fruits
#> [1] "banana" "apple"  "orange" "mango"  "lemon"  "50"
```
字符型的呢就要注意要给每一个单词或者数字加上英文双引号。

在实际应用中，有时候我们只想用一个向量中的某个或某几个元素，这时候该咋办呢？这里介绍一种方法，`[]`，中括号，英文`brackets`,比如我要把fruits中的`"banana"`和`"mango"`拿出来，

```r
fruits[c(1,4)]
#> [1] "banana" "mango"
```
前四个：

```r
fruits[1:4]
#> [1] "banana" "apple"  "orange" "mango"
```
如果想要选取除了`"banana`以外的所有元素，这时候可以用减号，

```r
fruits[-1]
#> [1] "apple"  "orange" "mango"  "lemon"  "50"
```
注意这里的数字代表的是各个元素所在位置。

当然了，对向量内元素进行排序也是可以的，遵循原则就是从小到大或者按照首字母排序，函数为`sort`,

```r
fruits <- c("banana", "apple", "orange", "mango", "lemon")
numbers <- c(13, 3, 5, 7, 20, 2)

sort(fruits)  # Sort a string
#> [1] "apple"  "banana" "lemon"  "mango"  "orange"
sort(numbers) # Sort numbers
#> [1]  2  3  5  7 13 20
```
## Lists(列表)
R 中的列表可以在其中包含许多不同的数据类型，列表是有序且可变的数据集合。啥意思呢？
说人话就是甭管啥类型数据都往里搁就完了，要创建列表，使用`list()`函数：打个样，

```r
thislist <- list(
  a = c("apple", "banana", "cherry"),
  b = c(1,2,5,6,7,9),
  c = c(TRUE, FALSE, TRUE)
)
# Print the list
thislist
#> $a
#> [1] "apple"  "banana" "cherry"
#> 
#> $b
#> [1] 1 2 5 6 7 9
#> 
#> $c
#> [1]  TRUE FALSE  TRUE
```
瞅见没，最常见的三种类型都在这个列表里，有点大肚能容一切的意思。
上一节讲向量有属性，列表有没有呢？同样的我们试试，

```r
typeof(thislist)
#> [1] "list"
```

```r
length(thislist)
#> [1] 3
```
## Matrices(矩阵)
矩阵是啥？别看名字吓人，其实也没啥，前面讲向量，列表它们都是一维的，矩阵是具有列(column)和行(row)的二维数据集。列是数据的垂直表示，而行是数据的水平表示。可以使用`matrix()` 函数创建矩阵,打个样，

```r
# Create a matrix
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)

# Print the matrix
thismatrix
#>      [,1] [,2]
#> [1,]    1    4
#> [2,]    2    5
#> [3,]    3    6
```
NOTE:千万别忘了`c()`函数的用法啊，把众多元素组合在一起，怕你忘，提醒一下。
数字矩阵，字符行不行呢？

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

thismatrix
#>      [,1]     [,2]    
#> [1,] "apple"  "cherry"
#> [2,] "banana" "orange"
```
一样一样的，道理都是通的。

Access Matrix Items
You can access the items by using [ ] brackets. The first number "1" in the bracket specifies the row-position, while the second number "2" specifies the column-position:


```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

thismatrix[1, 2]
#> [1] "cherry"
```
The whole row can be accessed if you specify a comma after the number in the bracket:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

thismatrix[2,]
#> [1] "banana" "orange"
```
The whole column can be accessed if you specify a comma before the number in the bracket:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

thismatrix[,2]
#> [1] "cherry" "orange"
```
Access More Than One Row
More than one row can be accessed if you use the c() function:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

thismatrix[c(1,2),]
#>      [,1]     [,2]     [,3]   
#> [1,] "apple"  "orange" "pear" 
#> [2,] "banana" "grape"  "melon"
```
Access More Than One Column
More than one column can be accessed if you use the c() function:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

thismatrix[, c(1,2)]
#>      [,1]     [,2]       
#> [1,] "apple"  "orange"   
#> [2,] "banana" "grape"    
#> [3,] "cherry" "pineapple"
```
Add Rows and Columns
Use the cbind() function to add additional columns in a Matrix:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

newmatrix <- cbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# Print the new matrix
newmatrix
#>      [,1]     [,2]        [,3]    [,4]        
#> [1,] "apple"  "orange"    "pear"  "strawberry"
#> [2,] "banana" "grape"     "melon" "blueberry" 
#> [3,] "cherry" "pineapple" "fig"   "raspberry"
```
Use the rbind() function to add additional rows in a Matrix:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

newmatrix <- rbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# Print the new matrix
newmatrix
#>      [,1]         [,2]        [,3]       
#> [1,] "apple"      "orange"    "pear"     
#> [2,] "banana"     "grape"     "melon"    
#> [3,] "cherry"     "pineapple" "fig"      
#> [4,] "strawberry" "blueberry" "raspberry"
```

Remove Rows and Columns
Use the c() function to remove rows and columns in a Matrix:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange", "mango", "pineapple"), nrow = 3, ncol =2)

#Remove the first row and the first column
thismatrix <- thismatrix[-c(1), -c(1)]

thismatrix
#> [1] "mango"     "pineapple"
```

Check if an Item Exists
To find out if a specified item is present in a matrix, use the %in% operator:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

"apple" %in% thismatrix
#> [1] TRUE
```

Number of Rows and Columns
Use the dim() function to find the number of rows and columns in a Matrix:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

dim(thismatrix)
#> [1] 2 2
```

Matrix Length
Use the length() function to find the dimension of a Matrix:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

length(thismatrix)
#> [1] 4
```

Combine two Matrices
Again, you can use the rbind() or cbind() function to combine two or more matrices together:

```r
# Combine matrices
Matrix1 <- matrix(c("apple", "banana", "cherry", "grape"), nrow = 2, ncol = 2)
Matrix2 <- matrix(c("orange", "mango", "pineapple", "watermelon"), nrow = 2, ncol = 2)

# Adding it as a rows
Matrix_Combined <- rbind(Matrix1, Matrix2)
Matrix_Combined
#>      [,1]     [,2]        
#> [1,] "apple"  "cherry"    
#> [2,] "banana" "grape"     
#> [3,] "orange" "pineapple" 
#> [4,] "mango"  "watermelon"

# Adding it as a columns
Matrix_Combined <- cbind(Matrix1, Matrix2)
Matrix_Combined
#>      [,1]     [,2]     [,3]     [,4]        
#> [1,] "apple"  "cherry" "orange" "pineapple" 
#> [2,] "banana" "grape"  "mango"  "watermelon"
```
## Data Frame(数据框)
数据框是以表格格式显示的数据。

数据框可以在其中包含不同类型的数据。 第一列可以是字符，第二列和第三列可以是数字或逻辑。 但是，每一列都应具有相同类型的数据。

使用 data.frame() 函数创建数据框：

```r
# Create a data frame
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

# Print the data frame
Data_Frame
#>   Training Pulse Duration
#> 1 Strength   100       60
#> 2  Stamina   150       30
#> 3    Other   120       45
```
Use the `summary()` function to summarize the data from a Data Frame:

```r
summary(Data_Frame)
#>    Training             Pulse          Duration   
#>  Length:3           Min.   :100.0   Min.   :30.0  
#>  Class :character   1st Qu.:110.0   1st Qu.:37.5  
#>  Mode  :character   Median :120.0   Median :45.0  
#>                     Mean   :123.3   Mean   :45.0  
#>                     3rd Qu.:135.0   3rd Qu.:52.5  
#>                     Max.   :150.0   Max.   :60.0
```
我们可以使用单括号 `[]`、双括号 `[[ ]]` 或 `$` 来访问数据框中的列：

```r
Data_Frame[1]
#>   Training
#> 1 Strength
#> 2  Stamina
#> 3    Other

Data_Frame[["Training"]]
#> [1] "Strength" "Stamina"  "Other"

Data_Frame$Training
#> [1] "Strength" "Stamina"  "Other"
```

使用 `rbind()` 函数在数据框中添加新行：

```r
# Add a new row
New_row_DF <- rbind(Data_Frame, c("Strength", 110, 110))

# Print the new row
New_row_DF
#>   Training Pulse Duration
#> 1 Strength   100       60
#> 2  Stamina   150       30
#> 3    Other   120       45
#> 4 Strength   110      110
```
使用 `cbind()` 函数在数据框中添加新列：

```r
# Add a new column
New_col_DF <- cbind(New_row_DF, Steps = c(1000, 6000, 2000,5000))

# Print the new column
New_col_DF
#>   Training Pulse Duration Steps
#> 1 Strength   100       60  1000
#> 2  Stamina   150       30  6000
#> 3    Other   120       45  2000
#> 4 Strength   110      110  5000
```

使用 rbind() 函数垂直组合 R 中的两个或多个数据框：

```r
Data_Frame1 <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame2 <- data.frame (
  Training = c("Stamina", "Stamina", "Strength"),
  Pulse = c(140, 150, 160),
  Duration = c(30, 30, 20)
)

New_Data_Frame <- rbind(Data_Frame1, Data_Frame2)
New_Data_Frame
#>   Training Pulse Duration
#> 1 Strength   100       60
#> 2  Stamina   150       30
#> 3    Other   120       45
#> 4  Stamina   140       30
#> 5  Stamina   150       30
#> 6 Strength   160       20
```
使用 cbind() 函数水平组合 R 中的两个或多个数据框：

```r
Data_Frame3 <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame4 <- data.frame (
  Steps = c(3000, 6000, 2000),
  Calories = c(300, 400, 300)
)

New_Data_Frame1 <- cbind(Data_Frame3, Data_Frame4)
New_Data_Frame1
#>   Training Pulse Duration Steps Calories
#> 1 Strength   100       60  3000      300
#> 2  Stamina   150       30  6000      400
#> 3    Other   120       45  2000      300
```

