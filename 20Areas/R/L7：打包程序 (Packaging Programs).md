# 第7讲：打包程序 (Packaging Programs)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#包 (Packages)]]
* [[#包结构 (Package Structure)]]
* [[#devtools]]
* [[#编写测试 (Writing Tests)]]
* [[#编写 R 代码 (Writing R Code)]]
* [[#NAMESPACE]]
* [[#测试代码 (Testing Code)]]
* [[#编写文档 (Writing Documentation)]]
* [[#构建包 (Building Packages)]]
* [[#更新包 (Updating Packages)]]
* [[#使用和分享包 (Using and Sharing Packages)]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

欢迎回到 CS50 的 R 语言编程入门课程！

今天，我们将学习如何打包 (Packaging) 和分发我们的程序。这样，我们就可以与世界分享它们了！

## 包 (Packages)

今天，我们将要构建并打包一个名为 `ducksay` 的程序。

如果你上过我们其他的 CS50 课程，你可能知道一个名为 `cowsay` 的程序。它接受一段文本，并创建一个牛说这段话的图像。我们将秉持同样的精神构建 `ducksay`。

包 (Packages) 是已经编译好的源代码，以便于分发。

## 包结构 (Package Structure)

包应该放在一个与包名同名的文件夹中。

我们可以通过在 R 控制台中输入以下命令来实现：

```R
dir.create("ducksay")
setwd("ducksay")
```

注意这些命令创建了一个名为 `ducksay` 的目录，然后将工作目录设置为 `ducksay`。

在主文件夹内，包通常具有如下结构：

```text
DESCRIPTION
NAMESPACE
man/
R/
tests/
```

`DESCRIPTION` 文件将包含包的描述，包括作者是谁。`NAMESPACE` 文件将包含我们希望向包用户开放的函数列表。`man` 是一个保存包手册（文档）的文件夹。`R` 文件夹包含包的 R 代码。最后，`tests` 文件夹保存了我们希望运行的所有测试，以确保我们的包行为符合预期。

我们可以通过在 R 控制台中输入 `file.create("DESCRIPTION")` 来创建 `DESCRIPTION` 文件。现在我们可以打开此文件并编写如下代码：

```R
# 演示 DESCRIPTION 文件的必需组件

Package: ducksay
Title: Duck Say
Description: Say hello with a duck.
Version: 1.0
Authors@R: person("Carter", "Zenke", email = "carter@cs50.harvard.edu", role = c("aut", "cre", "cph"))
License: MIT + file LICENSE
```

注意包是如何命名和命名的。然后提供了一个描述。包含了作者信息。最后提供了该包所采用的许可证 (License)。你可以在 `DESCRIPTION` 文件文档中了解更多关于这些字段的信息。

正如你在上面的 `DESCRIPTION` 文件中所看到的，我们还需要一个 `LICENSE` 文件。我们可以如下编写代码：

```R
# 演示在许可证模板上进行添加

YEAR: ...
COPYRIGHT HOLDER: ducksay authors
```

用当前年份填写 `...`。注意许可证的年份和版权持有者是如何命名的。

## devtools

一个名为 `devtools` 的包允许我们更快地创建包。

特别地，`devtools` 附带了一些工具，用于为我们的包的测试和 R 代码创建必要的文件夹结构。

假设已经安装了 `devtools`，我们可以通过在 R 控制台中输入 `library(devtools)` 来加载它。

## 编写测试 (Writing Tests)

多亏了 `devtools` 包，我们可以轻松地使用 `testthat` 为我们编写的包开发测试。

然后，我们可以输入 `use_testthat()` 来启用 `testthat` 功能。我们的 `DESCRIPTION` 文件将自动修改如下：

```R
# 演示为了测试目的建议添加的依赖项

Package: ducksay
Title: Duck Say
Description: Say hello with a duck.
Version: 1.0
Authors@R: person("Carter", "Zenke", email = "carter@cs50.harvard.edu", role = c("aut", "cre", "cph"))
License: MIT + file LICENSE
Suggests:
    testthat (>= 3.0.0)
Config/testthat/edition: 3
```

注意该包会建议安装 3.0.0 或更高版本的 `testthat`。这可能会根据你安装的 `testthat` 版本而有所不同。

在我们由 `use_testthat` 创建的 `tests/testthat` 文件夹中，我们可以如下创建我们的第一个测试文件 `test-ducksay.R`：

```R
# 演示描述 `ducksay` 的行为

describe("ducksay()", {
  it("can print to the console with `cat`", {
    expect_output(cat(ducksay()))
  })
  it("can say hello to the world", {
    expect_match(ducksay(), "hello, world")
  })
})
```

注意 `expect_match` 会在 `ducksay` 的输出中查找字符串 “hello, world”。

## 编写 R 代码 (Writing R Code)

继续使用 `devtools`，我们现在可以在 R 控制台中输入：`use_r("ducksay")`。

此命令将创建一个名为 `R` 的文件夹和一个名为 `ducksay.R` 的文件。

现在，是时候在我们要打包的程序中提供一些功能了。这些功能应该与我们编写的测试相匹配。

如下为 `ducksay.R` 编写代码：

```R
# 演示为包定义一个函数

ducksay <- function() {
  paste(
    "hello, world",
    ">(. )__",
    " (____/",
    sep = "\n"
  )
}
```

## NAMESPACE

如前所述，我们需要在一个名为 `NAMESPACE` 的文件中提供关于哪些函数对该包的最终用户可用的信息。

为此，你可以在控制台中输入 `file.create("NAMESPACE")`。然后，如下编辑此文件：

```R
# 演示声明 `ducksay` 对包的最终用户可见

export(ducksay)
```

此文件只是使 `ducksay` 函数对包的最终用户可用。

我们现在可以在 R 控制台中输入 `load_all()`，以加载 `NAMESPACE` 中命名的所有可用函数。

## 测试代码 (Testing Code)

你现在可以运行 `test()` 来测试我们的函数。不应产生任何错误。

此外，在加载了该包的函数后，你现在可以在 RStudio 中使用 `ducksay` 了。

更新我们的测试，让我们测试一下 `ducksay` 中是否出现了一只鸭子：

```R
# 演示检查输出中是否存在鸭子

describe("ducksay()", {
  it("can print to the console with `cat`", {
    expect_output(cat(ducksay()))
  })
  it("can say hello to the world", {
    expect_match(ducksay(), "hello, world")
  })
  it("can say hello with a duck", {
    duck <- paste(
      ">(. )__",
      " (____/",
      sep = "\n"
    )
    expect_match(ducksay(), duck, fixed = TRUE)
  })
})
```

注意这个测试如何查看是否有一只鸭子的图形。此外，请注意讲座中提到的 `fixed = TRUE`，它可以防止测试将鸭子内部的一些字符误解为正则表达式 (Regular expression) 的一部分。目前只需要知道，正则表达式并不是我们想要的！

## 编写文档 (Writing Documentation)

我们现在可以记录如何使用我们的函数。通常，我们可以输入 `?ducksay` 来查看文档。但是，我们还没有创建文档。

文档是用一种称为标记语言 (Markup language) 的语言编写的。标记语言提供了指定文档格式的语法。

你可以通过输入以下命令来编写文档：

```R
dir.create("man")
file.create("man/ducksay.Rd")
```

第一个命令创建了一个名为 `man` 的文件夹。第二个命令创建了我们的文档文件。

如下修改你的文档文件：

```text
# 演示 R 文档文件所需的标记

\name{ducksay}
\alias{ducksay}
\title{Duck Say}
\description{A duck that says hello.}
\usage{
ducksay()
}
\value{
A string representation of a duck saying hello to the world.
}
\examples{
cat(ducksay())
}
```

注意如何提供名称、标题、描述、用法和其他部分。你可以在通过阅读 R 文档文件的文档来了解更多关于这些元素的信息。

现在，是时候结束工作并分享我们的包了。

## 构建包 (Building Packages)

一旦包的内容准备好被捆绑并分发，可以使用以下两个命令之一来启动构建 (Build)：

* `build`
* `R CMD build`

注意 `build` 是一个 `devtools` 函数，可以直接从 R 控制台运行。`R CMD build` 可以从 R 外部的计算机终端运行。

运行 `build` 后，你会看到一个 `.gz` 文件输出到你的工作目录中。

## 更新包 (Updating Packages)

要更新我们的代码，我们可以打开我们的测试文件并如下更新测试：

```R
# 演示确保小鸭重复给定的短语

describe("ducksay()", {
  it("can print to the console with `cat`", {
    expect_output(cat(ducksay()))
  })
  it("can say hello to the world", {
    expect_match(ducksay(), "hello, world")
  })
  it("can say hello with a duck", {
    duck <- paste(
      ">(. )__",
      " (____/",
      sep = "\n"
    )
    expect_match(ducksay(), duck, fixed = TRUE)
  })
  it("can say any given phrase", {
    expect_match(ducksay("quack!"), "quack!")
  })
})
```

注意添加了一个查找 “quack!” 的新测试。

考虑到这个测试，我们现在可以更新源代码，以允许输入任何短语，然后小鸭会说出这个短语：

```R
# 演示接受一个参数进行打印

ducksay <- function(phrase = "hello, world") {
  paste(
    phrase,
    ">(. )__",
    " (____/",
    sep = "\n"
  )
}
```

注意提供了一个默认短语 “hello, world”。如果提供了另一个短语，它将改为说那个短语。

同样地，我们可以如下更新我们的文档文件：

```text
# 演示更新后的标记，包括指定参数

\name{ducksay}
\alias{ducksay}
\title{Duck Say}
\description{A duck that says hello.}
\usage{
ducksay(phrase = "hello, world")
}
\arguments{
\item{phrase}{The phrase for the duck to say.}
}
\value{
A string representation of a duck saying the given phrase.
}
\examples{
cat(ducksay())
cat(ducksay("quack!"))
}
```

注意返回值 (Value) 已更新。此外，参数 (Arguments) 也已更新。在示例中提供了另一个例子。

我们可以再次运行 `build` 以包含我们的修改。
这个包现在可以与他人分享了。

## 使用和分享包 (Using and Sharing Packages)

现在让我们创建一个名为 `greet.R` 的程序来使用这个包。
我们可以通过在 R 控制台中输入 `setwd("..")` 来将工作目录从 `ducksay` 移开。这将把我们的工作目录移动到 `ducksay` 的上一级目录。

接下来，我们可以输入 `file.create("greet.R")` 来创建一个新文件。如下修改此文件：

```R
# 演示使用自定义包

library(ducksay)

name <- readline("What's your name? ")
greeting <- ducksay(paste("hello,", name))
cat(greeting)
```

注意该程序加载了 `ducksay`。然后，代码使用了这个新库。

虽然这在我们的电脑上可行（因为我们在本地开发了这个包），但其他人需要安装这个包。为此，可以使用以下命令之一：

* `install.packages`
* `R CMD INSTALL`

正如在之前的讲座中讨论过的，第一个命令可以直接在 RStudio 中运行，并内置在 R 本身中。另一个命令可以在计算机终端运行，它也内置在 R 中。

要安装我们的包，我们可以在控制台中运行：`install.packages("ducksay_1.0.tar.gz")`
你可以使用 CRAN、GitHub 甚至电子邮件来分享你的代码。

## 总结 (Summing Up)

在本课中，你学习了如何在 R 中打包你的程序。具体来说，你了解了：

* [[#包 (Packages)]]
* [[#包结构 (Package Structure)]]
* [[#devtools]]
* [[#编写测试 (Writing Tests)]]
* [[#编写 R 代码 (Writing R Code)]]
* [[#NAMESPACE]]
* [[#测试代码 (Testing Code)]]
* [[#编写文档 (Writing Documentation)]]
* [[#构建包 (Building Packages)]]
* [[#更新包 (Updating Packages)]]
* [[#使用和分享包 (Using and Sharing Packages)]]

在本课程中，你学到了许多关于 R 以及使用 R 编程的知识。你学习了如何表示数据、转换数据、应用函数、清理数据、可视化数据、测试程序和打包程序。总之，我们希望你发现这些材料对你有所帮助。我们也希望你能利用所学知识在世界上做出伟大的贡献。

这就是 CS50 的 R 语言编程入门。

---
[[00：目录 (Table of Contents)|返回课程目录]]