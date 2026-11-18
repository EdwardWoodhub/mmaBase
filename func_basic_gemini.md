这份速查表精选了 Mathematica（Wolfram 语言）最核心的 **100 个高频内置函数**，按日常编程、符号推导、数值计算与科学可视化的实际工作流分为 8 大模块。

---

### 1. 列表生成与结构操作（16 个）

Wolfram 语言的核心哲学是“万物皆表达式（列表）”，熟练掌握列表操作可替代绝大多数循环。

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `Table` | 生成列表或数组 | `Table[i^2, {i, 1, 5}]` |
| `Range` | 生成等差数列 | `Range[0, 10, 2]` |
| `ConstantArray` | 生成常数数组 | `ConstantArray[0, {2, 3}]` |
| `Length` | 获取列表第一层长度 | `Length[{a, b, c}]` |
| `Dimensions` | 获取多维数组维度 | `Dimensions[{{1, 2}, {3, 4}}]` |
| `Part` (`[[...]]`) | 索引提取元素（下标从 1 开始） | `list[[1, -1]]` |
| `First` / `Last` | 提取首元素 / 末元素 | `First[{10, 20, 30}]` |
| `Take` / `Drop` | 截取前 n 个 / 丢弃前 n 个 | `Take[list, {2, 4}]` |
| `Append` / `Prepend` | 末尾追加 / 开头插入 | `Append[{1, 2}, 3]` |
| `Join` | 合并多个同级列表 | `Join[{1, 2}, {3, 4}]` |
| `Flatten` | 展平嵌套列表 | `Flatten[{{1, 2}, {3}}, 1]` |
| `Partition` | 按指定长度切分列表 | `Partition[Range[6], 2]` |
| `Transpose` | 矩阵或嵌套列表转置 | `Transpose[{{1, 2}, {3, 4}}]` |
| `Tuples` | 生成笛卡尔积/全排列组合 | `Tuples[{0, 1}, 3]` |
| `Sort` / `SortBy` | 排序 / 按指定函数排序 | `SortBy[list, Last]` |
| `DeleteDuplicates` | 去除重复元素 | `DeleteDuplicates[{1, 2, 1}]` |

---

### 2. 函数式编程与规则替换（14 个）

这是摆脱过程式 `For` 循环、写出地道且高效 Wolfram 代码的核心。

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `Map` (`/@`) | 将函数映射到列表每个元素 | `Sin /@ {0, Pi/2, Pi}` |
| `Apply` (`@@`) | 替换表达式头部（剥去外层括号） | `Plus @@ {1, 2, 3}` |
| `MapThread` | 多列表对应位置同步映射 | `MapThread[f, {{a, b}, {1, 2}}]` |
| `Function` (`#`, `&`) | 定义匿名纯函数 | `(#^2 + 1) & /@ {1, 2, 3}` |
| `Nest` / `NestList` | 嵌套迭代计算（输出终值/过程） | `NestList[Cos, 1.0, 5]` |
| `Fold` / `FoldList` | 带双参数的累积迭代 | `FoldList[Plus, 0, {1, 2, 3}]` |
| `Select` | 按条件筛选列表元素 | `Select[Range[10], EvenQ]` |
| `Cases` | 按模式匹配提取元素 | `Cases[{1, a, 2, b}, _Integer]` |
| `Count` | 统计符合模式的元素个数 | `Count[list, _?Positive]` |
| `Position` | 查找匹配元素的索引位置 | `Position[{a, b, a}, a]` |
| `Rule` (`->`) | 定义替换规则 | `x -> 5` |
| `RuleDelayed` (`:>`) | 延迟替换规则（右侧替换时求值） | `x_ :> RandomReal[]` |
| `ReplaceAll` (`/.`) | 全局应用替换规则 | `x^2 + y /. {x -> 2, y -> 3}` |
| `ReplaceRepeated` (`//.`) | 反复应用规则直到结果不再变化 | `expr //. rules` |

---

### 3. 作用域、条件与流程控制（10 个）

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `Module` | 词法作用域（创建局部符号变量） | `Module[{x = 1}, x + 2]` |
| `Block` | 动态作用域（临时重定义全局符号） | `Block[{x = 5}, x^2]` |
| `With` | 局部常量替换（直接嵌入值，无开销） | `With[{a = 2}, a*x + 1]` |
| `If` | 条件分支判断 | `If[x > 0, "Pos", "NonPos"]` |
| `Which` | 多分支条件判断（类似 else if） | `Which[x < 0, -1, x == 0, 0, True, 1]` |
| `Switch` | 模式匹配多分支选择 | `Switch[val, 1, "A", 2, "B", _, "Other"]` |
| `Do` | 执行重复操作（无返回值） | `Do[Print[i], {i, 3}]` |
| `While` | 条件循环 | `While[n < 5, n++]` |
| `Evaluate` | 强制在 `HoldAll` 函数内部提前求值 | `Plot[Evaluate[Table[a x, {a, 3}]], {x, 0, 1}]` |
| `Timing` / `AbsoluteTiming` | 测量代码 CPU 时间 / 真实耗时 | `AbsoluteTiming[Integrate[Sin[x]^10, x]]` |

---

### 4. 代数化简与符号变换（12 个）

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `Simplify` | 通用代数化简 | `Simplify[Sin[x]^2 + Cos[x]^2]` |
| `FullSimplify` | 深度化简（调用特殊函数恒等式） | `FullSimplify[Gamma[x + 1]/Gamma[x]]` |
| `Assuming` | 在指定假设条件下化简或计算 | `Assuming[x > 0, Simplify[Sqrt[x^2]]]` |
| `Expand` | 展开多项式乘积与乘方 | `Expand[(x + y)^3]` |
| `Factor` | 多项式因式分解 | `Factor[x^2 - 1]` |
| `Together` / `Apart` | 通分合并 / 部分分式展开 | `Apart[1/(x^2 - 1)]` |
| `Collect` | 按指定变量的幂次合并同类项 | `Collect[a x + b x + c, x]` |
| `TrigExpand` / `TrigReduce` | 三角函数展开 / 积化和差降幂 | `TrigReduce[Sin[x]^2]` |
| `ComplexExpand` | 假设变量为实数展开复数表达式 | `ComplexExpand[Exp[I x]]` |
| `Re` / `Im` | 提取实部 / 虚部 | `Re[3 + 4 I]` |
| `Conjugate` / `Abs` / `Arg` | 共轭复数 / 模长 / 幅角 | `Conjugate[x + I y]` |
| `Coefficient` | 提取多项式中特定次幂的系数 | `Coefficient[3 x^2 + 2 x + 1, x, 2]` |

---

### 5. 方程求解与微积分（12 个）

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `Solve` | 符号求解代数方程（组） | `Solve[x^2 - 3 x + 2 == 0, x]` |
| `NSolve` | 数值求解多项式或代数方程（组） | `NSolve[x^5 - x + 1 == 0, x]` |
| `FindRoot` | 局部数值求根（牛顿法，需初值） | `FindRoot[Cos[x] == x, {x, 0.5}]` |
| `Reduce` | 完整逻辑化简求解（含不等式与条件） | `Reduce[a x + b == 0, x]` |
| `D` | 求偏导数或高阶导数 | `D[Sin[x y], {x, 2}]` |
| `Integrate` | 不定积分与定积分 | `Integrate[Exp[-x^2], {x, -Infinity, Infinity}]` |
| `NIntegrate` | 高精度数值积分 | `NIntegrate[Sin[Sin[x]], {x, 0, 2}]` |
| `Limit` | 求极限 | `Limit[Sin[x]/x, x -> 0]` |
| `Series` | 泰勒/洛朗级数展开 | `Series[Exp[x], {x, 0, 4}]` |
| `Normal` | 截断级数高阶无穷小，转为普通表达式 | `Normal[Series[Sin[x], {x, 0, 5}]]` |
| `DSolve` | 符号求解常/偏微分方程 | `DSolve[y'[x] == k y[x], y[x], x]` |
| `NDSolve` | 数值求解微分方程（返回插值函数） | `NDSolve[{y'[x] == y[x], y[0] == 1}, y, {x, 0, 2}]` |

---

### 6. 线性代数与矩阵运算（10 个）

*注：在 Mathematica 中，向量是一维列表，矩阵是二维嵌套列表。*

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `Dot` (`.`) | 矩阵乘法 / 向量内积（非逐元素乘） | `matA . matB` |
| `Cross` | 三维向量叉乘 | `Cross[{1, 0, 0}, {0, 1, 0}]` |
| `IdentityMatrix` | 生成 $n \times n$ 单位矩阵 | `IdentityMatrix[3]` |
| `DiagonalMatrix` | 生成对角矩阵 | `DiagonalMatrix[{1, 2, 3}]` |
| `Inverse` | 矩阵求逆 | `Inverse[{{1, 2}, {3, 4}}]` |
| `Det` | 计算矩阵行列式 | `Det[{{1, 2}, {3, 4}}]` |
| `Tr` | 计算矩阵的迹（对角线元素之和） | `Tr[mat]` |
| `Eigenvalues` / `Eigenvectors` | 求特征值 / 特征向量 | `Eigensystem[mat]` |
| `LinearSolve` | 高效求解线性方程组 $A \cdot x = b$ | `LinearSolve[A, b]` |
| `Norm` / `Normalize` | 计算向量或矩阵范数 / 向量归一化 | `Normalize[{3, 4}]` |

---

### 7. 数值计算、统计与拟合（12 个）

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `N` | 将精确符号转为指定精度的浮点数 | `N[Pi, 30]` |
| `Chop` | 将绝对值极小（默认 $<10^{-10}$）的数归零 | `Chop[1.0 + 10^-15 I]` |
| `FindMinimum` / `FindMaximum` | 数值寻找局部极小值 / 极大值 | `FindMinimum[x^2 + 2 x, {x, 0}]` |
| `Minimize` / `Maximize` | 全局符号或数值最优化 | `Minimize[{x^2 + y^2, x + y == 1}, {x, y}]` |
| `Interpolation` | 对离散数据构建连续插值函数 | `f = Interpolation[data]; f[1.5]` |
| `Fit` / `LinearModelFit` | 线性最小二乘拟合 | `LinearModelFit[data, x, x]` |
| `FindFit` / `NonlinearModelFit` | 非线性函数曲线拟合 | `NonlinearModelFit[data, a Exp[-b x], {a, b}, x]` |
| `Fourier` / `InverseFourier` | 快速离散傅里叶变换（FFT） | `Fourier[signal]` |
| `Mean` / `Median` | 均值 / 中位数 | `Mean[{1, 2, 3, 4}]` |
| `StandardDeviation` / `Variance` | 标准差 / 方差 | `StandardDeviation[data]` |
| `RandomReal` / `RandomInteger` | 生成均匀分布随机实数 / 整数 | `RandomReal[{-1, 1}, {100}]` |
| `Total` / `Accumulate` | 列表求和 / 累加序列 | `Total[Range[100]]` |

---

### 8. 数据可视化与文件 I/O（14 个）

| 函数 | 功能说明 | 语法示例 |
| --- | --- | --- |
| `Plot` | 绘制一元函数二维曲线 | `Plot[Sin[x], {x, 0, 2 Pi}]` |
| `ListPlot` | 绘制离散数据散点图 | `ListPlot[data]` |
| `ListLinePlot` | 绘制离散数据折线图 | `ListLinePlot[data, PlotRange -> All]` |
| `ParametricPlot` | 绘制二维参数方程曲线 | `ParametricPlot[{Cos[t], Sin[t]}, {t, 0, 2 Pi}]` |
| `Plot3D` | 绘制二元函数三维曲面 | `Plot3D[Sin[x y], {x, 0, 3}, {y, 0, 3}]` |
| `ContourPlot` | 绘制等高线图或隐函数曲线 | `ContourPlot[x^2 + y^2 == 1, {x, -2, 2}, {y, -2, 2}]` |
| `DensityPlot` | 绘制二维标量场热力图 | `DensityPlot[Sin[x] Cos[y], {x, -3, 3}, {y, -3, 3}]` |
| `Show` | 叠加合并多个图形对象 | `Show[plot1, plot2]` |
| `GraphicsGrid` | 将多个图形按网格排版 | `GraphicsGrid[{{p1, p2}, {p3, p4}}]` |
| `Manipulate` | 创建带交互滑块的动态演示界面 | `Manipulate[Plot[Sin[k x], {x, 0, 6}], {k, 1, 5}]` |
| `Import` / `Export` | 导入 / 导出 CSV、MAT、JSON、图像等 | `Export["fig.png", plot, ImageResolution -> 600]` |
| `ToString` / `StringJoin` (`<>`) | 转为字符串 / 字符串拼接 | `"Result: " <> ToString[val]` |
| `SetDirectory` / `NotebookDirectory` | 设置工作目录 / 获取当前笔记本路径 | `SetDirectory[NotebookDirectory[]]` |
| `Clear` / `ClearAll` | 清除变量定义 / 彻底清除定义与属性 | `ClearAll["Global`*"]` |
