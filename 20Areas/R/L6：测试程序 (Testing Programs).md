# 第6讲：测试程序 (Testing Programs)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#异常 (Exceptions)]]
* [[#message]]
* [[#warning]]
* [[#stop]]
* [[#单元测试 (Unit Tests)]]
* [[#testthat]]
* [[#测试浮点数值 (Testing Floating-Point Values)]]
* [[#容差 (Tolerance)]]
* [[#测试驱动开发 (Test-Driven Development)]]
* [[#行为驱动开发 (Behavior-Driven Development)]]
* [[#测试覆盖率 (Test Coverage)]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

欢迎回到 CS50 的 R 语言编程入门课程！

今天，我们将学习如何测试程序。我们将了解程序可能会出现什么问题、当问题发生时我们该如何处理，以及如何有条不紊地测试我们的程序以确保它们的行为符合我们的预期！

## 异常 (Exceptions)

考虑以下计算平均值的程序：

```R
# 定义一个计算向量中平均值的函数

average <- function(x) {
  sum(x) / length(x)
}
```

注意该程序如何尝试将一个数字向量作为输入并输出平均值。

你可以想象，你的用户可能会不小心传递字符而不是数字，这会导致我们的 `average` 函数输出一个错误。

这些错误被称为异常 (Exceptions)。有没有一种方法可以让我们检查潜在的此类异常？考虑以下对 `average` 的更新：

```R
# 处理非数值输入

average <- function(x) {
  if (!is.numeric(x)) {
    return(NA)
  }
  sum(x) / length(x)
}
```

注意条件语句（一个 `if` 语句）如何检查向量 `x` 是否不全是数字。按照 R 语言世界的惯例，在这种情况下返回一个值 `NA` 是合适的。

## message

虽然这可以让我们的程序静默运行，但我们可能希望让用户知道发生了一个异常。提醒用户的一种方式是通过 `message` 函数：

```R
# 关于返回 NA 的消息提示

average <- function(x) {
  if (!is.numeric(x)) {
    message("`x` must be a numeric vector. Returning NA instead.")
    return(NA)
  }
  sum(x) / length(x)
}
```

注意如何向用户发送一条关于程序为何返回 `NA` 的消息。

传统上，`message` 旨在用于事情尚未出错时：`message` 纯粹是为了提供信息。因此，我们可以通过警告来提升这些信息的重要性。

## warning

我们可以如下将消息的重要性提升为警告 (Warning)：

```R
# 关于返回 NA 的警告

average <- function(x) {
  if (!is.numeric(x)) {
    warning("`x` must be a numeric vector. Returning NA instead.")
    return(NA)
  }
  sum(x) / length(x)
}
```

注意现在的输出是一条警告消息。

警告不会完全停止程序，但它会让程序员知道有些地方出错了。

## stop

你可以想象一些情景，你不仅仅想警告用户，还想完全停止函数。考虑以下内容：

```R
# 停止而不是警告

average <- function(x) {
  if (!is.numeric(x)) {
    stop("`x` must be a numeric vector.")
  }
  sum(x) / length(x)
}
```

注意 `stop` 如何告诉用户，鉴于他们提供给我们的输入，我们无法继续执行。

也可以将两种可能性结合起来。例如，以下代码既考虑了 `x` 包含非数值元素的情况，也兼顾了存在 `NA` 值的情况：

```R
# 处理 NA 值

average <- function(x) {
  if (!is.numeric(x)) {
    stop("`x` must be a numeric vector.")
  }
  if (any(is.na(x))) {
    warning("`x` contains one or more NA values.")
    return(NA)
  }
  sum(x) / length(x)
}
```

注意这里提供了两个 `if` 语句。

## 单元测试 (Unit Tests)

单元测试 (Unit tests) 用于测试我们的函数和程序。

考虑在单独的文件中为 `average` 编写的以下测试函数：

```R
# 编写测试函数

source("average6.R")

test_average <- function() {
  if (average(c(1, 2, 3)) == 2) {
    cat("`average` passed test :)\n")
  } else {
    cat("`average` failed test :(\n")
  }
}

test_average()
```

注意该函数提供了一个测试用例，其中将数字 1、2 和 3 提供给 `average` 函数。然后提供了一些反馈。注意在第一行中，`source` 确保此测试文件可以访问 `average` 函数。

测试负数也是明智之举：

```R
# 增加测试用例

source("average6.R")

test_average <- function() {
  if (average(c(1, 2, 3)) == 2) {
    cat("`average` passed test :)\n")
  } else {
    cat("`average` failed test :(\n")
  }
    
  if (average(c(-1, -2, -3)) == -2) {
    cat("`average` passed test :)\n")
  } else {
    cat("`average` failed test :(\n")
  }
    
  if (average(c(-1, 0, 1)) == 0) {
    cat("`average` passed test :)\n")
  } else {
    cat("`average` failed test :(\n")
  }
}

test_average()
```

注意这里为正数、负数和零提供了额外的测试。

我们已经编写了 21 行代码！值得庆幸的是，程序员们已经创建了各种可以用来测试我们代码的测试包 (Packages) 或库 (Libraries)。

## testthat

`testthat` 是一个用于测试 R 代码的包。可以通过在控制台中输入 `library(testthat)` 来加载它。

`testthat` 包含一个名为 `test_that` 的函数，可以用来测试我们的函数：

```R
# 测试关于 NA 值的警告

source("average6.R")

test_that("`average` calculates mean", {
  expect_equal(average(c(1, 2, 3)), 2)
  expect_equal(average(c(-1, -2, -3)), -2)
  expect_equal(average(c(-1, 0, 1)), 0)
  expect_equal(average(c(-2, -1, 1, 2)), 0)
})

test_that("`average` warns about NAs in input", {
  expect_warning(average(c(1, NA, 3)))
  expect_warning(average(c(NA, NA, NA)))
})
```

注意多亏了 `expect_equal`，可以告知 `test_that` 函数期望各种数字的平均值等于某个特定值。同样，我们可以向 `test_that` 函数提供指令，使其在平均值计算包含 `NA` 值时 `expect_warning`（期望产生警告）。此外，注意测试是如何被分为不同部分的：一部分测试均值的计算，而另一部分测试警告。

运行上述测试，我们发现 `average` 函数中 `if` 语句的顺序可能需要调整：

```R
# 修正错误处理的顺序

average <- function(x) {
  if (any(is.na(x))) {
    warning("`x` contains one or more NA values.")
    return(NA)
  }
  if (!is.numeric(x)) {
    stop("`x` must be a numeric vector.")
  }
  sum(x) / length(x)
}
```

注意条件语句的顺序是如何改变的。

我们仍然应该测试当输入中给定 `NA` 值时 `average` 会返回 `NA`，而不只是测试 `average` 会产生警告！

```R
# 测试 NA 返回值

source("average7.R")

test_that("`average` calculates mean", {
  expect_equal(average(c(1, 2, 3)), 2)
  expect_equal(average(c(-1, -2, -3)), -2)
  expect_equal(average(c(-1, 0, 1)), 0)
  expect_equal(average(c(-2, -1, 1, 2)), 0)
})

test_that("`average` returns NA with NAs in input", {
  expect_equal(suppressWarnings(average(c(1, NA, 3))), NA)
  expect_equal(suppressWarnings(average(c(NA, NA, NA))), NA)
})

test_that("`average` warns about NAs in input", {
  expect_warning(average(c(1, NA, 3)))
  expect_warning(average(c(NA, NA, NA)))
})
```

注意我们有两个独立的测试将 `NA` 值作为输入传递给 `average`。一个测试正确的返回值，而另一个测试是否产生了警告。

`test_that` 还有其他可以协助我们进行测试的函数，包括 `expect_error` 和 `expect_no_error`。

使用 `expect_error`，我们可以如下修改代码：

```R
# 测试如果参数是非数值型则停止运行

source("average7.R")

test_that("`average` calculates mean", {
  expect_equal(average(c(1, 2, 3)), 2)
  expect_equal(average(c(-1, -2, -3)), -2)
  expect_equal(average(c(-1, 0, 1)), 0)
  expect_equal(average(c(-2, -1, 1, 2)), 0)
})

test_that("`average` returns NA with NAs in input", {
  expect_equal(suppressWarnings(average(c(1, NA, 3))), NA)
  expect_equal(suppressWarnings(average(c(NA, NA, NA))), NA)
})

test_that("`average` warns about NAs in input", {
  expect_warning(average(c(1, NA, 3)))
  expect_warning(average(c(NA, NA, NA)))
})

test_that("`average` stops if `x` is non-numeric", {
  expect_error(average(c("quack!")))
  expect_error(average(c("1", "2", "3")))
})
```

注意这段代码在输入为 “quack!” 或提供字符而不是数字时，期望产生一个错误。

## 测试浮点数值 (Testing Floating-Point Values)

我们可能希望将浮点数值（即小数位数值）作为 `average` 的输入：

```R
# 测试双精度浮点型 (doubles)

source("average7.R")

test_that("`average` calculates mean", {
  expect_equal(average(c(1, 2, 3)), 2)
  expect_equal(average(c(-1, -2, -3)), -2)
  expect_equal(average(c(-1, 0, 1)), 0)
  expect_equal(average(c(-2, -1, 1, 2)), 0)
  expect_equal(average(c(0.1, 0.5)), 0.3)
})

test_that("`average` returns NA with NAs in input", {
  expect_equal(suppressWarnings(average(c(1, NA, 3))), NA)
  expect_equal(suppressWarnings(average(c(NA, NA, NA))), NA)
})

test_that("`average` warns about NAs in input", {
  expect_warning(average(c(1, NA, 3)))
  expect_warning(average(c(NA, NA, NA)))
})

test_that("`average` stops if `x` is non-numeric", {
  expect_error(average(c("quack!")))
  expect_error(average(c("1", "2", "3")))
})
```

注意在第一组测试的最后添加了对浮点数值的测试。

## 容差 (Tolerance)

浮点数值是独特的，因为它们受浮点数不精确性 (Floating-point imprecision) 的影响。

让我们通过一个例子来理解浮点数的不精确性：

```R
# 演示浮点数不精确性

print(0.3)
print(0.3, digits = 17)
```

注意我们可以看到在 R 中 0.3 并没有被表示为精确的 0.3。这是编程语言中的普遍现象，因为存在无限数量的浮点值，而用于表示它们的位数 (Bits) 是有限的。

由于浮点数的不精确性，涉及浮点数值的等值测试需要允许一定的容差 (Tolerance)。容差指的是高于或低于预期值的一个数值范围，为了测试的目的，该范围内的值将被视为与预期值相等。容差通常以绝对项指定，例如 ± 0.000001。

`expect_equal` 函数已经提供了一个通常适用于大多数用例的容差水平。这个默认值可以通过 `tolerance` 参数来更改。

你和你的团队应该决定计算中期望的精度水平。

## 测试驱动开发 (Test-Driven Development)

一种开发哲学被称为测试驱动开发 (Test-driven development, TDD)。这种心态认为，在编写要测试的源代码之前先创建测试是最好的。考虑以下测试：

```R
# 测试 greet

source("greet1.R")

test_that("`greet` says hello to a user", {
  expect_equal(greet("Carter"), "hello, Carter")
})
```

注意你可以想象一个 `greet` 函数应该向作为输入提供的用户打招呼。

通过查看测试，我们可以创建响应测试的代码：

```R
# 向用户打招呼

greet <- function(to) {
  return(paste("hello,", to))
}
```

注意这段代码如何通过姓名向用户问好。

在测试驱动开发中，编写测试让程序员知道他们应该实现哪些功能。好处是这些功能随后可以立即进行测试。进一步的修改应该始终通过已经编写好的测试。

## 行为驱动开发 (Behavior-Driven Development)

行为驱动开发 (Behavior-driven development, BDD) 在精神上与测试驱动开发相似，但更注重函数在上下文中的行为。在行为驱动开发中，人们可能会通过明确命名函数应该做什么来描述我们希望函数完成的任务。

`testthat` 附带了两个实现行为驱动开发的函数，`describe` 和 `it`：

```R
# 描述 greet

source("greet2.R")

describe("greet()", {
  it("can say hello to a user", {
    name <- "Carter"
    expect_equal(greet(name), "hello, Carter")
  })
  it("can say hello to the world", {
    expect_equal(greet(), "hello, world")
  })
})
```

注意 `describe` 包含了关于它（该函数！）应该能够做什么的多个基于代码的描述。

## 测试覆盖率 (Test Coverage)

当你去为你的代码编写测试时，请考虑这些测试的全面程度。定义代码完成哪些任务是至关重要的，并创建体现这些关键任务的测试。

## 总结 (Summing Up)

在本课中，你学习了如何在 R 中测试程序。具体来说，你学习了：

* [[#异常 (Exceptions)]]
* [[#message]]
* [[#warning]]
* [[#stop]]
* [[#单元测试 (Unit Tests)]]
* [[#testthat]]
* [[#测试浮点数值 (Testing Floating-Point Values)]]
* [[#容差 (Tolerance)]]
* [[#测试驱动开发 (Test-Driven Development)]]
* [[#行为驱动开发 (Behavior-Driven Development)]]
* [[#测试覆盖率 (Test Coverage)]]

下次见，届时我们可以讨论 [[L7：打包程序 (Packaging Programs)|如何打包我们的代码并与世界分享]]。