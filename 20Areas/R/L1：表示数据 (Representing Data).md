# 第1讲：表示数据 (Representing Data)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#集成开发环境 (IDE)]]
* [[#创建你的第一个程序 (Creating Your First Program)]]
* [[#函数 (Functions)]]
* [[#错误/漏洞 (Bugs)]]
* [[#readline]]
* [[#paste]]
* [[#文档 (Documentation)]]
* [[#算术 (Arithmetic)]]
* [[#表格 (Tables)]]
* [[#向量 (Vectors)]]
* [[#向量算术 (Vector Arithmetic)]]
* [[#外部数据 (External Data)]]
* [[#特殊值 (Special Values)]]
* [[#因子 (factor)]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

欢迎来到 CS50 的 R 语言编程入门课程！

编程 (Programming) 是我们向计算机传达指令的一种方式。

有许多编程语言可以用来编程，包括 C、Python、Java、R 等等！

我们可以使用 R 来回答有关数据的问题，例如模拟新冠肺炎 (COVID-19) 在邮轮上的传播情况。R 还可以用于将这些问题的答案可视化 (Visualize)。

## 集成开发环境 (IDE)

集成开发环境 (Integrated Development Environment, IDE) 是用于编程的一套预先配置好的工具。

R 有自己的 IDE，称为 RStudio，它专门用于 R 语言编程。

在 RStudio 中，请注意 `>` 符号。这表示 R 控制台 (R console)，我们可以在这里发布命令。

## 创建你的第一个程序 (Creating Your First Program)

你可以通过在 R 控制台中输入 `file.create("hello.R")` 并按下键盘上的回车键来创建你的第一个程序。

注意 `hello.R` 以 `.R` 结尾。你过去可能见过其他带有 `.jpg` 或 `.gif` 后缀的文件。`.R` 是 R 语言使用的特定文件扩展名 (File extension)。

当你发布上述命令时，你应该在 R 控制台中看到 `[1] TRUE`。稍后会详细介绍！

在 R 控制台的右侧，你可以访问文件浏览器 (File explorer)。观察 `hello.R` 是如何在我们当前的工作目录 (Working directory) 中创建的——这是默认情况下保存我们所有文件的地方。

我们可以通过双击 `hello.R` 文件来打开它。

现在会出现文件编辑器 (File editor)，这是一个我们可以编写多行代码的地方。

在文件编辑器中，输入你的第一个程序，如下所示：

```R
print("hello, world")
```

注意这里出现的所有文本和字符。它们都是必不可少的。

你可以通过点击保存图标进行保存。

你可能习惯于通过双击图标来运行程序。在 R 中，我们必须采取不同的方法来运行程序。

R 不仅仅是一种编程语言。它也是一个解释器 (Interpreter)，可以将我们的源代码 (Source code) 转换为计算机能够理解并运行的内容。

我们可以通过点击运行 (Run) 按钮来执行这个过程。观察现在是如何显示 `hello, world` 的。做得好！

## 函数 (Functions)

函数 (Functions) 是我们运行一套指令的一种方式。

在你的代码中，`print` 是一个函数，"hello world" 被传递给它。我们传递给函数的内容称为参数 (Argument)。

该函数的副作用 (Side effect) 是在 R 控制台中显示 `hello, world`。

## 错误/漏洞 (Bugs)

错误 (Bugs) 是在代码中可能出现的无意中的失误。

如下修改你的代码：

```R
# 演示一个错误

prin("hello, world")
```

注意 `prin` 中缺少了字母 `t`。

运行你的代码，你会注意到产生了一个错误。

调试 (Debugging) 是寻找并消除错误的过程。

## readline

在 R 中，`readline` 函数可以读取来自用户的输入 (Input)。

如下修改你的代码：

```R
readline("What's your name? ")
print("Hello, Carter")
```

注意，如果我们运行这段代码，总会显示 `Carter`。

我们需要创建一种方式来读取并使用用户提供的姓名。

函数不仅有参数和副作用，它们还有返回值 (Return values)。返回值是由函数提供的。我们可以将返回值存储为变量 (Variables)。在 R 中，变量也可以被称为对象 (Objects)，以避免与统计变量 (Statistical variables) 混淆——这是一个不同的概念！

如下修改你的代码：

```R
name <- readline("What's your name? ")
print("Hello, name")
```

注意名为 `name` 的变量是如何存储 `readline` 的返回值的。箭头 `<-` 表示返回值正从 `readline` 传递到 `name`。这个箭头被称为赋值操作符 (Assignment operator)。

运行这段代码并打开 IDE 右侧的环境窗口 (Environment window)，你可以看到程序中的变量以及其中存储的内容。

## paste

尽管如此，运行这段代码时，你会注意到始终显示 “name”。这显然是一个错误！

我们可以如下修正这个错误：

```R
name <- readline("What's your name? ")
greeting <- paste("Hello, ", name)
print(greeting)
```

注意第一行代码保持不变。观察我们如何创建一个名为 `greeting` 的新变量，并将 “Hello, ” 和 `name` 的字符串拼接 (String concatenation) 结果赋值给 `greeting`。字符串 (Strings) 是字符的集合。使用 `paste` 函数可以将两个独立的字符串合并为一个。生成的变量 `greeting` 使用 `print` 函数打印出来。

运行这段代码，观察环境中出现的新变量。

如果你观察得特别仔细，这里仍然有一个错误！在 “Hello,” 和 `name` 的值之间，`greeting` 中存储了两个空格。

## 文档 (Documentation)

通过在 R 控制台中输入 `?paste` 可以访问 `paste` 的文档 (Documentation)。相应地，`paste` 的文档将会出现。阅读这份文档，你可以了解在 `paste` 中可以使用的各种参数 (Parameters)。

与我们当前工作相关的一个参数是 `sep`。

如下修改你的代码：

```R
name <- readline("What's your name? ")
greeting <- paste("Hello, ", name, sep = "")
print(greeting)
```

注意代码中添加了 `sep = ""`。

运行这个程序，你会看到输出现在符合预期。

恰好程序员经常需要通过将 `sep` 设置为空字符串 `""` 来省略这些多余的空格。因此，他们发明了 `paste0`，它可以在没有任何分隔符的情况下拼接字符串。`paste0` 可以如下使用：

```R
name <- readline("What's your name? ")
greeting <- paste0("Hello, ", name)
print(greeting)
```

注意 `paste` 变成了 `paste0`。

你的程序可以进一步简化如下：

```R
# 询问用户的姓名
name <- readline("What's your name? ")

# 向用户打招呼
print(paste("Hello,", name))
```

注意如何通过直接将 `paste` 的返回值作为 `print` 的输入值来消除 `greeting` 变量。

最后，当像上面那样在函数中嵌套 (Nesting) 函数时，请考虑你和他人阅读代码时的挑战。有时，过多的嵌套会导致无法理解代码在做什么。这是一个设计决策 (Design decision)。也就是说，你经常会为了用户和程序员的利益而对代码做出决定。

此外，你可能会做出的一个风格决策 (Style decision) 是使用 `#` 符号包含注释 (Comments)，在其中描述一段代码正在做什么。

## 算术 (Arithmetic)

让我们创建一个新程序，为一些虚构角色统计选票。

关闭 `hello.R` 文件。

在控制台中输入 `file.create("count.R")`。

如下编写代码：

```R
mario <- readline("Enter votes for Mario: ")
peach <- readline("Enter votes for Peach: ")
bowser <- readline("Enter votes for Bowser: ")

total <- mario + peach + bowser

print(paste("Total votes:", total))
```

注意 `readline` 的返回值是如何存储在名为 `mario`、`peach` 和 `bowser` 的三个变量中的。变量 `total` 被赋予了 `mario`、`peach` 和 `bowser` 相加的值。然后，打印出总量。

R 有许多算术操作符 (Arithmetic operators)，包括 `+`、`-`、`*`、`/` 等等！

运行这段代码并输入票数，会产生一个错误。

这是因为来自用户的输入被视为字符串 (String) 而不是数字 (Number)。查看环境，注意 `mario` 和其他变量的值是如何被双引号包围的。这些引号表示它们被存储为字符型字符串 (Character strings) 而不是数字。这些值必须是数字才能用 `+` 相加。

在 R 中，变量可以以不同的模式 (Modes，有时也称为“类型” Type！) 存储。其中一些 “存储模式” (Storage modes) 包括字符型 (character)、双精度浮点型 (double) 和整型 (integer)。

我们可以如下将这些变量转换为我们想要的存储模式：

```R
mario <- readline("Enter votes for Mario: ")
peach <- readline("Enter votes for Peach: ")
bowser <- readline("Enter votes for Bowser: ")

mario <- as.integer(mario)
peach <- as.integer(peach)
bowser <- as.integer(bowser)

total <- mario + peach + bowser

print(paste("Total votes:", total))
```

注意如何通过 `as.integer` 采用强制类型转换 (Coercion) 将 `mario` 等变量转换为整数。

运行这段代码并查看环境，你可以看到这些值现在正以不带引号的整数形式存储。

该程序可以进一步简化如下：

```R
mario <- as.integer(readline("Enter votes for Mario: "))
peach <- as.integer(readline("Enter votes for Peach: "))
bowser <- as.integer(readline("Enter votes for Bowser: "))

total <- sum(mario, peach, bowser)

print(paste("Total votes:", total))
```

注意如何使用 `sum` 函数来汇总三个变量的值。

有没有一种方法可以利用预先存在的数据源？

## 表格 (Tables)

表格 (Tables) 是我们可以用来组织数据的多种结构之一。

表格是一组行 (Rows) 和列 (Columns)，其中行通常代表被存储的某个实体，而列代表这些实体的属性。

表格可以以多种文件格式存储。一种常见的格式是逗号分隔值 (Comma-separated values, CSV) 文件。

在 CSV 文件中，每一行存储在单独的一行。列由逗号分隔。

在我们开始下一个程序之前，在 R 控制台中输入 `ls()` 以确定环境中所有活动的变量。然后，输入 `rm(list = ls())` 以从环境中删除所有这些值。再次输入 `ls()`，你会注意到环境中没有剩下的对象了。

接下来，输入 `file.create("tabulate.R")` 来创建我们的新程序文件。打开文件浏览器，打开 `tabulate.R` 文件。此外，你应该从本讲座的源代码中下载 `votes.csv` 文件，并将其拖入你的工作目录。

如下编写代码：

```R
votes <- read.table("votes.csv")
View(votes)
```

注意第一行代码如何将 `votes.csv` 中的表格读入 `votes` 变量中。然后，`View` 允许你查看 `votes` 中存储的内容。

运行这段代码，你现在可以看到一个显示 `votes` 对象中存储内容的单独标签页。但是，出现了一个错误。观察所有数据是如何被读入一个列中的。似乎 `read.table` 正在从 csv 文件中读取数据，但似乎仍需要一些格式设置。

如下修改你的代码：

```R
votes <- read.table(
  "votes.csv",
  sep = ","
)
View(votes)
```

注意如何使用 `sep` 来告诉 `read.table` 每一列是以哪个字符分隔的。

尽管如此，运行这段代码时仍然有一个错误。我们如何让 `read.table` 识别表格的表头 (Header)？

如下修改你的代码：

```R
votes <- read.table(
  "votes.csv",
  sep = ",",
  header = TRUE
)
View(votes)
```

注意 `header = TRUE` 参数如何让 `read.table` 识别出存在表头。

运行此文件，表格将按预期显示。

程序员们创造了一个快捷方式来更简单地完成这项工作。如下修改你的代码：

```R
votes <- read.csv("votes.csv")
View(votes)
```

注意 `read.csv` 如何以比之前的代码大得多的简洁性完成工作！

现在我们的数据已加载，我们该如何访问它？如下修改你的代码：

```R
votes <- read.csv("votes.csv")

votes[, 1]
votes[, 2]
votes[, 3]
```

注意如何使用括号表示法 (Bracket notation) 以 `votes[行, 列]` 的格式访问值。因此，`votes[, 2]` 将显示 `poll` 列中的数字。

## 向量 (Vectors)

向量 (Vectors) 是具有相同存储模式的一组值的列表。

考虑到我们的候选人和选票的数据框 (Data frame)（或表格），我们可以通过创建一个新向量来访问特定的值。

我们可以通过调用每一列的准确名称来简化这个程序：

```R
votes <- read.csv("votes.csv")

colnames(votes)

votes$candidate
votes$poll
votes$mail
```

注意 `votes$poll` 如何返回 `poll` 列中所有值的向量。我们现在可以使用这个新向量访问 `poll` 列的值。

运行这段代码，观察每一列的值是如何出现的。

回到我们最初关于如何汇总这些值的问题，如下修改你的代码：

```R
votes <- read.csv("votes.csv")

sum(votes$poll[1], votes$poll[2], votes$poll[3])
```

注意如何使用 `sum` 来汇总 `poll` 中第一、二、三行的值。

然而，这段代码不是动态的 (Dynamic)。它相当不灵活。如果有超过三个候选人怎么办？因此，我们可以将代码简化如下，使其更具动态性：

```R
votes <- read.csv("votes.csv")

sum(votes$poll)
sum(votes$mail)
```

注意向量 `votes$poll` 和 `votes$mail` 中的值是如何被汇总的。

正如上面使用括号表示法所说明的，我们也可以尝试汇总 `poll` 和 `mail` 列中每一行的值。如下修改你的代码：

```R
votes <- read.csv("votes.csv")

votes$poll[1] + votes$mail[1]
votes$poll[2] + votes$mail[2]
votes$poll[3] + votes$mail[3]
```

注意 `poll` 和 `mail` 的每一行是如何相加的。

不过，这是 R 提供的最佳方法吗？

## 向量算术 (Vector Arithmetic)

很多时候，我们希望能够将一个向量的行与另一个向量的行相加。我们可以通过向量算术 (Vector arithmetic) 来实现这一点。

秉持着让代码更具动态性的精神，我们可以进一步将代码修改如下：

```R
votes <- read.csv("votes.csv")

votes$poll + votes$mail
```

注意向量是如何逐元素地 (Element-wise) 相加的。也就是说，第一个向量的第一行加到第二个向量的第一行，第一个向量的第二行加到第二个向量的第二行，依此类推。这将产生一个与 `poll` 和 `mail` 向量行数相同的新向量。

向量算术会产生一个全新的向量。我们可以用各种方式处理这个新向量。

自然地，我们可能想要存储算术运算的结果。我们可以通过如下修改代码来实现：

```R
votes <- read.csv("votes.csv")

votes$total <- votes$poll + votes$mail

write.csv(votes, "totals.csv")
```

注意最终的总数是如何存储在一个名为 `votes$total` 的新向量中的，它实际上是 `votes` 数据框的一个新总数列。然后我们将生成的 `votes` 数据框写入一个名为 `totals.csv` 的文件中。

当你查看 csv 文件时，会出现一个问题。注意，默认情况下包含了 “行名” (Row names)。可以通过如下修改代码来排除它们：

```R
votes <- read.csv("votes.csv")

votes$total <- votes$poll + votes$mail

write.csv(votes, "totals.csv", row.names = FALSE)
```

注意 `row.names` 被设置为 `FALSE`。

## 外部数据 (External Data)

今天，我们已经看到了许多关于如何使用 R 的例子。

在很多情况下，你可能希望使用别人的数据集 (Dataset)。

你可以按照如下方式访问在线数据源：

```R
# 演示从 URL 读取数据

url <- "https://github.com/fivethirtyeight/data/raw/master/non-voters/nonvoters_data.csv"
voters <- read.csv(url)
```

注意 `read.csv` 是如何从定义的 URL 提取数据的。

查看这个数据框，你可以运行 `nrow` 来获取行数，运行 `ncol` 来获取列数。

```R
# 演示在大型数据集中查找行数和列数

url <- "https://github.com/fivethirtyeight/data/raw/master/non-voters/nonvoters_data.csv"
voters <- read.csv(url)

nrow(voters)
ncol(voters)
```

注意 `nrow` 和 `ncol` 是如何用于确定数据中存在多少行和多少列的。

数据集有时会附带一个代码簿 (Code book)。代码簿是关于数据中包含哪些列的指南。例如，`Q1` 列可能代表研究参与者被问到的一个特定问题。通过查看此数据集的代码簿，我们可以知道有一个名为 `voter_category` 的列，它定义了每个参与者的特定投票行为。

你可能想了解参与者在该列中可以选择的各种选项。这可以通过 `unique` 函数来实现。

```R
# 演示在向量中查找唯一值

url <- "https://github.com/fivethirtyeight/data/raw/master/non-voters/nonvoters_data.csv"
voters <- read.csv(url)

unique(voters$voter_category)
```

注意 `unique` 是如何被用来确定参与者可能选择的可选选项的。

## 特殊值 (Special Values)

对于 `Q22`，我们在代码簿中发现这个问题涉及参与者未注册投票的原因。查看这些数据，我们看到 `NA` 是呈现的值之一。在 R 中，`NA` 代表 “不可用” (Not available)，是一个特殊值。

R 中的其他特殊值 include `Inf`、`-Inf`、`NaN` 和 `NULL`。它们分别表示无穷大 (Infinite)、负无穷大 (Negatively infinite)、非数字 (Not a number) 和空值 (Null 或 None value)。

要查看 `Q22` 的这些可能值，我们可以运行以下代码：

```R
# 演示 NA

url <- "https://github.com/fivethirtyeight/data/raw/master/non-voters/nonvoters_data.csv"
voters <- read.csv(url)

voters$Q22
unique(voters$Q22)
```

注意再次使用 `unique` 来发现 `Q22` 的可能值。

## 因子 (factor)

`Q21` 涉及参与者在未来选举中投票的计划。在这一列中，值 1、2 和 3 与特定的可能答案相对应。例如，1 可能代表 “Yes”。

在 R 中，我们可以使用 `factor` 将数字值转换为特定的文本答案。例如，我们可以使用 `factor` 将数字 1 更改为对应文本 “Yes”。我们可以通过如下修改代码来实现：

```R
# 演示将向量转换为因子

url <- "https://github.com/fivethirtyeight/data/raw/master/non-voters/nonvoters_data.csv"
voters <- read.csv(url)

voters$Q21

factor(
  voters$Q21
)

factor(
  voters$Q21,
  labels = c("?", "Yes", "No", "Unsure/Undecided")
)
```

注意 `factor(voters$Q21)` 如何显示 `Q21` 数据的特定水平 (Levels)（即类别）。在随后出现的因子代码中，标签 (Labels) 被应用于每个水平。例如，1 与 “Yes” 相关联。

在许多情况下，我们可能希望排除某些值。在 `Q21` 中，我们可能希望排除 `-1`，因为不清楚该值代表什么。我们可以如下操作：

```R
# 演示从因子的水平中排除值

url <- "https://github.com/fivethirtyeight/data/raw/master/non-voters/nonvoters_data.csv"
voters <- read.csv(url)

voters$Q21 <- factor(
  voters$Q21,
  labels = c("Yes", "No", "Unsure/Undecided"),
  exclude = c(-1)
)
```

注意 `-1` 是如何被排除的。

## 总结 (Summing Up)

在本课中，你学习了如何在 R 中表示数据。具体来说，你学习了……

* [[#函数 (Functions)]]
* [[#错误/漏洞 (Bugs)]]
* [[#readline]]
* [[#paste]]
* [[#文档 (Documentation)]]
* [[#算术 (Arithmetic)]]
* [[#表格 (Tables)]]
* [[#向量 (Vectors)]]
* [[#向量算术 (Vector Arithmetic)]]
* [[#外部数据 (External Data)]]
* [[#特殊值 (Special Values)]]
* [[#因子 (factor)]]

下次见，届时我们将讨论 [[L2：转换数据 (Transforming Data)|如何转换数据]]。