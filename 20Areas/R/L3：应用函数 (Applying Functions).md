# 第3讲：应用函数 (Applying Functions)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#定义函数 (Defining Functions)]]
* [[#作用域 (Scope)]]
* [[#检查输入 (Checking Input)]]
* [[#循环 (Loops)]]
* [[#使用循环 (Using Loops)]]
* [[#使用函数和循环 (Using Functions and Loops)]]
* [[#应用函数 (Applying Functions)]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

欢迎回到 CS50 的 R 语言编程入门课程！

今天，我们将学习应用函数。我们还将学习如何编写我们自己的函数以及如何应用循环。

回想一下我们在上一讲中创建的一个名为 `count.R` 的程序。

```R
# 演示为 3 个不同的候选人统计选票

mario <- as.integer(readline("Mario: "))
peach <- as.integer(readline("Peach: "))
bowser <- as.integer(readline("Bowser: "))

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意这些行是如何重复获取用户输入的。

在编程中，任何时候重复使用代码都被视为改进的机会。函数 (Functions) 是我们减少这些冗余的一种方式，通过定义可以在整个程序中重复使用的特定代码块。

## 定义函数 (Defining Functions)

在 R 中，函数由语法 `function()` 定义。

考虑我们程序的以下改进版本：

```R
# 演示定义一个函数

get_votes <- function() {
  votes <- as.integer(readline("Enter votes: "))
  return(votes)
}

mario <- get_votes()
peach <- get_votes()
bowser <- get_votes()

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意创建了一个名为 `get_votes` 的新函数。函数体由大括号（`{` 和 `}`）表示。注意在函数体内有两行代码，每次调用该函数时都会运行。首先，从用户那里收集选票；其次，返回选票。`mario`、`peach` 和 `bowser` 在调用 `get_votes` 后分别接收其返回值。最后，提供总和并显示给用户。

恭喜你，这是你在 R 中的第一个函数！

然而，运行这个函数后，我们发现该函数丢失了我们之前拥有的一些功能。有没有一种方法可以为函数提供一个参数 (Parameter)，以便我们可以更准确地提示用户？确实可以！考虑以下内容：

```R
# 演示定义参数

get_votes <- function(prompt) {
  votes <- as.integer(readline(prompt))
}

mario <- get_votes("Mario: ")
peach <- get_votes("Peach: ")
bowser <- get_votes("Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意为 `get_votes` 函数提供了一个提示信息 (Prompt)。因此，用户会看到他们正在为谁投票的姓名提示。此外，请注意 `return(votes)` 语句已被删除。在 R 中，函数会自动返回最后计算出的值。

带有参数的函数可以分配默认值 (Default values)。考虑我们程序的以下更新：

```R
# 演示定义带有默认值的参数

get_votes <- function(prompt = "Enter votes: ") {
  votes <- as.integer(readline(prompt))
}

mario <- get_votes()
peach <- get_votes()
bowser <- get_votes()

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意第一行代码中是如何提供默认值的。

我们仍然可以按如下方式覆盖默认提示：

```R
# 演示精确参数匹配

get_votes <- function(prompt = "Enter votes: ") {
  votes <- as.integer(readline(prompt))
}

mario <- get_votes(prompt = "Mario: ")
peach <- get_votes(prompt = "Peach: ")
bowser <- get_votes(prompt = "Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意对于每次函数调用，给定的参数如何覆盖默认参数。

## 作用域 (Scope)

观察 RStudio 中的环境面板 (Environment pane)，注意显示了 `bowser` 等变量的值。然而，并没有出现 `votes` 的值。这是为什么呢？

事实证明，所有对象都定义在特定的“环境” (Environments) 中。其中一个环境是“全局” (Global) 环境。全局环境是你定义在 R 控制台中或函数体之外的对象（如 `mario`、`bowser` 和 `peach`）的所在地。默认情况下，RStudio 的环境面板显示全局环境中定义的对象。

`get_votes` 函数本身也是一个定义在全局环境中的对象。然而，独特之处在于 `get_votes` 本身也是一种环境！正如你所看到的，在 `get_votes` 的定义中，你可以定义其他对象，如 `votes` 和 `prompt`。

`get_votes` 的环境不是全局环境。在编写操作全局环境的代码时，无法访问该环境中的对象。对象可用的环境被称为它的“作用域” (Scope)。

## 检查输入 (Checking Input)

程序员始终面临的挑战之一是用户的不良行为。也就是说，作为程序员，我们应该预料到用户并不总是按照我们的意愿行事。例如，如果用户提供的是一段文本字符串而不是数字选票呢？

我们可以改进我们的程序来捕获输入的错误值：

```R
# 演示预判无效输入

get_votes <- function(prompt = "Enter votes: ") {
  votes <- as.integer(readline(prompt))
  if (is.na(votes)) {
    return(0)
  } else {
    return(votes)
  }
}

mario <- get_votes("Mario: ")
peach <- get_votes("Peach: ")
bowser <- get_votes("Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意如果 `votes` 的值为 `NA`，`get_votes` 将返回 0。否则，`get_votes` 将返回用户提供的值。

虽然这个程序可以运行，但它仍然会提供警告 (Warnings)，而我们可能不希望用户看到这些警告。我们可以按如下方式抑制警告：

```R
# 演示预判无效输入

get_votes <- function(prompt = "Enter votes: ") {
  votes <- suppressWarnings(as.integer(readline(prompt)))
  if (is.na(votes)) {
    return(0)
  } else {
    return(votes)
  }
}

mario <- get_votes("Mario: ")
peach <- get_votes("Peach: ")
bowser <- get_votes("Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意运行此代码时警告如何被抑制。

该程序可以通过使用 `ifelse` 进一步改进。考虑以下内容：

```R
# 演示将 ifelse 作为最后评估的表达式

get_votes <- function(prompt = "Enter votes: ") {
  votes <- as.integer(readline(prompt))
  ifelse(is.na(votes), 0, votes)
}

mario <- get_votes("Mario: ")
peach <- get_votes("Peach: ")
bowser <- get_votes("Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意 `ifelse` 的第一个值是要测试的逻辑表达式。第二个值 0 是如果第一个值 `is.na(votes)` 的计算结果为 `TRUE` 时将返回的内容。最后，第三个值 `votes` 是如果第一个值的计算结果为 `FALSE` 时提供的内容。

我们现在发现了检查用户输入的第一种基本方法。

正如我们之前所做的那样，我们可以抑制警告：

```R
# 演示 suppressWarnings

get_votes <- function(prompt = "Enter votes: ") {
  votes <- suppressWarnings(as.integer(readline(prompt)))
  ifelse(is.na(votes), 0, votes)
}

mario <- get_votes("Mario: ")
peach <- get_votes("Peach: ")
bowser <- get_votes("Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意警告如何被抑制。

## 循环 (Loops)

我们可能希望对程序进行的重大改进之一是：当用户出错时，能够反复提示用户。为了学习更多关于循环的知识，让我们邀请 CS50 小鸭调试器 (Duck Debugger) 来帮忙！嘎嘎！

考虑以下代码：

```R
# 演示小鸭嘎嘎叫 3 次

cat("quack!\n")
cat("quack!\n")
cat("quack!\n")
```

注意这段代码将输出三次 quack。然而，这非常低效！我们重复了同一行代码三次。

我们可以尝试使用 `repeat` 循环改进这段代码如下：

```R
# 演示小鸭在无限循环中嘎嘎叫

repeat {
  cat("quack!\n")
}
```

注意我们的小鸭叫了多次，但它是无限循环的。小鸭会非常累的！

我们可以实现循环的一种方式是利用 `break` 和 `next`。这种循环将使用计数器重复一定的次数。

```R
# 演示使用 repeat 叫 3 次

i <- 3
repeat {
  cat("quack!\n")
  i <- i - 1
  if (i == 0) {
    break
  } else {
    next
  }
}
```

注意 `i` 的值被设置为 3。然后每次叫声发生时，`i` 都会减少 1。当达到 0 时，循环将中断 (Break)。否则（`else`），此循环将继续 (Next)。

最后，`next` 并不是必需的。如果没有 `next` 语句，循环也会自动继续。我们可以删除这个语句如下：

```R
# 演示移除多余的 next 关键字

i <- 3
repeat {
  cat("quack!\n")
  i <- i - 1
  if (i == 0) {
    break
  }
}
```

注意当 `i` 等于 0 时循环将中断。虽然删除了 `next`，循环仍然可以运行。

我们可以使用的另一种循环类型称为 `while` 循环。只要满足某个条件，这种循环就会继续。考虑以下代码：

```R
# 演示 while 循环，向下计数

i <- 3
while (i != 0) {
  cat("quack!\n")
  i <- i - 1
}
```

注意只要 `i != 0` 这个条件为真，循环就会运行。

另一种循环类型称为 `for` 循环，它允许我们基于一个列表或向量进行重复：

```R
# 演示 for 循环

for (i in c(1, 2, 3)) {
  cat("quack!\n")
}
```

注意 `for` 循环如何将 `i` 的值从 1 开始并运行其内部的代码。然后，它将 `i` 的值设置为 2 并运行。最后，它将 `i` 设置为 3 并运行。因此，循环内部的代码运行了三次。

我们可以通过使用范围 `1:3`（一到三）来简化我们的代码：

```R
# 演示带有语法糖的 for 循环

for (i in 1:3) {
  cat("quack!\n")
}
```

注意代码 `i in 1:3` 达到了与之前示例中代码相同的任务。

## 使用循环 (Using Loops)

我们可以在为 Mario 及其朋友统计选票时使用新学到的循环能力。考虑以下利用 `repeat` 循环的代码：

```R
# 演示重新提示用户输入有效值

get_votes <- function(prompt = "Enter votes: ") {
  repeat {
    votes <- suppressWarnings(as.integer(readline(prompt)))
    if (!is.na(votes)) {
      break
    }
  }
  return(votes)
}

mario <- get_votes("Mario: ")
peach <- get_votes("Peach: ")
bowser <- get_votes("Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意用户将被重新提示，直到提供的值不是 `NA`。

我们可以进一步改进代码如下：

```R
# 演示精简 return

get_votes <- function(prompt = "Enter votes: ") {
  repeat {
    votes <- suppressWarnings(as.integer(readline(prompt)))
    if (!is.na(votes)) {
      return(votes)
    }
  }
}

mario <- get_votes("Mario: ")
peach <- get_votes("Peach: ")
bowser <- get_votes("Bowser: ")

total <- sum(mario, peach, bowser)
cat("Total votes:", total)
```

注意 `return(votes)` 子句是如何代替 `break` 的。该函数保持了相同的功能，但代码更简洁。

现在，利用我们对 `for` 循环的知识，我们可以改进为 Mario 及其朋友重复的代码：

```R
# 演示在循环中提示输入

get_votes <- function(prompt = "Enter votes: ") {
  repeat {
    votes <- suppressWarnings(as.integer(readline(prompt)))
    if (!is.na(votes)) {
      return(votes)
    }
  }
}

for (name in c("Mario", "Peach", "Bowser")) {
  votes <- get_votes(paste0(name, ": "))
}
```

注意这里不再使用三行独立的代码来提示用户为每个候选人投票，而是通过 `for` 循环遍历 “Mario”、“Peach” 和 “Bowser” 来获取选票。`paste0` 语句为每个提示添加了 `:` 字符。

作为最后的修饰，我们可以采用循环在进行过程中累计选票：

```R
# 演示在循环中提示输入并累计票数

get_votes <- function(prompt = "Enter votes: ") {
  repeat {
    votes <- suppressWarnings(as.integer(readline(prompt)))
    if (!is.na(votes)) {
      return(votes)
    }
  }
}

total <- 0
for (name in c("Mario", "Peach", "Bowser")) {
  votes <- get_votes(paste0(name, ": "))
  total <- total + votes
}

cat("Total votes:", total)
```

注意总票数是如何在 `for` 循环的每次迭代中更新的。

回想上述内容，你可以看到循环作为一名程序员为你提供的基本编程能力。

## 使用函数和循环 (Using Functions and Loops)

让我们回到之前讲座讨论过的一个案例，在如下表格中汇总候选人的选票。

现在让我们使用我们在循环和函数方面的新能力来创建一个更好的程序。

也许我们的第一个目标应该是汇总选票。考虑以下代码：

```R
# 演示以过程化方式汇总每位候选人的选票

votes <- read.csv("votes.csv")

total_votes <- c()
for (candidate in rownames(votes)) {
  total_votes[candidate] <- sum(votes[candidate, ])
}
total_votes
```

注意这个 `for` 循环如何遍历 `votes` 数据框中出现的每个候选人。然后，该候选人的选票总和将存储在 `total_votes` 向量中。`total_votes <- c()` 代表一个空向量，稍后将填充数据。`total_votes[candidate]` 在向量 `total_votes` 中创建一个新元素，循环中的每个候选人都有一个对应的元素。

第二个目标可能是汇总每个候选人通过不同方式获得选票的情况。

```R
# 演示以过程化方式汇总每种投票方式的票数

votes <- read.csv("votes.csv")

total_votes <- c()
for (method in colnames(votes)) {
  total_votes[method] <- sum(votes[, method])
}
total_votes
```

注意这个 `for` 循环如何遍历 `colnames`（或列名）中的每种方式。

## 应用函数 (Applying Functions)

上述程序可以使用一系列被称为应用 (apply) 函数的函数进一步优化。应用函数允许你在数据结构的各个元素上应用（即运行）一个函数。例如，`apply` 函数可以在数据表的所有行或列上应用一个函数。

在 `votes` 表的情况下，我们可以按如下方式使用 `apply` 来获取所有行的总和：

```R
# 演示使用 apply 汇总每位候选人的选票

votes <- read.csv("votes.csv")
total_votes <- apply(votes, MARGIN = 1, FUN = sum)
total_votes
```

注意通过使用 `MARGIN = 1` 将 `sum` 函数应用于所有行。如果我们设置 `MARGIN = 2`，`sum` 函数将应用于所有列。

我们可以如下汇总每一列：

```R
# 演示使用 apply 汇总每种投票方式的票数

votes <- read.csv("votes.csv")
total_votes <- apply(votes, MARGIN = 2, FUN = sum)
total_votes
```

注意此时 `MARGIN = 2`。

## 总结 (Summing Up)

在本课中，你学习了如何在 R 中应用函数。具体来说，你学习了……

* [[#定义函数 (Defining Functions)]]
* [[#作用域 (Scope)]]
* [[#检查输入 (Checking Input)]]
* [[#循环 (Loops)]]
* [[#使用循环 (Using Loops)]]
* [[#使用函数和循环 (Using Functions and Loops)]]
* [[#应用函数 (Applying Functions)]]

下次见，届时我们将讨论 [[L4：整理数据 (Tidying Data)|如何整理数据]]。