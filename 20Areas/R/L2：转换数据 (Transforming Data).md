# 第2讲：转换数据 (Transforming Data)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#离群值 (Outliers)]]
* [[#逻辑表达式 (Logical Expressions)]]
* [[#使用逻辑向量提取子集 (Subsets with Logical Vectors)]]
* [[#数据框子集 (Subsets of Data Frames)]]
* [[#菜单 (Menus)]]
* [[#转义字符 (Escape Characters)]]
* [[#条件语句 (Conditionals)]]
* [[#合并数据源 (Combining Data Sources)]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

欢迎回到 CS50 的 R 语言编程入门课程！

我们将学习如何删除部分数据、查找特定的数据片段，以及如何获取来自不同来源的不同数据并将它们合并。

## 离群值 (Outliers)

在统计学中，离群值 (Outliers) 是指超出预期范围的数据。

通常，统计学家和数据科学家希望识别离群值以进行特殊考虑。有时需要从计算中删除离群值；而另一些时候，你可能希望在包含离群值的情况下进行分析。

为了演示我们如何在 R 中处理离群值，你可以通过在 R 控制台中输入 `file.create("temps.R")` 在 RStudio 中创建一个新文件。此外，你需要将一个名为 `temps.RData` 的文件下载到你的工作目录中。

要加载数据，我们可以编写如下代码：

```R
# 演示从 .RData 文件加载数据

load("temps.RData")
mean(temps)
```

注意 `load` 函数如何加载名为 `temps.RData` 的数据文件。接着，`mean` 将对这些数据求平均值。

运行此脚本，你可以看到计算结果。

然而，如前所述，基础数据中存在离群值。让我们找出它们。

观察 `temps` 的整体情况，正如讲座视频中所示，我们希望能够直接访问这些离群温度。

回想一下在第 1 周中我们是如何对向量中的数据进行索引 (Index) 的。如下修改你的代码：

```R
# 演示通过索引识别离群值

load("temps.RData")

temps[2]
temps[4]
temps[7]

temps[c(2, 4, 7)]
```

注意 `temps[2]` 将直接访问其中一个离群温度。最后一行代码提取了 `temps` 向量的一个子集 (Subset)，该子集仅包含索引为第 2、4 和 7 的元素。

下一步，我们可以删除离群数据：

```R
# 演示通过索引删除离群值

load("temps.RData")
no_outliers <- temps[-c(2, 4, 7)]

mean(no_outliers)
mean(temps)
```

注意数据已被加载。然后，`no_outliers` 是一个新向量，它仅包含非离群值的温度。名为 `temps` 的向量仍然包含离群数据。

## 逻辑表达式 (Logical Expressions)

逻辑表达式 (Logical expressions) 是通过编程手段回答“是”或“否”问题的方法。逻辑表达式使用逻辑操作符 (Logical operators)，这些操作符用于比较数值。

在 R 中你可以使用许多逻辑操作符，包括：

* == (等于)
* `!=` (不等于)
* `>` (大于)
* `>=` (大于等于)
* `<` (小于)
* `<=` (小于等于)

例如，你可以通过在 R 控制台中输入 `1 == 2` 来询问 1 是否等于 2。结果应该是 `FALSE`（或“不！”）。然而，`1 < 2` 应该是 `TRUE`（或“是！”）。

逻辑值 (Logicals) 是逻辑表达式提供的响应。逻辑值可以是 `TRUE` 或 `FALSE`。这些值也可以分别简写为 `T` 或 `F`。

在代码中使用逻辑操作符，你可以如下修改代码：

```R
# 演示通过逻辑表达式识别离群值

load("temps.RData")

temps[1] < 0
temps[2] < 0
temps[3] < 0
```

注意运行这段代码会在 R 控制台中得到 `TRUE` 和 `FALSE` 的答案。

这段代码可以进一步改进如下：

```R
# 演示比较操作符是向量化的

load("temps.RData")

temps < 0
```

注意运行这段代码将创建一个逻辑向量 (Logical vector)（即逻辑值的向量）。逻辑向量中的每个值都回答了其对应的值是否小于 0。

要识别逻辑表达式为真 (TRUE) 的索引，你可以如下修改代码：

```R
# 演示使用 `which` 返回逻辑表达式为 TRUE 的索引

load("temps.RData")

which(temps < 0)
```

注意，现在向量中小于 0 的温度索引被输出到了 R 控制台。`which` 函数接受一个逻辑向量作为输入，并返回其中值为 `TRUE` 的索引。

在处理离群值时，一个常见的需求是显示低于或高于某个阈值 (Threshold) 的数据。你可以在代码中如下实现：

```R
# 演示通过复合逻辑表达式识别离群值

load("temps.RData")
temps < 0 | temps > 60
```

注意字符 `|` 在表达式中象征“或” (Or)。对于 `temps` 中任何小于 0 或大于 60 的值，此逻辑表达式都将为 `TRUE`。

除了我们之前讨论的逻辑操作符，我们现在在词汇表中增加两个新的：

* `|` (或)
* `&` (与)

注意它们提供了表达“或” (Or) 和“与” (And) 的能力。

你可以进一步改进代码如下：

```R
# 演示使用 `any` 和 `all` 测试离群值

load("temps.RData")

any(temps < 0 | temps > 60)
all(temps < 0 | temps > 60)
```

注意 `any` 和 `all` 接受逻辑向量作为输入。`any` 回答的问题是：“这些逻辑值中有任何一个是真吗？”；`all` 回答的问题是：“所有这些温度都符合条件吗？”

## 使用逻辑向量提取子集 (Subsets with Logical Vectors)

如前所述，我们可以如下创建一个删除离群值的新向量：

```R
# 演示使用逻辑向量提取向量子集

load("temps.RData")
filter <- temps < 0 | temps > 60
temps[filter]
```

注意如何基于逻辑表达式创建了一个名为 `filter` 的新子集提取向量。因此，现在可以将 `filter` 提供给 `temps`，以仅请求 `temps` 中逻辑表达式评估为 `TRUE` 的项。

类似地，可以修改代码以仅过滤那些非离群值的项：

```R
# 演示使用 ! 对逻辑表达式取反

load("temps.RData")
filter <- !(temps < 0 | temps > 60)
temps[filter]
```

注意增加的 `!` 意味着“不等于”或简单的“非” (Not)。

这种取反操作可以用来从数据中彻底删除离群值：

```R
# 演示删除离群值
load("temps.RData")

no_outliers <- temps[!(temps < 0 | temps > 60)]
save(no_outliers, file = "no_outliers.RData")

outliers <- temps[temps < 0 | temps > 60]
save(outliers, file = "outliers.RData")
```

注意现在保存了两个文件。一个排除了离群值，另一个包含了离群值。这些文件保存在工作目录中。

## 数据框子集 (Subsets of Data Frames)

我们如何从数据集中找到我们感兴趣的数据子集？

想象一张记录每只小鸡 (Chick)（幼年鸡！）、每只小鸡喂食的饲料 (Feed) 以及每只小鸡重量 (Weight) 的数据表。你可以从讲座源代码中下载 `chicks.csv` 来查看这些数据。

关闭 RStudio 中之前的文件，让我们通过在 R 控制台中输入 `file.create("chicks.R")` 创建一个新文件。确保你的工作目录中有 `chicks.csv`，然后选择 `chicks.R` 并如下编写代码：

```R
# 读取数据的 CSV 文件

chicks <- read.csv("chicks.csv")
View(chicks)
```

注意 `read.csv` 将 CSV 文件读入一个名为 `chicks` 的数据框 (Data frame) 中。然后查看 `chicks`。

查看上述输出，注意其中有许多 `NA` 值，代表不可用的数据。考虑这可能会如何影响小鸡平均重量的计算。如下修改你的代码：

```R
# 演示包含 NA 值的 `mean` 计算

chicks <- read.csv("chicks.csv")
average_weight <- mean(chicks$weight)
average_weight
```

注意运行这段代码会导致错误，因为某些值无法进行数学评估。

缺失数据 (Missing data) 是统计学中预料之中的问题。作为程序员，你需要决定如何处理缺失数据。你可以如下计算去除 `NA` 值后的小鸡平均重量：

```R
# 演示使用 na.rm 从 mean 计算中删除 NA 值

chicks <- read.csv("chicks.csv")
average_weight <- mean(chicks$weight, na.rm = TRUE)
average_weight
```

注意 `na.rm = TRUE` 将为了使用 `mean` 计算平均值的目的而删除所有 `NA` 值。根据文档，`na.rm` 可以设置为 `TRUE` 或 `FALSE`。

现在，让我们弄清楚每只小鸡吃的食物如何影响它们的重量：

```R
# 演示使用显式索引计算 casein 平均值

chicks <- read.csv("chicks.csv")
casein_chicks <- chicks[c(1, 2, 3), ]
mean(casein_chicks$weight)
```

注意通过显式指定适当的索引创建了 `chicks` 数据框的一个子集。

这并不是一种高效的编程方式，因为我们不应该期望我们的数据永远不改变。我们如何修改代码使其更具灵活性？我们可以使用逻辑表达式来动态提取数据框的子集。

```R
# 演示使用逻辑表达式识别饲料为 casein 的行

chicks <- read.csv("chicks.csv")

chicks$feed == "casein"
```

注意逻辑表达式如何识别 `feed` 列中的每个值是否等于 “casein”。

我们可以如下在代码中利用这个逻辑表达式：

```R
# 演示使用逻辑向量提取数据框子集

chicks <- read.csv("chicks.csv")

filter <- chicks$feed == "casein"
casein_chicks <- chicks[filter, ]
mean(casein_chicks$weight)
```

如讲座前半部分所示，注意创建了一个名为 `filter` 的逻辑向量。操作符。

我们现在拥有了数据框的一个子集。

你可以通过使用 `subset` 函数达到同样的结果：

```R
# 演示使用 `subset` 提取子集

chicks <- read.csv("chicks.csv")

casein_chicks <- subset(chicks, feed == "casein")
mean(casein_chicks$weight, na.rm = TRUE)
```

这个名为 `casein_chicks` 的数据框是使用 `subset` 函数创建的。

现在，有人可能希望在一开始就过滤掉所有 `NA` 值。考虑以下代码：

```R
# 演示使用 `is.na` 识别 NA 值

chicks <- read.csv("chicks.csv")

is.na(chicks$weight)
!is.na(chicks$weight)

chicks$chick[is.na(chicks$weight)]
```

注意这段代码如何使用 `is.na` 来查找 `NA` 值。

可以利用 `is.na` 如下将记录完全删除：

```R
# 演示删除 NA 值并重置行名

chicks <- read.csv("chicks.csv")

chicks <- subset(chicks, !is.na(weight))
rownames(chicks)

rownames(chicks) <- NULL
rownames(chicks)
```

注意这段代码创建了 `chicks` 的一个子集，其中 `is.na(weight)` 等于 `FALSE`。也就是说，`chicks` 仅包含 `weight` 列中不存在 `NA` 的行。但是，如果你关心数据框的行名 (Row names)，请注意——当你删除某些行时，你也删除了这些行对应的行名。你可以通过运行 `rownames(chicks) <- NULL` 来确保行名仍然按顺序升序排列，这将重置所有行的名称。

## 菜单 (Menus)

在 R 中，你可以向用户提供选项。例如，你可以向用户提供他们希望过滤的小鸡饲料类型。

考虑这段代码：

```R
# 演示按饲料类型查看数据的交互式程序

# 读取并清理数据
chicks <- read.csv("chicks.csv")
chicks <- subset(chicks, !is.na(weight))

# 确定饲料选项
feed_options <- unique(chicks$feed)

# 提示用户选项
cat("1.", feed_options[1])
cat("2.", feed_options[2])
cat("3.", feed_options[3])
cat("4.", feed_options[4])
cat("5.", feed_options[5])
cat("6.", feed_options[6])
feed_choice <- as.integer(readline("Feed type: "))
```

注意这段代码使用 `unique` 来发现独立的唯一饲料选项。每一个饲料选项随后使用 `cat` 输出。

这段代码在显示各种饲料选项的意义上是可行的，但格式并不是很好。我们如何让不同的选项在 R 控制台中各占一行？

## 转义字符 (Escape Characters)

转义字符 (Escape characters) 是指输出效果与其输入方式不同的字符。

例如，一些常用的转义字符有 `\n`（打印新行）或 `\t`（打印制表符）。

利用转义字符，我们可以如下修改代码：

```R
# 演示 \n

# 读取并清理数据
chicks <- read.csv("chicks.csv")
chicks <- subset(chicks, !is.na(weight))

# 确定饲料选项
feed_options <- unique(chicks$feed)

# 提示用户选项
cat("1.", feed_options[1], "\n")
cat("2.", feed_options[2], "\n")
cat("3.", feed_options[3], "\n")
cat("4.", feed_options[4], "\n")
cat("5.", feed_options[5], "\n")
cat("6.", feed_options[6], "\n")
feed_choice <- as.integer(readline("Feed type: "))
```

注意这如何将所有饲料选项输出在独立的行上。

虽然我们显示了正确类型的菜单，但从设计角度来看，我们仍然可以改进代码。例如，为什么我们要重复所有这些 `cat` 行？如下简化你的代码：

```R
# 演示按饲料类型查看数据的交互式程序

# 读取并清理数据
chicks <- read.csv("chicks.csv")
chicks <- subset(chicks, !is.na(weight))

# 确定饲料选项
feed_options <- unique(chicks$feed)

# 格式化饲料选项
formatted_options <- paste0(1:length(feed_options), ". ", feed_options)

# 提示用户选项
cat(formatted_options, sep = "\n")
feed_choice <- as.integer(readline("Feed type: "))
```

注意 `formatted_options` 包含了所有独立的饲料选项。这个向量中的每个元素都由 `cat(formatted_options, sep = "\n")` 打印并由换行符分隔。

现在，正如我们之前指出的，我们的目的是创建一个交互式程序。因此，我们现在可以提示用户进行选择：

```R
# 演示按饲料类型查看数据的交互式程序

# 读取并清理数据
chicks <- read.csv("chicks.csv")
chicks <- subset(chicks, !is.na(weight))

# 确定饲料选项
feed_options <- unique(chicks$feed)

# 格式化饲料选项
formatted_options <- paste0(1:length(feed_options), ". ", feed_options)

# 提示用户选项
cat(formatted_options, sep = "\n")
feed_choice <- as.integer(readline("Feed type: "))

# 打印选择的选项
selected_feed <- feed_options[feed_choice]
print(subset(chicks, feed == selected_feed))
```

注意用户是如何被提示输入 `Feed type: ` 的，其中一个数字可以转换为饲料选项的文本表示。然后，他们选择的 `feed_choice` 被赋值给 `selected_feed`。最后，与 `selected_feed` 相对应的子集被输出给用户。

然而，你可以想象用户可能不会按预期操作。例如，如果用户输入了 0，这并不是一个潜在的选择，我们程序的输出将会很奇怪。我们如何确保用户输入正确的文本？

## 条件语句 (Conditionals)

条件语句 (Conditionals) 是确定条件是否已满足的方法。

考虑以下代码：

```R
# 演示按饲料类型查看数据的交互式程序

# 读取并清理数据
chicks <- read.csv("chicks.csv")
chicks <- subset(chicks, !is.na(weight))

# 确定饲料选项
feed_options <- unique(chicks$feed)

# 格式化饲料选项
formatted_options <- paste0(1:length(feed_options), ". ", feed_options)

# 提示用户选项
cat(formatted_options, sep = "\n")
feed_choice <- as.integer(readline("Feed type: "))

# 无效选择？
if (feed_choice < 1 || feed_choice > length(feed_options)) {
  cat("Invalid choice.")
}

selected_feed <- feed_options[feed_choice]
print(subset(chicks, feed == selected_feed))
```

注意 `if (feed_choice < 1 || feed_choice > length(feed_options))` 是如何确定用户的输入是否落在值范围之外的。如果是，程序显示 “Invalid choice.”。然而，仍然有一个问题：即使选择了无效选项，程序仍会继续运行。

可以利用 `if` 和 `else` 如下操作，以便仅在用户输入有效选择时才运行最终计算：

```R
# 演示按饲料类型查看数据的交互式程序

# 读取并清理数据
chicks <- read.csv("chicks.csv")
chicks <- subset(chicks, !is.na(weight))

# 确定饲料选项
feed_options <- unique(chicks$feed)

# 格式化饲料选项
formatted_options <- paste0(1:length(feed_options), ". ", feed_options)

# 提示用户选项
cat(formatted_options, sep = "\n")
feed_choice <- as.integer(readline("Feed type: "))

# 无效选择？
if (feed_choice < 1 || feed_choice > length(feed_options)) {
  cat("Invalid choice.")
} else {
  selected_feed <- feed_options[feed_choice]
  print(subset(chicks, feed == selected_feed))
}
```

注意，包裹在 `if` 中的代码仅在存在无效选择时运行。包裹在 `else` 中的代码仅在不满足先前 `if` 中的条件时运行。

## 合并数据源 (Combining Data Sources)

作为本讲座的最后一个事项，让我们研究如何合并数据源。

想象一张代表客户销售额的表，就像亚马逊可能拥有的那样。

你可以想象数据分布在许多张表中的场景。如何从多个来源合并这些数据？

考虑以下名为 `sales.R` 的代码：

```R
# 读取 4 个独立的 CSV 文件

Q1 <- read.csv("Q1.csv")
Q2 <- read.csv("Q2.csv")
Q3 <- read.csv("Q3.csv")
Q4 <- read.csv("Q4.csv")
```

注意每个季度的财务数据（如 Q1 和 Q2）是如何被读入它们各自的数据框中的。

现在，让我们合并来自这四个数据框的数据：

```R
# 使用 `rbind` 合并数据框

Q1 <- read.csv("Q1.csv")
Q2 <- read.csv("Q2.csv")
Q3 <- read.csv("Q3.csv")
Q4 <- read.csv("Q4.csv")

sales <- rbind(Q1, Q2, Q3, Q4)
```

注意 `rbind` 被用来将每个数据框中的数据聚集在一起。

值得一提的是，`rbind` 在这种情况下是可用的，因为所有四个数据框的结构都是相同的。

之前运行的程序结果是 `sales` 包含了每个数据框的每一行。它不是为每个客户显示 Q1、Q2 等，而只是在文件底部为每一行数据创建新行。因此，随着越来越多的数据被合并到其中，文件变得越来越长。目前完全不清楚每笔销售额发生在哪一个季度。

我们的代码可以改进，为每条记录创建一个财务季度列，如下所示：

```R
# 向数据框添加季度列

Q1 <- read.csv("Q1.csv")
Q1$quarter <- "Q1"

Q2 <- read.csv("Q2.csv")
Q2$quarter <- "Q2"

Q3 <- read.csv("Q3.csv")
Q3$quarter <- "Q3"

Q4 <- read.csv("Q4.csv")
Q4$quarter <- "Q4"

sales <- rbind(Q1, Q2, Q3, Q4)
```

注意每个季度是如何被添加到特定的 `quarter` 列中的。因此，当 `rbind` 将数据框合并到 `sales` 时，销售数据是按季度列组织的。

作为最后的修饰，让我们增加一个 `value` 列，其中标注了高额回报 (High returns) 和常规回报 (Regular returns)：

```R
# 演示将销售额标记为高价值

Q1 <- read.csv("Q1.csv")
Q1$quarter <- "Q1"

Q2 <- read.csv("Q2.csv")
Q2$quarter <- "Q2"

Q3 <- read.csv("Q3.csv")
Q3$quarter <- "Q3"

Q4 <- read.csv("Q4.csv")
Q4$quarter <- "Q4"

sales <- rbind(Q1, Q2, Q3, Q4)

sales$value <- ifelse(sales$sale_amount > 100, "High Value", "Regular")
```

注意最后一行代码在 `sale_amount` 大于 100 时分配 “High Value”。否则，交易被分配为 “Regular”。

## 总结 (Summing Up)

在本课中，你学习了如何在 R 中转换数据。具体来说，你学习了……

* [[#离群值 (Outliers)]]
* [[#逻辑表达式 (Logical Expressions)]]
* [[#使用逻辑向量提取子集 (Subsets with Logical Vectors)|子集 (Subsets)]]
* [[#菜单 (Menus)]]
* [[#转义字符 (Escape Characters)]]
* [[#条件语句 (Conditionals)]]
* [[#合并数据源 (Combining Data Sources)]]

下次见，届时我们将讨论 [[L3：应用函数 (Applying Functions)|如何编写我们自己的函数]]。