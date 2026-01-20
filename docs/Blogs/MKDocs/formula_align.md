# MKdocs KaTeX 跨行公式对齐

本人使用 [KaTeX](https://katex.org/) 来支持 [mkdocs-material 对公式的渲染时](https://squidfunk.github.io/mkdocs-material/reference/math/#katex), 发现跨行公式很难对齐. 经过一番 debug, 同时查阅其他使用者 github repo 中的编写方式, 总结出了一些妥协规则. 

## 失败案例

```LaTeX
$$
\begin{aligned} 
\| \omega_k \|^2 =& \| \omega^* \|^2 \cdot \| \omega_k \|^2 \geq \| \omega^{*\top} \omega_{k} \|^2 \\ 
=& \left\| \omega^{*\top} \cdot \sum^{K}_{k=1} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2  \\ 
=& \left\| \sum^{K}_{k=1} \omega^{*\top} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2 .  
\end{aligned}
$$
```

渲染结果: 

$$
\begin{aligned} 
\| \omega_k \|^2 =& \| \omega^* \|^2 \cdot \| \omega_k \|^2 \geq \| \omega^{*\top} \omega_{k} \|^2 \\ 
=& \left\| \omega^{*\top} \cdot \sum^{K}_{k=1} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2  \\ 
=& \left\| \sum^{K}_{k=1} \omega^{*\top} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2 .  
\end{aligned}
$$

## 注意点 

- 应当使用 `$ $` 而非跨行居中的 `$$ $$` 来包裹 `\begin{aligned} \end{aligned}`. 
- 整个公式环境中都不应该换行. 

## 成功案例

```LaTeX
$\begin{aligned} \| \omega_k \|^2 =& \| \omega^* \|^2 \cdot \| \omega_k \|^2 \geq \| \omega^{*\top} \omega_{k} \|^2 \\ =& \left\| \omega^{*\top} \cdot \sum^{K}_{k=1} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2  \\ =& \left\| \sum^{K}_{k=1} \omega^{*\top} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2 .  \end{aligned}$
```

渲染结果: 

$\begin{aligned} \| \omega_k \|^2 =& \| \omega^* \|^2 \cdot \| \omega_k \|^2 \geq \| \omega^{*\top} \omega_{k} \|^2 \\ =& \left\| \omega^{*\top} \cdot \sum^{K}_{k=1} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2  \\ =& \left\| \sum^{K}_{k=1} \omega^{*\top} \left[ \phi(x^{(n)}, y^{(n)}) - \phi(x^{(n)},y) \right] \right\|^2 .  \end{aligned}$

------

如何呢? 真是让人心烦. 不得不做出妥协.

