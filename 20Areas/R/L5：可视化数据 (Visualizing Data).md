# 第5讲：可视化数据 (Visualizing Data)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#ggplot2]]
* [[#标度 (Scales)]]
* [[#标签 (Labels)]]
* [[#填充 (Fill)]]
* [[#主题 (Themes)]]
* [[#保存你的绘图 (Saving Your Plot)]]
* [[#点 (Point)]]
* [[#随时间变化的可视化 (Visualizing Over Time)]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

欢迎回到 CS50 的 R 语言编程入门课程！

今天，我们将学习如何将数据可视化 (Visualizing data)。一个良好的可视化可以帮助我们以一种全新的方式解释和理解数据。

## ggplot2

`ggplot` 中的 “plot” 意味着我们将要绘制我们的数据。

`ggplot` 中的 “gg” 指的是图形语法 (Grammar of graphics)，即可以将图形的各个独立组件聚集在一起来实现数据的可视化。

构成这种图形语法的组件有很多，首先是数据 (Data)。

另一个组件是几何对象 (Geometries)。这些是用于绘图的各种图形表示选项，包括柱状图、点和线。

最后，美学映射 (Aesthetic mappings) 是数据与图形视觉特征之间的关系。例如，在绘图中，水平的 x 轴可能代表每个候选人。然后，垂直的 y 轴可能与每个候选人的票数相关联。正是通过数据与几何对象之间的这种关系，我们才能够可视化并理解图表的美学映射。你可能想象过别人向你展示设计糟糕的图表时的情景：当映射不正确时，数据将变得更难以解释和理解。

下载讲座的源文件并在 R 控制台中运行 `library("tidyverse")`，以便将 `tidyverse` 加载到内存中。然后，按如下方式创建一个可视化：

```R
# 创建一个空白的可视化

votes <- read.csv("votes.csv")

ggplot()
```

注意 `votes.csv` 是如何加载到 `votes` 中的。运行 `ggplot` 时，目前没有任何可视化内容。

我们可以如下向 `ggplot` 提供输入：

```R
# 提供数据

votes <- read.csv("votes.csv")

ggplot(votes)
```

注意 `votes` 是如何提供给 `ggplot` 的。尽管如此，仍然没有任何可视化内容。

我们需要告诉 `ggplot` 我们想要哪种类型的图表：

```R
# 添加第一个几何对象

votes <- read.csv("votes.csv")

ggplot(votes) +
  geom_col()
```

注意 `geom_col` 指定了数据应以列 (Column) 几何对象进行可视化。然而，此时会产生错误。错误指出我们需要指定美学映射。

同时请注意，`+` 操作符有了新的含义：使用 `+` 操作符可以在绘图的基础层之上添加一个新的层 (Layer)。

为了指定美学映射，我们可以如下定义它们：

```R
# 添加 x 和 y 美学映射

votes <- read.csv("votes.csv")

ggplot(votes, aes(x = candidate, y = votes)) +
  geom_col()
```

注意括号内由 `aes` 指定的各种美学映射是如何定义的。例如，`x = candidate` 和 `y = votes` 都是美学映射。现在，`ggplot` 知道了哪些数据映射到了绘图的哪些美学特征。

运行上述代码，我们的第一个可视化图表终于出现了！

## 标度 (Scales)

注意 `ggplot` 是如何决定 `votes` 轴的数值范围为 0 到 200 的。如果我们想提供更多的余量，以便我们可以可视化高达 250 的数值呢？让我们学习一下标度 (Scales)。

标度可以是连续的 (Continuous)，范围从一个数字到另一个数字；也可以是离散的 (Discrete)，这意味着是类别型的。

连续标度具有限制 (Limits)。例如，`votes` 中提供的数据范围是 0 到 200。因此，我们可以如下修改这些限制：

```R
# 调整 y 轴标度

votes <- read.csv("votes.csv")

ggplot(votes, aes(x = candidate, y = votes)) +
  geom_col() +
  scale_y_continuous(limits = c(0, 250))
```

注意 y 轴的标度是如何通过 `scale_y_continuous` 修改为 0 到 250 的。同样地，这是通过 `+` 操作符提供的一个新层。

## 标签 (Labels)

此外，人们可以向绘图添加标签 (Labels)。考虑以下内容：

```R
# 添加标签

votes <- read.csv("votes.csv")

ggplot(votes, aes(x = candidate, y = votes)) +
  geom_col() +
  scale_y_continuous(limits = c(0, 250)) +
  labs(
    x = "Candidate",
    y = "Votes",
    title = "Election Results"
  )
```

注意如何为 `x`、`y` 和 `title` 提供标签。这些也是通过 `+` 操作符添加的新层。

## 填充 (Fill)

填充 (Fill) 颜色也可以根据候选人名称进行更改。考虑以下内容：

```R
# 为 geom_col 添加填充美学映射

votes <- read.csv("votes.csv")

ggplot(votes, aes(x = candidate, y = votes)) +
  geom_col(aes(fill = candidate)) +
  scale_y_continuous(limits = c(0, 250)) +
  labs(
    x = "Candidate",
    y = "Votes",
    title = "Election Results"
  )
```

注意填充颜色是通过 `aes` 函数依赖于 `candidate` 的。

我们可能希望调整填充颜色，使其对色盲 (Color blindness) 人士友好。我们可以按如下方式操作：

```R
# 使用 viridis 标度为色盲设计

votes <- read.csv("votes.csv")

ggplot(votes, aes(x = candidate, y = votes)) +
  geom_col(aes(fill = candidate)) +
  scale_fill_viridis_d("Candidate") +
  scale_y_continuous(limits = c(0, 250)) +
  labs(
    x = "Candidate",
    y = "Votes",
    title = "Election Results"
  )
```

注意 `viridis` 标度是如何通过 `scale_fill_viridis_d` 函数提供的。

## 主题 (Themes)

人们还可以修改 `ggplot` 使用的主题 (Themes)。你可以按如下方式操作：

```R
# 调整 ggplot 主题

votes <- read.csv("votes.csv")

ggplot(votes, aes(x = candidate, y = votes)) +
  geom_col(aes(fill = candidate)) +
  scale_fill_viridis_d("Candidate") +
  scale_y_continuous(limits = c(0, 250)) +
  labs(
    x = "Candidate",
    y = "Votes",
    title = "Election Results"
  ) +
  theme_classic()
```

注意提供了 `theme_classic`。`ggplot2` 提供了几种主题。

## 保存你的绘图 (Saving Your Plot)

最后，绘图是可以保存的。

```R
# 保存文件

votes <- read.csv("votes.csv")

p <- ggplot(votes, aes(x = candidate, y = votes)) +
  geom_col(aes(fill = candidate)) +
  scale_fill_viridis_d("Candidate") +
  scale_y_continuous(limits = c(0, 250)) +
  labs(
    x = "Candidate",
    y = "Votes",
    title = "Election Results"
  ) +
  theme_classic()

ggsave(
  "votes.png",
  plot = p,
  width = 1200,
  height = 900,
  units = "px"
)
```

注意整个绘图被命名为 `p`。然后，使用 `ggsave`，指定文件名、绘图对象（在本例中为 `p`）、高度、宽度和单位。

通过执行此代码，你保存了你的第一个绘图。恭喜！

## 点 (Point)

现在，让我们看看一种名为点 (Point) 的新几何对象。

想象一组代表糖果价格百分位 (Price percentile) 和含糖百分位 (Sugar percentile) 的数据。

你可以想象如何将含糖百分位映射在 y 轴上，而将价格百分位记录在 x 轴上。

这可以在代码形式中实现如下：

```R
# 引入 geom_point

load("candy.RData")

ggplot(
  candy,
  aes(x = price_percentile, y = sugar_percentile)
) +
  geom_point()
```

注意数据 `candy` 是如何提供给 `ggplot` 函数的。然后，使用 `aes` 函数设置美学映射。例如，`price_percentile` 被分配到 x 轴。最后，运行 `geom_point` 函数。

运行此代码会导致在绘图中以点表示数据。

可以按如下方式添加标签：

```R
# 添加标签和主题

load("candy.RData")

ggplot(
  candy,
  aes(x = price_percentile, y = sugar_percentile)
) +
  geom_point() +
  labs(
    x = "Price",
    y = "Sugar",
    title = "Price and Sugar"
  ) +
  theme_classic()
```

注意如何为 `x`、`y` 和 `title` 提供标签。此外，还指定了一个主题。

现在，有许多点发生了重叠。`jitter` (抖动) 可以用来帮助可视化重叠的点：

```R
# 引入 geom_jitter

ggplot(
  candy,
  aes(x = price_percentile, y = sugar_percentile)
) +
  geom_jitter() +
  labs(
    x = "Price",
    y = "Sugar",
    title = "Price and Sugar"
  ) +
  theme_classic()
```

注意 `geom_point` 被替换为了 `geom_jitter`。这允许对重叠的点进行可视化。

我们可以为我们的点添加颜色美学特征：

```R
# 引入大小和颜色美学映射

ggplot(
  candy,
  aes(x = price_percentile, y = sugar_percentile)
) +
  geom_jitter(
    color = "darkorchid",
    size = 2
  ) +
  labs(
    x = "Price",
    y = "Sugar",
    title = "Price and Sugar"
  ) +
  theme_classic()
```

注意所有点如何被更改为同一种颜色。

此外，我们可以更改点的大小和形状：

```R
# 引入点形状和填充颜色

ggplot(
  candy,
  aes(x = price_percentile, y = sugar_percentile)
) +
  geom_jitter(
    color = "darkorchid",
    fill = "orchid",
    shape = 21,
    size = 2
  ) +
  labs(
    x = "Price",
    y = "Sugar",
    title = "Price and Sugar"
  ) +
  theme_classic()
```

注意形状 (Shape) 和大小 (Size) 的变化。你可以查阅文档以了解哪些数字对应于哪些形状。

## 随时间变化的可视化 (Visualizing Over Time)

你可以想象数据是如何随时间表示的。

例如，考虑有关飓风 Anita (Hurricane Anita) 的数据如何随时间表示。

我们可以像之前那样用点进行绘图：

```R
# 使用 geom_point 进行可视化

load("anita.RData")

ggplot(anita, aes(x = timestamp, y = wind)) +
  geom_point()
```

注意时间戳 (Timestamp) 和风速是如何随时间以点的形式放置的。

虽然这种可视化很有用，但如果能用线条显示风速是增加还是减少，可能会更有用制。可以按如下方式用线连接每个点：

```R
# 引入 geom_line

load("anita.RData")

ggplot(anita, aes(x = timestamp, y = wind)) +
  geom_line()
```

注意 `geom_line` 被作为一个新层使用。

结果是一系列在每个时间戳改变方向的线条。如果我们能结合点和线呢？当然可以！

```R
# 结合 geom_line 和 geom_point

load("anita.RData")

ggplot(anita, aes(x = timestamp, y = wind)) +
  geom_line() +
  geom_point(color = "deepskyblue4")
```

注意如何通过 `geom_line` 添加一个线条层。然后，使用 `deepskyblue4` 颜色通过 `geom_point` 添加一个点层。

美学特征可以以各种方式修改：

```R
# 尝试 geom_line 和 geom_point 的美学特征

load("anita.RData")

ggplot(anita, aes(x = timestamp, y = wind)) +
  geom_line(
    linetype = 1,
    linewidth = 0.5
  ) +
  geom_point(
    color = "deepskyblue4",
    size = 2
  )
```

注意线型 (Linetype) 和线宽 (Linewidth) 的修改。然后，更改了点的大小。你可以查阅文档以了解关于各种线型的更多信息。

与我们今天之前的绘图一样，我们可以添加标签和主题：

```R
# 添加标签并调整主题

load("anita.RData")

ggplot(anita, aes(x = timestamp, y = wind)) +
  geom_line(
    linetype = 1,
    linewidth = 0.5
  ) +
  geom_point(
    color = "deepskyblue4",
    size = 2
  ) +
  labs(
    y = "Wind Speed (Knots)",
    x = "Date",
    title = "Hurricane Anita"
  ) +
  theme_classic()
```

注意 `labs` 如何允许我们指定 `y`、`x` 和 `title` 的标签。然后，启用了 `theme_classic`。

作为最后的修饰，我们还可以添加一条水平线来划分飓风状态。Anita 飓风是在什么时候变成飓风的？

```R
# 添加水平线以划分飓风状态

load("anita.RData")

ggplot(anita, aes(x = timestamp, y = wind)) +
  geom_line(
    linetype = 1,
    linewidth = 0.5
  ) +
  geom_point(
    color = "deepskyblue4",
    size = 2
  ) +
  geom_hline(
    linetype = 3,
    yintercept = 64
  ) +
  labs(
    y = "Wind Speed (Knots)",
    x = "Date",
    title = "Hurricane Anita"
  ) +
  theme_classic()
```

注意如何添加一个新层，在 `yintercept = 64` 处显示一条线，以指明任何 64 或更高值都被视为飓风。线型被指定为 3 或虚线 (Dotted)。

## 总结 (Summing Up)

在本课中，你学习了如何在 R 中将数据可视化. 具体来说，你了解了：

* [[#ggplot2]]
* [[#标度 (Scales)]]
* [[#标签 (Labels)]]
* [[#填充 (Fill)]]
* [[#主题 (Themes)]]
* [[#点 (Point)]]
* [[#随时间变化的可视化 (Visualizing Over Time)|随时间变化的可视化 (Visualizing over time)]]

下次见，届时我们将讨论 [[L6：测试程序 (Testing Programs)|如何测试我们的程序]]。