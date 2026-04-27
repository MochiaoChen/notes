# 第4讲：整理数据 (Tidying Data)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#dplyr]]
* [[#select]]
* [[#filter]]
* [[#管道操作符 (Pipe Operator)]]
* [[#arrange]]
* [[#distinct]]
* [[#写入数据 (Writing Data)]]
* [[#group_by]]
* [[#summarize]]
* [[#ungroup]]
* [[#tidyr]]
* [[#整洁数据 (Tidy Data)]]
* [[#规范化 (Normalizing)]]
* [[#旋转 (Pivoting)]]
* [[#stringr]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

欢迎回到 CS50 的 R 语言编程入门课程！

今天，我们将学习如何清理数据 (Tidying data)。事实上，你可以想象很多时候表格和数据可能并不是你所希望的形状！

包 (Packages) 是由开发者创建的代码片段，我们可以安装并加载到我们的 R 程序中。这些包可以提供 R 原生不具备的功能。

包存储在 R 的库 (Library) 中。因此，你可以使用 `library` 函数加载包。

## dplyr

`dplyr` 是 `tidyverse` 中的一个包，包含了用于操作数据的函数。

`dplyr` 包含了一个名为 `storms` 的数据集，其中包含了来自美国国家海洋和大气管理局 (NOAA) 的风暴观测数据。

加载 `dplyr` 或 `tidyverse` 后，只需在 R 控制台中输入 `storms` 即可加载数据集。

输入 `storms` 后，请注意显示的是一个 `tibble`。`tibble` 是 `tidyverse` 对 R 数据框 (Data frame) 的“重塑”。注意行、行号以及各种列是如何包含并标注的。此外，注意 `tibble` 中使用的文本颜色。

## select

让我们在数据集中找出最强的风暴。首先，让我们删除不需要的列。考虑以下程序：

```R
# 删除选定的列

dplyr::select(
  storms,
  !c(lat, long, pressure, tropicalstorm_force_diameter, hurricane_force_diameter)
)
```

注意 `dplyr` 中的 `select` 函数如何允许人们确定数据框或 `tibble` 中将包含哪些列。`select` 的第一个参数是要操作的数据框（或 `tibble`）：`storms`。`select` 的第二个参数是要选择的列向量。然而，在这种情况下，使用了 `!`：`!` 表示随后的列名将被排除。另外，`-` 具有相同的功能。运行此代码将通过删除上述列来简化 `tibble`。

输入所有这些列名有点麻烦！

辅助函数如 `contains`、`starts_with` 或 `ends_with` 可以提供帮助。考虑以下代码：

```R
# 引入 ends_with

select(
  storms,
  !c(lat, long, pressure, ends_with("diameter"))
)
```

注意如何使用 `ends_with` 来排除所有以 `diameter` 结尾的列。使用了更少的代码，但结果与之前相同。

## filter

另一个有用的函数是 `filter`，它可以用于从数据框中过滤行。

考虑以下代码：

```R
# 仅查找有关飓风 (hurricanes) 的行

filter(
  select(
    storms,
    !c(lat, long, pressure, ends_with("diameter"))
  ),
  status == "hurricane"
)
```

注意只有在 `status` 列中包含 `hurricane` 的行才被包含在内。

注意最新的示例中已经删除了第一个示例中的 `dplyr::` 语法。事实证明，除非两个或多个包定义了同名函数，否则你不需要指出定义函数的特定包。在这种情况下，你需要通过指定要使用哪个包的函数来消除歧义 (Ambiguity)。

## 管道操作符 (Pipe Operator)

在 R 中，管道操作符 (Pipe operator) 由 `|>` 表示，它允许人们将数据“传输” (Pipe) 到特定的函数中。例如，考虑以下代码：

```R
# 引入管道操作符

storms |>
  select(!c(lat, long, pressure, ends_with("diameter"))) |>
  filter(status == "hurricane")
```

注意 `storms` 是如何传输给 `select` 的，隐含地成为了 `select` 的第一个参数。然后，注意 `select` 的返回值是如何传输给 `filter` 的，隐含地成为了 `filter` 的第一个参数。当你使用管道操作符时，可以避免嵌套函数调用，并使代码编写更具顺序性。

## arrange

现在让我们使用 `arrange` 函数对我们的行进行排序：

```R
# 仅查找有关飓风的行，并按最高风速降序排列

storms |>
  select(!c(lat, long, pressure, ends_with("force_diameter"))) |>
  filter(status == "hurricane") |>
  arrange(desc(wind))
```

注意 `select` 函数的返回值是如何传输给 `filter` 的，其返回值随后又传输给 `arrange`。结果数据框中的行按 `wind` 列的值降序排列。

## distinct

你可能会注意到这个 `tibble` 包含了许多关于同一场风暴的行。因为这些数据包含了对同一场风暴的多次观测，所以这并不奇怪。然而，如果能只找到独特的 (Distinct) 风暴，岂不是更好？

`distinct` 函数允许人们获取 `tibble` 中的唯一项。

`distinct` 返回唯一的行，它会查找重复行并返回重复集中的第一行。

默认情况下，`distinct` 仅在行中的所有值都与另一行中的所有值匹配时才认为行是重复的。

然而，你可以告诉 `distinct` 在确定行是否重复时要考虑哪些值。考虑以下利用此能力的代码：

```R
# 仅保留每场飓风的第一条观测记录

storms |>
  select(!c(lat, long, pressure, ends_with("force_diameter"))) |>
  filter(status == "hurricane") |>
  arrange(desc(wind), name) |>
  distinct(name, year, .keep_all = TRUE)
```

注意 `distinct` 被告知仅查看每场风暴的 `name` 和 `year` 以确定它是否是一个唯一项。`.keep_all = TRUE` 告诉 `distinct` 仍然返回每行的所有列。

## 写入数据 (Writing Data)

我们可以将数据保存为 CSV 文件以便以后使用。

考虑以下代码：

```R
# 将列的子集写入 CSV

hurricanes <- storms |>
  select(!c(lat, long, pressure, ends_with("force_diameter"))) |>
  filter(status == "hurricane") |>
  arrange(desc(wind), name) |>
  distinct(name, year, .keep_all = TRUE)

hurricanes |>
  select(c(year, name, wind)) |>
  write.csv("hurricanes.csv", row.names = FALSE)
```

注意第一个代码块的结果是如何存储为 `hurricanes` 的。为了将 `hurricanes` 存储为 CSV 文件，`select` 首先选择了 3 个特定的列（`year`、`name` 和 `wind`），这些列被写入名为 `hurricanes.csv` 的文件中。

## group_by

现在让我们找出每年最强大的飓风。

考虑以下代码：

```R
# 找出每年最强大的飓风

hurricanes <- read.csv("hurricanes.csv")

hurricanes |>
  group_by(year) |>
  arrange(desc(wind)) |>
  slice_head()
```

注意 `hurricanes.csv` 是如何读入 `hurricanes` 的。然后，使用 `group_by` 函数将每年的所有飓风分组。对于每个组，使用 `arrange(desc(wind))` 按风速降序排列。最后，使用 `slice_head` 输出每个组的首行。因此，呈现了每年的最强风暴。

`slice_max` 用于选择变量中的最大值。考虑如何在我们的代码中应用它：

```R
# 引入 slice_max

hurricanes <- read.csv("hurricanes.csv")

hurricanes |>
  group_by(year) |>
  slice_max(order_by = wind)
```

注意 `hurricanes` 按年份分组。然后，使用 `slice_max` 呈现 `wind` 的最高值。这样做消除了对 `arrange(desc(wind))` 的需求。

## summarize

如果我们想知道每年飓风的数量呢？考虑以下代码：

```R
# 找出每年的飓风数量

hurricanes <- read.csv("hurricanes.csv")

hurricanes |>
  group_by(year) |>
  summarize(hurricanes = n())
```

注意 `summarize` 函数如何利用 `n` 来计算每个组中的行数。

## ungroup

观察我们的 `hurricanes` 数据框，你会注意到存在分组。事实上，这些分组是按年份划分的。在未来的活动中，有时你可能希望取消数据中的分组。相应地，考虑以下内容：

```R
# 展示 ungroup

hurricanes <- read.csv("hurricanes.csv")

hurricanes |>
  group_by(year) |>
  slice_max(order_by = wind) |>
  ungroup()
```

注意使用了 `ungroup` 命令来移除 `tibble` 的分组。

## tidyr

当数据已经组织良好时，`dplyr` 非常有用。

那么如果数据尚未组织良好呢？

为此，`tidyr` 包非常有用！

## 整洁数据 (Tidy Data)

根据 `tidyverse` 的哲学，有三个原则指导着我们所说的整洁数据 (Tidy data)：

1. 每个观测值 (Observation) 占一行；每一行是一个观测值。
2. 每个变量 (Variable) 占一列；每一列是一个变量。
3. 每个值是一个单元格；每个单元格是一个单一值。

在评估数据时，最好查看上述三个原则是否得到遵守。

## 规范化 (Normalizing)

规范化 (Normalizing) 是转换数据的过程，使其符合上述原则。

规范化还可以指转换数据，使其符合上述准则之外更好的设计原则。

从课程文件中下载 `students.csv` 文件并将其放在你的工作目录中。创建如下新代码：

```R
# 读取 CSV

students <- read.csv("students.csv")
View(students)
```

注意这段代码加载了一个名为 `students.csv` 的 CSV 文件并将这些值存储在 `students` 中。

检查这些数据，你可以看到它们是如何不遵循我们之前提到的原则的。你观察到哪些原则没有被遵循？

## 旋转 (Pivoting)

在 `students` 数据集中，你可能会注意到有一些行值实际上应该是列名：“major” (专业) 和 “GPA”。明确地说，这个数据集违反了整洁数据的第二条原则：学生变化的每一种方式都不是一列。

多亏了 `pivot_wider`！我们可以通过旋转数据集将这些变量转换为列。`pivot_wider` 将一个比预期“更长” (Longer) 的数据集（即变量作为行值的数据集）转换为“更宽” (Wider) 的数据集（即把这些变量变成列）。

但该如何操作呢？考虑以下用法：

```R
# 演示 pivot_wider

students <- read.csv("students.csv")

students <- pivot_wider(
  students,
  id_cols = student,
  names_from = attribute,
  values_from = value
)
```

注意 `pivot_wider` 接受几个参数，解释如下：

* 第一个是操作的数据集，`students`。
* 第二个参数 `id_cols` 指定了在转换后的数据集中哪一列最终应该是唯一的。注意在 `pivot_wider` 转换之前，`student` 列中存在重复值。转换后，`student` 列中包含了唯一值。
* 第三个参数 `names_from` 指定了哪一列包含应该变成变量（列）的值。注意在 `pivot_wider` 转换后，`attribute` 列中的值变成了列。
* 最后，第四个参数 `values_from` 指定了用于填充新列值的列。注意在 `pivot_wider` 转换后，`value` 列中的值被用于填充新列。

因为我们的数据变得更加整洁，我们可以对数据做更多的事情！

考虑以下内容：

```R
# 演示按专业计算平均 GPA

students <- read.csv("students.csv")

students <- pivot_wider(
  students,
  id_cols = student,
  names_from = attribute,
  values_from = value
)

students$GPA <- as.numeric(students$GPA)

students |>
  group_by(major) |>
  summarize(GPA = mean(GPA))
```

注意该程序如何利用 `pivot_wider` 和 `tidyr` 来发现学生的平均 GPA。`students` 中的 GPA 被转换为数值。然后，使用管道语法查找 GPA 的平均值。

## stringr

当我们描述的过程在值本身干净时运行良好。然而，如果值本身不整洁呢？

`stringr` 为我们提供了清理字符串的方法。从课程文件中下载 `shows.csv` 并将其放在你的工作目录中。考虑以下程序：

```R
# 统计最喜爱节目的票数

shows <- read.csv("shows.csv")

shows |>
  group_by(show) |>
  summarize(votes = n()) |>
  ungroup() |>
  arrange(desc(votes))
```

注意节目是如何按 `show` 分组的。然后计算票数。最后，票数按降序排列。

查看此程序的结果，你可以看到有许多版本的《阿凡达：最后的气宗》(Avatar: The Last Airbender)。我们可能应该先处理空格问题。

```R
# 清理内部空格

shows <- read.csv("shows.csv")

shows$show <- shows$show |>
  str_trim() |>
  str_squish()

shows |>
  group_by(show) |>
  summarize(votes = n()) |>
  ungroup() |>
  arrange(desc(votes))
```

注意 `str_trim` 用于移除每个记录前后的空格。`str_squish` 随后用于移除字符之间多余的空格。

虽然这些都很好，但大写字母仍存在一些不一致。我们可以如下解决：

```R
# 清理大写字母

shows <- read.csv("shows.csv")

shows$show <- shows$show |>
  str_trim() |>
  str_squish() |>
  str_to_title()

shows |>
  group_by(show) |>
  summarize(votes = n()) |>
  ungroup() |>
  arrange(desc(votes))
```

注意 `str_to_title` 如何用于强制每个字符串使用标题格式 (Title casing)。

最后，我们可以处理《阿凡达：最后的气宗》拼写变体的问题：

```R
# 清理拼写

shows <- read.csv("shows.csv")

shows$show <- shows$show |>
  str_trim() |>
  str_squish() |>
  str_to_title()

shows$show[str_detect(shows$show, "Avatar")] <- "Avatar: The Last Airbender"

shows |>
  group_by(show) |>
  summarize(votes = n()) |>
  ungroup() |>
  arrange(desc(votes))
```

注意 `str_detect` 用于定位包含 “Avatar” 的实例。每一个都被转换为 “Avatar: The Last Airbender”。

虽然这些工具非常有用，但也要考虑需要保持谨慎而不覆盖正确条目的情况。例如，有很多电影都叫 《阿凡达》(Avatar)！我们如何知道投票者不是想投给那些电影呢？

## 总结 (Summing Up)

在本课中，你学习了如何在 R 中清理数据。具体来说，你学习了三个新包，它们都是 `tidyverse` 的一部分：

* [[#dplyr]]
* [[#tidyr]]
* [[#stringr]]

下次见，届时我们将讨论 [[L5：可视化数据 (Visualizing Data)|如何将我们的数据可视化]]。