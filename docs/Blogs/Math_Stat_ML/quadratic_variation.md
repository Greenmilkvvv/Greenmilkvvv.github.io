# 二次变分

在金融数学中, **二次变分 (Quadratic Variation)**是一个重要的概念, 是随机过程在给定时间点的波动性,可以用来描述随机过程的波动性。

------

## Why 二次变分?

**定义** (Adatptivity,  可实时观测性,  $\mathcal{F} (t) \text{-measurable}$). 对于一个随机过程 $(X_t)_{t\ge 0}$ 和某个 **信息流 (filtration)** $(\mathcal{F_t})_{t \geq 0}$,  若到时刻 $t$ 为止,  你能拿到的全部信息 $\mathcal{F_t}$ 已经足以确定 $X_t$ 的值, 则称 $X(t)$ 为 **可实时观测** 的. 严格地, 

$$ 
\forall~t, ~ X_t\ \text{是}\ \mathcal {F}(t)\text{-measurable},  
$$

则称其为 **可实时观测** 的. 

------

对于积分

$$
\int^T_0 \Delta(t) \mathrm{d} W(t) ,  
$$

其中 $T$ 为时间 (恒正),   $W(t)$ 为布朗运动. 对于被积函数 $\Delta (t)$ 其金融学意义为 $t$ 时刻的\textbf{持仓},   因而可以通过随机过程来刻画. 显然 $\Delta(t)$ 是\textbf{可实时观测}的.

**然而**,  在处理这个积分时,  由于

- 布朗运动 $W(t)$ 的**增量**, **独立于**过往信息集合 $\mathcal{F}(t)$, 
- 持仓 $\Delta(t)$ 完全 **依赖于** $\mathcal{F}(t)$.

可以理解成: $W(t)$ 在任意小的区间中都**无限抖动**, 恼人的随机性导致**导数处处不存在**. 故这一积分**在经典微积分的逻辑下没有意义**.

## 二次变分

如前所述, 随机性导致了微积分的定义出现问题. 既然 "瞬时斜率" 不存在，我们或许可以尝试更粗糙的度量, 即**只看增量平方, 以此来观察随机微积分的收敛性**, 应运而生的是二次变分这一数学工具：

------

**定义** (二次变分). 设 $X=(X_t)_{t \ge 0}$ 为定义于滤子概率空间 $(\Omega, \mathcal F, (\mathcal F_t)_{t\ge 0}, \mathbb P)$ 上的连续半鞅. 对任意有限分割

$$ 
\pi_n=\{0=t_0^{(n)}<t_1^{(n)}<\dots<t_{k_n}^{(n)}=t\} 
\quad\text{且} 
\quad |\pi_n|=\max_i|t_{i}^{(n)}-t_{i-1}^{(n)}|\to 0, 
$$

称随机变量
 
$$
[X]_t:=\lim_{n\to\infty}\sum_{i=1}^{k_n}
\left (X_{t_i^{(n)}}-X_{t_{i-1}^{(n)}} \right)^2
\quad(\text{依概率收敛})
$$

为 $X$ 在区间 $[0, t]$ 上的**二次变分**. 

------

------

**命题** (二次变分的性质). 二次变分具有以下基本性质：

-  **适应性**：$[X]_t$ 是 $\mathcal F_t$-可测的, 且关于 $t$ 非降、右连续. 

-  **双线性**：对任意两个连续半鞅 $X, Y$, 存在唯一的协变分（covariation）
   
$$
[X, Y]_t:=\frac{1}{4}\left([X+Y]_t-[X-Y]_t\right), 
$$

使得 $(X, Y)\mapsto [X, Y]_t$ 为对称双线性型. 

-  **Ito 等距核心**：对适应局部有界可料过程 $H$, 有
   
$$
\mathbb E\biggl[\Bigl(\int_0^t H_s\, dX_s\Bigr)^2\biggr]
=\mathbb E\biggl[\int_0^t H_s^2\, d[X]_s\biggr], 
$$

随机积分能量守恒. 

------

## Python 实现

以下是一个简单的示例，展示如何使用 `numpy` 来模拟二次变分：

```python
import numpy as np

def f(x):
    # 定义被积分的函数，例如 f(x) = x^2
    return x**2

def quad(f, a, b, n=100):
    # 二次变分的实现
    h = (b - a) / n  # 步长
    x = np.linspace(a, b, n + 1)  # 生成 n+1 个点
    y = f(x)
    
    # 计算积分的近似值
    integral = h * (y[0] + y[-1]) / 2
    for i in range(1, n):
        integral += h * (y[i] + y[i + 1]) / 2
    
    return integral

# 测试函数
a = 0  # 积分下限
b = 1   # 积分上限
n = 100  # 分割数

result = quad(f, a, b, n)
print(f"The integral of f(x) = x^2 from {a} to {b} is approximately {result}")
```

在这个示例中：

- `f(x)` 是被积分的函数，这里我们使用 `f(x) = x^2` 作为示例。
- `quad` 函数实现了二次变分算法，它接受被积分的函数 `f`，积分的上下限 `a` 和下限 `b`，以及分割数 `n`。
- `h` 是步长，计算为 `(b - a) / n`。
- `x` 是分割点的数组，`y` 是这些点上的函数值。
- 积分的近似值是通过将每个小区间上的函数值乘以步长 `h` 并求和得到的。

