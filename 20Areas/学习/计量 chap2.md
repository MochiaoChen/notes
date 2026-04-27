# 计量 Chap2

## Simple Regression Model 的定义与核心术语

在计量经济学中，Simple Regression Model 的核心目的在于研究变量 $y$ 是如何随着变量 $x$ 的变化而变化的 。换言之，它通过变量 $x$ 来解释变量 $y$。该模型最基础的代数表达式为：

$$
y=\beta_{0}+\beta_{1}x+u
$$

在这个等式中，每一项都有其特定的统计学与经济学含义，我们需要精确界定这些专业术语 ：

- **y**：位于方程左侧，是我们试图去解释或预测的对象。在计量经济学中，它有多种称呼，最常见的是 Dependent variable 以及 Explained variable 。在不同的应用语境下，它也可以被称为 Response variable 、Predicted variable 或者 Regressand 。
- **x**：位于方程右侧，是用来解释 $y$ 变化的变量。它通常被称为 Independent variable 或者是 Explanatory variable 。此外，文献中也经常使用 Control variable 、Predictor variable 或 Regressor  来指代这一项。
- **u**：代表了所有影响 $y$ 但并没有被 $x$ 包含进去的其他因素的总和。我们严格称其为 Error term 。由于这些因素在当前模型中无法被显式地观测与衡量，它也常被叫做 Disturbance 或 Unobservables 。
- **β0​**：模型的 Intercept ，在几何上代表回归线与纵轴的交点。
- **β1​**：模型的 Slope parameter ，这是经济学分析与政策评估中最核心的参数，它衡量了 $x$ 对 $y$ 的边际影响。
  
### 模型的数学解释与因果推断基础

当我们试图赋予模型因果解释（Causal interpretation）时，核心关注的问题是：如果 Independent variable 增加一个单位，Dependent variable 会发生多大程度的改变 ？

首先，我们写出 Simple Regression Model 的基准方程：

$$
y=\beta_{0}+\beta_{1}x+u
$$

现在，假设 Independent variable $x$ 发生了一个增量变化 $\Delta x$，同时 Error term $u$ 也发生了一个潜在的增量变化 $\Delta u$。这些变化最终会导致 Dependent variable $y$ 产生相应的增量 $\Delta y$。
我们可以写出变化后的新方程：

$$
y+\Delta y=\beta_{0}+\beta_{1}(x+\Delta x)+(u+\Delta u)
$$
接下来，我们将变化后的方程减去基准方程，以孤立出变化量：

$$
(y+\Delta y)-y=[\beta_{0}+\beta_{1}(x+\Delta x)+(u+\Delta u)]-[\beta_{0}+\beta_{1}x+u]
$$
展开右侧的各项：

$$
\Delta y=\beta_{0}+\beta_{1}x+\beta_{1}\Delta x+u+\Delta u-\beta_{0}-\beta_{1}x-u
$$
抵消掉相同的项后，我们得到差分方程：

$$
\Delta y=\beta_{1}\Delta x+\Delta u
$$
为了衡量 $x$ 的单位变化对 $y$ 的影响，我们在方程两边同时除以 $\Delta x$：

$$
\frac{\Delta y}{\Delta x}=\beta_{1}+\frac{\Delta u}{\Delta x}
$$

根据上述方程的差分形式推导，只要能够保证 $\frac{\Delta u}{\Delta x}=0$，我们就可以得出结论：

$$
\frac{\Delta y}{\Delta x}=\beta_{1}
$$

这里的关键前提 $\frac{\Delta u}{\Delta x}=0$ 意味着，我们在改变 $x$ 的同时，必须保持其他所有隐藏在 $u$ 中的因素固定不变 。这正是经济学中经典的「保持其他条件不变」（all other things remain equal）假设 。只有当这个条件成立时，$\beta_1$ 才具有真正的因果效应解释力。在现实的横截面数据中，Simple Regression Model 很少能直接适用，但它的讨论对于建立计量经济学的直觉非常有帮助 。

### 两个 Examples

为了更好地理解上述抽象概念，我们举两个具体的例子：

1. **农业产量与肥料**：我们可以建立模型 yield = $\beta_0$ + $\beta_1$ fertilizer + $u$。这里的 $\beta_1$ 衡量了在保持降雨量（Rainfall）、土地质量（Land quality）以及寄生虫（Parasites）等其他因素不变的情况下，肥料对大豆产量的单纯影响 。
2. **工资方程（Wage equation）**：我们可以建立模型 wage = $\beta_0$ + $\beta_1$ educ + $u$。这里的 $\beta_1$ 代表了在固定工作经验（Labor force experience）、当前雇主连任时间（Tenure）、职业道德与智力（Intelligence）等因素的情况下，额外增加一年教育对小时工资的预期改变 。

## Conditional Mean Independence Assumption 与 Population Regression Function

在明确了差分推导后，我们需要引入一个更严格、更具统计学意义的假设，来保证我们能够得到真正的 Causal interpretation 。这就是 Conditional mean independence assumption 。
它的数学表达为：

$$
E(u|x)=0
$$

这个等式的统计学含义非常深刻。它要求 Explanatory variable 中不能包含任何关于未观测因素均值的信息 。换句话说，无论 $x$ 取什么值，$u$ 的条件均值都必须严格为零。
结合Wage equation的例子 ：

$$
wage=\beta_{0}+\beta_{1}educ+u
$$
在这个模型中，Conditional mean independence assumption 往往很难成立 。因为受教育程度更高的人，通常在智力等未被观测的特征（隐藏在 $u$ 中）上也表现得更高 。这意味着给定一个更高的教育水平，$u$ 的期望值也会随之增加，从而违反了 $E(u|x)=0$ 的核心前提假设 。
当 Conditional mean independence assumption 成立时，我们可以推导出 Population regression function 。严格的推导过程如下：

$$
E(y|x)=E(\beta_{0}+\beta_{1}x+u|x)
$$

由于 $\beta_{0}$ 以及 $\beta_{1}x$ 在给定 $x$ 的条件下可以视为常数，我们利用期望的线性性质将其提出：

$$
E(y|x)=\beta_{0}+\beta_{1}x+E(u|x)
$$
代入核心假设 $E(u|x)=0$：

$$
E(y|x)=\beta_{0}+\beta_{1}x
$$

这就引出了 Population regression function 的物理意义：Dependent variable 的平均值可以表达为 Explanatory variable 的线性函数 。我们在坐标系中看到的回归线，正是代表了在特定的 $x$ 取值下，$y$ 的平均预期水平 。

## 推导 Ordinary Least Squares 估计量

既然我们已经明确了 Population Regression Function 的理论概念，下一步就是将其应用到实际数据中 。在现实的实证研究中，我们无法观察到整个总体的全部特征，因此必须依赖样本数据来估计模型参数 。

假设我们拥有一个包含 $n$ 个观测值的随机样本（Random sample），记作 $\{(x_i,y_i):i=1,...,n\}$。这里的 $x_i$ 和 $y_i$ 分别代表了第 $i$ 个观测值的 Explanatory variable 和 Dependent variable 的具体数值 。

在构建模型时，我们将变量 $y$ 拆分为两个独立的组成部分：由 $x$ 成功解释的系统性部分（Systematic part），以及未能被 $x$ 解释的非系统性部分（Unsystematic part） 。
为了在坐标系的数据点中拟合出一条「尽可能好」的回归线 ，我们需要引入两个极其关键的统计量：Fitted values 与 Residuals 。

- **Fitted values**（也可称为 Predicted values）在代数上表达为 $\hat{y}_i=\hat{\beta}_0+\hat{\beta}_1x_i$。这里的 $\hat{\beta}_0$ 和 $\hat{\beta}_1$ 正是我们迫切需要求解的样本估计量。
- **Residuals** 则是实际观测值与模型拟合值之间的垂直偏差，严格定义为 $\hat{u}_i=y_i-\hat{y}_i=y_i-\hat{\beta}_0-\hat{\beta}_1x_i$。

### 数学推导：最小化残差平方和

Ordinary Least Squares (OLS) 方法的核心优化准则，顾名思义，就是最小化残差平方和（Minimize sum of squared regression residuals） 。其数学目标函数可以写为 ：

$$
\min_{\hat{\beta}_0,\hat{\beta}_1}\sum_{i=1}^n\hat{u}_i^2=\sum_{i=1}^n(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)^2
$$
为了求解这个极值问题，我们需要分别对未知参数 $\hat{\beta}_0$ 和 $\hat{\beta}_1$ 求一阶偏导数，并令它们等于零。这在最优化理论中被称为一阶条件（First Order Conditions）。

#### 第一步：对 β^​0​ 求偏导

$$
\frac{\partial}{\partial\hat{\beta}_0}\sum_{i=1}^n(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)^2=-2\sum_{i=1}^n(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)=0
$$
将上式化简，剔除常数项 -2 后，我们直接得到了 OLS 极其重要的第一个代数性质 ：

$$
\sum_{i=1}^n\hat{u}_i=0
$$
这个等式清晰地表明，在 OLS 拟合下，所有 Residuals 的总和必然严格为零 。

我们将上述偏导等式中的求和符号展开，推导 Intercept 的估计公式：

$$
\sum_{i=1}^ny_i-n\hat{\beta}_0-\hat{\beta}_1\sum_{i=1}^nx_i=0
$$
等式两边同除以样本总数 $n$，可以得到 ：

$$
\bar{y}=\hat{\beta}_0+\hat{\beta}_1\bar{x}
$$
这构成了 OLS 的第二个重要代数性质：样本的均值坐标点 $(\bar{x},\bar{y})$ 必定落在拟合的回归线上 。经过简单的移项，我们就得到了 $\hat{\beta}_0$ 的最终代数表达式 ：

$$
\hat{\beta}_0=\bar{y}-\hat{\beta}_1\bar{x}
$$

#### 第二步：对 $β^​1$​ 求偏导

$$
\frac{\partial}{\partial\hat{\beta}_1}\sum_{i=1}^n(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)^2=-2\sum_{i=1}^nx_i(y_i-\hat{\beta}_0-\hat{\beta}_1x_i)=0
$$
化简后，我们得到了 OLS 的第三个代数性质，即 Regressors 与 Residuals 之间的样本协方差为零 ：

$$
\sum_{i=1}^nx_i\hat{u}_i=0
$$
接下来，将前面得到的 $\hat{\beta}_0=\bar{y}-\hat{\beta}_1\bar{x}$ 代入上式，并利用求和算子的代数性质进行展开：

$$
\sum_{i=1}^nx_i(y_i-(\bar{y}-\hat{\beta}_1\bar{x})-\hat{\beta}_1x_i)=0
$$

$$
\sum_{i=1}^nx_i(y_i-\bar{y})-\hat{\beta}_1\sum_{i=1}^nx_i(x_i-\bar{x})=0
$$
利用离差乘积的和等于原始变量乘积的和减去均值乘积的和这一统计学基本性质，最终我们可以解出 Slope parameter 的估计量 ：

$$
\hat{\beta}_1=\frac{\sum_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})}{\sum_{i=1}^n(x_i-\bar{x})^2}
$$

## Goodness-of-Fit 与平方和分解推导

在通过 Ordinary Least Squares 方法估算出模型参数后，一个自然而然的学术问题是：我们的 Explanatory variable 在多大程度上成功解释了 Dependent variable 的变化 ？为了严谨地回答这个问题，我们需要引入 Goodness-of-Fit 的概念，并进行严格的方差分解数学推导。
首先，我们定义三个核心的平方和指标：

1. **Total sum of squares (SST)**：衡量 Dependent variable 的总变异程度，公式为 $SST\equiv\sum_{i=1}^{n}(y_{i}-\overline{y})^{2}$。
2. **Explained sum of squares (SSE)**：衡量模型拟合值所能解释的变异程度，公式为 $SSE\equiv\sum_{i=1}^{n}(\hat{y}_{i}-\overline{y})^{2}$。
3. **Residual sum of squares (SSR)**：衡量模型未能解释的变异程度，公式为 $SSR\equiv\sum_{i=1}^{n}\hat{u}_{i}^{2}$。

### 变异分解的推导

我们现在来证明这三者之间存在极其优美的加和关系：$SST=SSE+SSR$。
对于任意一个观测值的离差 $(y_{i}-\overline{y})$，我们可以通过加上并减去拟合值 $\hat{y}_{i}$ 来进行恒等变形：

$$
y_{i}-\overline{y}=(y_{i}-\hat{y}_{i})+(\hat{y}_{i}-\overline{y})
$$
根据前面的定义，实际值与拟合值之差就是 Residual $\hat{u}_{i}$，代入上式得：

$$
y_{i}-\overline{y}=\hat{u}_{i}+(\hat{y}_{i}-\overline{y})
$$
为了得到 SST，我们将等式两边同时平方并对所有样本求和 ：

$$
\sum_{i=1}^{n}(y_{i}-\overline{y})^{2}=\sum_{i=1}^{n}[\hat{u}_{i}+(\hat{y}_{i}-\overline{y})]^{2}
$$
将右侧的完全平方公式展开：

$$
\sum_{i=1}^{n}(y_{i}-\overline{y})^{2}=\sum_{i=1}^{n}\hat{u}_{i}^{2}+\sum_{i=1}^{n}(\hat{y}_{i}-\overline{y})^{2}+2\sum_{i=1}^{n}\hat{u}_{i}(\hat{y}_{i}-\overline{y})
$$

$$
SST=SSR+SSE+2\sum_{i=1}^{n}\hat{u}_{i}(\hat{y}_{i}-\overline{y})
$$
要使 $SST=SSE+SSR$ 成立，我们必须证明最后的交叉项求和等于零 。我们把交叉项提取出来进行推导：

$$
\sum_{i=1}^{n}\hat{u}_{i}(\hat{y}_{i}-\overline{y})=\sum_{i=1}^{n}\hat{u}_{i}(\hat{\beta}_{0}+\hat{\beta}_{1}x_{i}-\overline{y})
$$
利用求和符号的分配律将其展开：

$$
\sum_{i=1}^{n}\hat{u}_{i}(\hat{y}_{i}-\overline{y})=\hat{\beta}_{0}\sum_{i=1}^{n}\hat{u}_{i}+\hat{\beta}_{1}\sum_{i=1}^{n}\hat{u}_{i}x_{i}-\overline{y}\sum_{i=1}^{n}\hat{u}_{i}
$$
回顾我们在上一节推导的 Ordinary Least Squares 一阶条件（代数性质）：残差的总和为零（$\sum_{i=1}^{n}\hat{u}_{i}=0$），且 Regressor 与 Residual 的内积也为零（$\sum_{i=1}^{n}x_{i}\hat{u}_{i}=0$）。将这两个性质代入上式，显然三项全部等于零。
因此交叉项严格为零，我们完美证明了总变异可以被正交分解为解释部分与未解释部分：

$$
SST=SSE+SSR
$$
基于这个分解，计量经济学定义了 R-squared 这一 Goodness-of-Fit 核心指标：

$$
R^{2}\equiv\frac{SSE}{SST}=1-\frac{SSR}{SST}
$$

R-squared 的物理意义十分明确：它测量了模型回归所能解释的总变异的分数（或百分比）。不过需要学术界极度警惕的一点是，一个很高的 R-squared 绝对不能作为证明模型存在 Causal interpretation 的充要条件 。高拟合度仅仅代表数据上的强相关性。

## Units of Measurement 与 Functional Form 

在实际的计量实证中，数据的存在形式多种多样。本节重点讨论改变数据衡量单位以及使用对数进行非线性建模的影响。

### 衡量单位的改变

如果我们对 Dependent variable 或 Independent variable 的测度单位进行线性缩放（例如把以「美元」为单位的数据改为以「千美元」为单位），模型的拟合本质并不会改变，但系数的数值需要做相应调整以保持逻辑一致性 。

例如幻灯片中的案例：

原方程为 $\hat{salary}=963.191+18.501roe$。

如果我们定义 $salardol=1000\times salary$，那么新模型的系数也会整体放大一千倍，变为 $\widehat{salardol}=963191+18501roe$。

### 引入对数的非线性 Functional Form

经济学变量之间往往表现出非线性关系（如边际报酬递减）。通过对变量取自然对数（Natural logarithm），我们可以将某些非线性关系转化为 Ordinary Least Squares 能够处理的线性关系，并且赋予系数更具经济学直觉的解释。

幻灯片总结了三种核心的对数 Functional Form ：

1. **Log-level (Semi-logarithmic form)**：
模型设定为 $\log(y)=\beta_{0}+\beta_{1}x+u$。
此处的 Slope parameter $\beta_{1}$ 的数学定义为：
$$\beta_{1}=\frac{\Delta\log(y)}{\Delta x}\approx\frac{\frac{\Delta y}{y}}{\Delta x}$$这意味着，当 Independent variable 增加一个单位时，Dependent variable 预期的百分比变化量。换句话说，$\beta_{1}$ 衡量的是 $y$ 的增长率（Growth rate）或半弹性 。

2. **Log-log (Log-logarithmic form)**：
模型设定为 $\log(y)=\beta_{0}+\beta_{1}\log(x)+u$。
此处的 Slope parameter $\beta_{1}$ 的数学定义为：
$$\beta_{1}=\frac{\Delta\log(y)}{\Delta\log(x)}\approx\frac{\frac{\Delta y}{y}}{\frac{\Delta x}{x}}$$
这在经济学中被称为常弹性模型（Constant elasticity model）。它表示当 $x$ 变化 1% 时，$y$ 会产生 $\beta_{1}\%$ 的变化 。

3. **Level-log 模型**：
模型设定为 $y=\beta_{0}+\beta_{1}\log(x)+u$。根据类似的差分近似原理，它的解释为：当 $x$ 增加 1% 时，$y$ 的绝对数值会发生大约 $\frac{\beta_{1}}{100}$ 个单位的变化 。

### 估计量的随机性与四个核心假设

首先，我们需要深刻理解一个统计学概念：我们计算出来的估计量 $\hat{\beta}_{0}$ 和 $\hat{\beta}_{1}$ 本质上是 Random variables 。为什么？因为我们的数据来源于一个 Random sample 。如果在总体中重新进行随机抽样，我们会得到完全不同的一组数据，进而计算出不同的估计值 。因此，我们真正关心的学术问题是：在反复抽样的平均意义上，这些估计量是否等于总体的真实参数 ？
为了在数学上严格证明这一点，讲义引入了 Simple Linear Regression 模型的前四个 Standard assumptions ：

- **SLR.1 (Linear in parameters)**：总体模型中 $y$ 和 $x$ 满足线性关系，即 $y=\beta_{0}+\beta_{1}x+u$。
- **SLR.2 (Random sampling)**：我们拥有一组从总体中随机抽取的样本 $\{(x_{i},y_{i}):i=1,...,n\}$。每个数据点都服从总体的线性方程 。
- **SLR.3 (Sample variation in the explanatory variable)**：样本中 $x$ 的值不能全部相同，即 $\sum_{i=1}^{n}(x_{i}-\overline{x})^{2}>0$。如果 $x$ 没有任何变异性，我们就无法研究 $x$ 的变化如何导致 $y$ 的变化 。
- **SLR.4 (Zero conditional mean)**：Error term 给定 $x$ 的条件期望为零，即 $E(u|x)=0$。这意味着解释变量不能包含任何关于未观测因素均值的信息 。

### OLS 的无偏性及其数学证明

在满足假设 SLR.1 到 SLR.4 的前提下，我们指出 OLS 估计量是无偏的，即 $E(\hat{\beta}_{0})=\beta_{0}$ 且 $E(\hat{\beta}_{1})=\beta_{1}$。无偏性的经济学意义在于，虽然在某一次特定的样本抽样中，估计值可能会偏离真实值很远，但在反复多次抽样的平均意义上，它将准确地等于刻画总体真实关系的参数 。

接下来我们证明 $\hat{\beta}_{1}$ 的无偏性 。
为了简化书写，我们定义 $x$ 的总变异为 $SST_{x}=\sum_{i=1}^{n}(x_{i}-\overline{x})^{2}$。同时定义 $x$ 的离差为 $d_{i}=x_{i}-\overline{x}$。
回顾我们在第三节推导出的公式：

$$
\hat{\beta}_{1}=\frac{\sum_{i=1}^{n}(x_{i}-\overline{x})(y_{i}-\overline{y})}{SST_{x}}
$$
利用代数性质 $\sum_{i=1}^{n}(x_{i}-\overline{x})\overline{y}=0$，分子可以等价化简为 $\sum_{i=1}^{n}d_{i}y_{i}$。

我们将 SLR.1 假设中的真实数据生成过程 $y_{i}=\beta_{0}+\beta_{1}x_{i}+u_{i}$ 代入上式 ：

$$
\hat{\beta}_{1}=\frac{\sum_{i=1}^{n}d_{i}(\beta_{0}+\beta_{1}x_{i}+u_{i})}{SST_{x}}
$$
将分子展开为三项相加：

$$
\sum_{i=1}^{n}d_{i}\beta_{0}+\sum_{i=1}^{n}d_{i}\beta_{1}x_{i}+\sum_{i=1}^{n}d_{i}u_{i}
$$
由于离差之和严格为零（即 $\sum_{i=1}^{n}d_{i}=0$），第一项等于零。

对于第二项，我们提取常数 $\beta_{1}$，得到 $\beta_{1}\sum_{i=1}^{n}(x_{i}-\overline{x})x_{i}$，这在数学上等价于 $\beta_{1}\sum_{i=1}^{n}(x_{i}-\overline{x})^{2}$，也就是 $\beta_{1}SST_{x}$。

因此，我们将估计量 $\hat{\beta}_{1}$ 成功分解为了两部分：

$$
\hat{\beta}_{1}=\frac{\beta_{1}SST_{x}+\sum_{i=1}^{n}d_{i}u_{i}}{SST_{x}}=\beta_{1}+\frac{1}{SST_{x}}\sum_{i=1}^{n}d_{i}u_{i}
$$

现在，我们在给定样本 Independent variable 取值的条件下对等式两边求 Expected values 。在这个条件期望的操作下，$d_{i}$ 和 $SST_{x}$ 被视为非随机的常数 ：

$$
E(\hat{\beta}_{1})=\beta_{1}+\frac{1}{SST_{x}}\sum_{i=1}^{n}d_{i}E(u_{i})
$$

根据假设 SLR.4，我们已知 $E(u_{i}|x_{i})=0$。将其代入上式，导致最后一项彻底消失。

最终我们得到：

$$
E(\hat{\beta}_{1})=\beta_{1}
$$

至此，我们在数学上证明了 Slope parameter 估计量的无偏性 。$\hat{\beta}_{0}$ 的推导逻辑与此完全一致 。

## Homoskedasticity 假设与 OLS 估计量的 Variances

在上一节中，我们从数学上证明了 Ordinary Least Squares 估计量的 Unbiasedness 。但是，仅仅知道估计量在平均意义上等于真实参数是远远不够的。我们自然需要追问：在每一次具体的随机抽样中，这些估计值偏离真实值的波动范围到底有多大 ？

这种由随机抽样带来的不确定性（Sampling variability）是通过估计量的 Variances，即 $Var(\hat{\beta}_{0})$ 和 $Var(\hat{\beta}_{1})$ 来严格衡量的 。

### 引入SRL5：Homoskedasticity

为了能够推导出这些 Variances 的具体代数表达式，我们必须引入 Simple Linear Regression 模型的第五个经典假设 SLR.5，即 Homoskedasticity（同方差性）。

它的数学条件表达为：

$$
Var(u|x)=\sigma^{2}
$$

这个等式的统计学内涵非常深刻。它要求 Unobserved factors 的变异程度（即方差）必须是一个常数 $\sigma^{2}$，绝对不能依赖于 Explanatory variable $x$ 的具体取值 。幻灯片中提供了一个违反该假设的典型实证反例（即存在 Heteroskedasticity）：在讨论 Wage and education 的关系时，随着受教育年限的提高，工资的未观测决定因素（如个人能力、机遇等）的方差往往也会显著放大，这就违背了同方差假设 。

### 推导 OLS 估计量的方差

在假设 SLR.1 到 SLR.5 共同成立的严苛前提下，我们可以得到给出了估计量 Variances 的精确代数解 。对于我们最关心的 Slope parameter，其方差为：

$$
Var(\hat{\beta}_{1})=\frac{\sigma^{2}}{SST_{x}}
$$
证明如下：

**Step 1：回顾 Estimator 的代数展开式**在上一节证明 Unbiasedness 时，我们将 $\hat{\beta}_{1}$ 进行了分解。为了书写简洁，我们令离差 $d_{i}=x_{i}-\overline{x}$，此时 $SST_{x}=\sum_{i=1}^{n}d_{i}^{2}$。
展开后的公式为 ：

$$
\hat{\beta}_{1}=\beta_{1}+\frac{1}{SST_{x}}\sum_{i=1}^{n}d_{i}u_{i}
$$
**Step 2：对等式两边应用 Variance 算子**在给定样本 Independent variable 取值的条件下，我们对等式两边求 Variance 。

$$
Var(\hat{\beta}_{1})=Var\left(\beta_{1}+\frac{1}{SST_{x}}\sum_{i=1}^{n}d_{i}u_{i}\right)
$$
**Step 3：利用 Variance 的基本代数性质化简**
这里需要运用两个统计学法则：
第一，总体的真实参数 $\beta_{1}$ 是一个固定的常数，常数的 Variance 严格为 0。
第二，因为我们是在给定 $x$ 的条件下求 Variance，所以 $d_{i}$ 和 $SST_{x}$ 都在此条件下被视为非随机的常数。根据公式 $Var(aX)=a^{2}Var(X)$，当我们将常数项 $\frac{1}{SST_{x}}$ 提取出算子外部时，必须对其进行平方 。

$$
Var(\hat{\beta}_{1})=\left(\frac{1}{SST_{x}}\right)^{2}Var\left(\sum_{i=1}^{n}d_{i}u_{i}\right)
$$
**Step 4：处理加和项的 Variance**根据 Assumption SLR.2 也就是 Random sampling 假设，不同的观测值之间是相互独立的，这意味着不同 Error terms 之间不存在协方差。因此，和的 Variance 就等于各个项 Variance 的总和 。同时，我们再次将常数 $d_{i}$ 提取出来并平方 ：

$$
Var\left(\sum_{i=1}^{n}d_{i}u_{i}\right)=\sum_{i=1}^{n}Var(d_{i}u_{i})=\sum_{i=1}^{n}d_{i}^{2}Var(u_{i})
$$
**Step 5：引入 Homoskedasticity 假设**这是极其关键的一步。根据 Assumption SLR.5，所有的 Error term 具有完全相同的条件方差，即 $Var(u_{i})=\sigma^{2}$。我们将未知的常量 $\sigma^{2}$ 代入上式，并将其作为公因式提取到求和符号的前面 ：

$$
=\sum_{i=1}^{n}d_{i}^{2}\sigma^{2}=\sigma^{2}\sum_{i=1}^{n}d_{i}^{2}
$$
**Step 6：代回原式并完成最终化简**我们观察到，$\sum_{i=1}^{n}d_{i}^{2}$ 的数学定义刚好就是 $SST_{x}$。我们将 Step 5 得到的结果代回 Step 3 的等式中 ：

$$
Var(\hat{\beta}_{1})=\left(\frac{1}{SST_{x}}\right)^{2}(\sigma^{2}SST_{x})
$$
分子和分母同时消去一个 $SST_{x}$ 后，我们就得到了最终的结果 ：
$$
Var(\hat{\beta}_{1})=\frac{\sigma^{2}}{SST_{x}}
$$
通过这个推导，我们在数学上清晰地看到了 Error variance（$\sigma^{2}$）以及样本变异程度（$SST_{x}$）是如何直接决定参数估计精度的。

在这个公式中，我们可以清晰地提炼出影响估计量抽样变异性的三大核心因素 ：

1. **Error variance σ2 越大，估计量的 Variance 就越大**。隐藏在 $u$ 中的不可观测因素的变动越剧烈，系统中的「噪声」就越大，我们的估计也就越不精确 。
2. **总样本量 n 越小，估计量的 Variance 越大**。由于 $SST_{x}$ 是 $n$ 个离差平方的累加，较小的样本量通常意味着较小的分母，从而放大方差 。
3. **Explanatory variable x 的变异性 SSTx​ 越低，估计量的 Variance 越大**。如果样本中所有人的受教育年限都非常接近，我们就很难捕捉到教育对工资的真实边际影响。$x$ 的取值散得越开，我们的估计就越确凿 。

### 估算 Error Variance 与 Standard Errors

在真实的计量经济学应用中，总体的真实 Error variance $\sigma^{2}$ 是永远无法直接观测到的，我们必须使用手中的样本数据来估算它。一个直观的学术思路是用样本 Residuals 的方差来替代。但是，如果直接除以样本量 $n$，会得到一个有偏的估计 。
为了获取 Unbiased estimate，我们需要进行统计学上的自由度调整。定理 2.3 给出了无偏的 Error variance 估计公式：

$$
\hat{\sigma}^{2}=\frac{1}{n-2}\sum_{i=1}^{n}\hat{u}_{i}^{2}
$$

这里的分母是 $n-2$ 具有严格的代数依据：因为在计算 Residuals 之前，我们已经利用现有的样本数据估算出了两个回归系数（$\hat{\beta}_{0}$ 和 $\hat{\beta}_{1}$），这消耗了两个信息自由度 。
最后一步，我们将未知的总体 $\sigma^{2}$ 替换为我们刚刚算出的估计量 $\hat{\sigma}^{2}$，再对其开平方，就得到了回归系数极其重要的测度指标 Standard errors（标准误）：

$$
se(\hat{\beta}_{1})=\frac{\hat{\sigma}}{\sqrt{SST_{x}}}
$$

Standard errors 严格衡量了我们对回归系数估计的精确度 。在后续的计量经济学推演中，它是构建 Confidence intervals（置信区间）以及进行 Hypothesis testing（假设检验）的绝对基石。

## 总结

### 一、 Ordinary Least Squares 估计量的代数性质

在任何给定的数据样本中， Ordinary Least Squares 估计出的参数必然严格满足以下三个特征，这在后续的代数推演与证明中非常重要 ：

1. 样本 Residuals 的总和必定为零，即 $\sum_{i=1}^{n}\hat{u}_{i}=0$。
2. Explanatory variable 与 Residuals 的样本协方差为零，即 $\sum_{i=1}^{n}x_{i}\hat{u}_{i}=0$。
3. 样本坐标的均值点必定落在拟合的回归线上，即 $\overline{y}=\hat{\beta}_{0}+\hat{\beta}_{1}\overline{x}$。

### 二、 Causal Effect 与核心识别假设

经济学家通常关心因果关系（ Causal Effect ） 。为了赋予回归系数真正的因果解释力，我们必须保证在改变 Independent variable 时，隐藏在 Error term 中的其他所有因素保持不变，即满足 $\frac{\Delta u}{\Delta x}=0$。这在统计学上被严谨地表述为条件均值独立假设，也就是 $E(u|x)=0$。

### 三、 Goodness-of-Fit 与因果性的界限

在评估模型时， R-squared 的取值在 0 和 1 之间，它表达的是模型的解释力度 。学术研究中必须严格遵守的准则是，仅仅依靠数据的相关性与拟合优度，不能用于证明变量之间存在真正的因果关系 。

### 四、 Estimators 的统计学性质

在满足既定的前四个计量经济学假设下， Ordinary Least Squares 的估计量是无偏估计（ Unbiased estimators ） 。这意味着经过无限次重复抽样，估计量的期望值会严格等于总体的真实参数。
此外，在引入同方差假设后，我们推导了估计量的方差。影响估计量 Variance 的因素有三个 ：

1. Sample size ，即样本量 $n$ 的大小。
2. Error term 的 Variance ，即 $u$ 的变异程度 。
3. Explanatory variable 的变异性，即 $x$ 的离散程度 。
