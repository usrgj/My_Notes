---
title: Markdown 语法
created: '2025-07-13T07:09:55.143Z'
modified: '2025-07-30T05:42:25.527Z'
---

Markdown 语法

[1数学](#1-数学)
[2锚点](#2-锚点)

## 1 数学
### 1 行内式与独立式
$x+y=1$
$$x+y=1$$

### 2 上下标
^上标  
_下标  
\\\\换行  
{}作括号
$$
x^2 + y_2 = x^{x_1+y} \\
x
$$

### 3 括号
$$
(1+1) \\
[1+1] \\
\{1+1\} 
$$

### 4 省略号
$$
1, 2, 3,\ldots,n 对齐逗号\\
1, 2*1, 3*1,\cdots, n对齐乘号
$$

### 5 分数
$$
\frac{1-x}{y+1}第一个括号为分子第二个为分母 \\
{x\over y}
$$

### 6 开方
$$
\sqrt[3]{27}
$$

### 7 向量
$$
\vec a \\
\vec {ab}
$$

### 8 极限
$$
\lim_{n \rightarrow + \infin} \frac{1}{n}
$$

### 9 求导
$$
y \prime = nx^{n-1}
$$

### 10 方程组
$$
y: \begin{cases} x+y = 1 \\
x - y = 0 \end{cases}

\begin{cases}

\end{cases}
$$

### 11 矩阵
$$
A = \left[ \begin{matrix}
1&2&3 \\
4&5&6 \\
7&8&9 \\
\end{matrix} \right]
\left[ \begin{matrix}

\end{matrix} \right]
$$

### 12 对数
$$
\log_24\\
\lg\\
\ln\\
$$

### 13 定积分
$$
\int \\
\iint \\
\iiint \\
\oint \\
$$

### 14 三角函数
$$
\bot \\
\angle \\
30^\circ \\
\sin \\
\cos \\
\tan\\
\cot \\
\sec \\
\csc \\
$$

### 15 集合
$$
\empty \\
\in \\
\notin\\
\supset \\
\supseteq\\
\bigcap \\
\bigcup \\
\bigvee \\
\bigwedge \\
$$

### 16 符号
$$
\because\\
\therefore\\
\not= \\
\approx \\
\leq \\
\geq \\
\times \\
\cdot \\
\pm\\
\div\\
\infin\\
\sum\\
\prod\\
\coprod\\
\uparrow\\
\downarrow\\
\leftarrow\\
\rightarrow\\
\overline{a+b+c}平均值\\
\sqrt1 \\
{1\over2} \\
() \\
\left(\sqrt1\right)加大括号 \\
\left.(\sqrt1\right)
$$

### 17 希腊字母
| 小写 LaTeX 符号 | 大写 LaTeX 符号 | 显示效果|
|----------------|----------------|----------------|
| `\alpha`|| α|
| `\beta`|| β|
| `\gamma`|| γ|
| `\delta`|| δ|
| `\pi`|| π|
| `\epsilon`| `\varepsilon`| ϵ, ε|
| `\zeta`|| ζ|
| `\eta`|| η|
| `\theta`| `\Theta`| θ, Θ|
| `\vartheta`|| ϑ|
| `\phi`|| ϕ|
| `\psi`| `\Psi`| ψ, Ψ|
| `\omega`| `\Omega`| ω, Ω|
| `\rho`|| ρ|
| `\sigma`|| σ|
| `\xi`|| ξ|
| `\mu`|| μ|
| `\partial`|| ∂|

## 2 锚点
部分解析器能自动为标题生成锚点，因此链接标题
[1. 算法介绍](#1-算法介绍)  
空格要用```-``` 替代
``` ```  
[1.1).线性表](#1-线性表)
```(``` ```)``` ```.``` ```,``` 可能被忽略  
[③左闭右开写法 \[left, right)](#③-左闭右开写法-left-right)
[④左开右闭写法 (left, right\]](#④-左开右闭写法-left-right)
标题中的单个```[``` ```]``` 要转义  
[3. AI的使用](#3-ai的使用)
[4. 关键步骤所用的 prompt](#4-关键步骤所用的-prompt)
使用小写字母
### 忽略英文标点
`:` `=`

###### 引用
> look this

###### 图片
![风景照](https://example.com/scenery.jpg "美丽的山水风景")

###### 分割线（上下空行）

***

###### 复选框
- [ ] 



