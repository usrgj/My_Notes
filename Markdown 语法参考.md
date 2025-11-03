---
title: Markdown 语法参考
created: '2025-07-13T07:09:55.143Z'
modified: '2025-10-28T10:03:28.489Z'
---

# Markdown 语法参考

<style>

  span>* {
            line-height: 40px;
            margin-bottomx !important
        }
  

</style>

## 数学公式

### 1. 行内式与独立式
| 语法 | 效果 |
|------|------|
| `$x+y=1$` 行内式| $x+y=1$ |
| `$$x+y=1$$` 独立式| $$x+y=1$$ |

### 2. 上下标
| 语法 | 效果 |
|------|------|
| `x^2 + y_2` | $x^2 + y_2$ |
| `x^{x_1+y}` | $x^{x_1+y}$ |
| `\\` 换行 | 公式内换行 |

### 3. 括号
| 语法 | 效果 |
|------|------|
| `(1+1)` | $(1+1)$ |
| `[1+1]` | $[1+1]$ |
| `\{1+1\}` | $\{1+1\}$ |
| `\left(\frac{1}{2}\right)` | $\left(\frac{1}{2}\right)$ |

### 4. 省略号
| 语法 | 效果 |
|------|------|
| `\ldots` | $1,\ldots,n$ |
| `\cdots` | $1+\cdots+n$ |
| `\ddots` | $\ddots$ |
| `\vdots` | $\vdots$ |

### 5. 分数
| 语法 | 效果 |
|------|------|
| `\frac{1-x}{y+1}` | $\frac{1-x}{y+1}$ |
| `{x\over y}` | ${x\over y}$ |

### 6. 开方
| 语法 | 效果 |
|------|------|
| `\sqrt{9}` | $\sqrt{9}$ |
| `\sqrt[3]{27}` | $\sqrt[3]{27}$ |

### 7. 向量
| 语法 | 效果 |
|------|------|
| `\vec a` | $\vec a$ |
| `\vec{ab}` | $\vec{ab}$ |

### 8. 极限
| 语法 | 效果 |
|------|------|
| `\lim_{n\to\infty}` | $\lim_{n\to\infty}$ |

### 9. 求导
| 语法 | 效果 |
|------|------|
| `y\prime` | $y\prime$ |
| `\frac{dy}{dx}` | $\frac{dy}{dx}$ |
| `\frac{d^2y}{dx^2}` | $\frac{d^2y}{dx^2}$ |
| `\frac{\partial f}{\partial x}` | $\frac{\partial f}{\partial x}$ |
|`\dot s`|$\dot s$|

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

\end{matrix} \right]\\
\det A\\

\begin{vmatrix}
a & b \\
c & d 
\end{vmatrix}\\

\begin{bmatrix}
  1 & 2 \\
  3 & 4
  \end{bmatrix}

\\
\begin{pmatrix}
  1 & 2 \\
  3 & 4
\end{pmatrix}
$$


### 12. 对数
| 语法 | 效果 |
|------|------|
| `\log_2 4` | $\log_2 4$ |
| `\lg` | $\lg$ |
| `\ln` | $\ln$ |

### 13. 积分
| 语法 | 效果 |
|------|------|
| `\int` | $\int$ |
| `\iint` | $\iint$ |
| `\iiint` | $\iiint$ |
| `\oint` | $\oint$ |

### 14. 三角函数
| 语法 | 效果 |
|------|------|
| `\sin` | $\sin$ |
| `\cos` | $\cos$ |
| `\tan` | $\tan$ |
| `30^\circ` | $30^\circ$ |

### 15. 集合
| 语法 | 效果 |
|------|------|
| `\in` | $\in$ |
| `\notin` | $\notin$ |
| `\bigcup` | $\bigcup$ |
| `\bigcap` | $\bigcap$ |

### 16. 常用符号
| LaTeX 写法| 效果|
|---------------------|-------------------|
| `\tilde{A}`| $\tilde{A}$|
| `\because`| $\because$|
| `\therefore`| $\therefore$|
| `\not=`| $\not=$|
| `\approx`| $\approx$|
| `\leq`| $\leq$|
| `\geq`| $\geq$|
| `\times`| $\times$|
| `\cdot`| $\cdot$|
| `\pm`| $\pm$|
| `\div`| $\div$|
| `\infin`| $\infin$|
| `\sum`| $\sum$|
| `\prod`| $\prod$|
| `\coprod`| $\coprod$|
| `\uparrow`| $\uparrow$|
| `\downarrow`| $\downarrow$|
| `\leftarrow`| $\leftarrow$|
| `\rightarrow`| $\rightarrow$|
| `\overline{a+b+c}`| $\overline{a+b+c}$ |
| `\sqrt{1}`| $\sqrt{1}$|
| `{1\over2}`| ${1\over2}$|
| `()`| $()$|
| `\left(\sqrt{1}\right)` | $\left(\sqrt{1}\right)$ |
| `\left.(\sqrt{1}\right)` | $\left.(\sqrt{1}\right)$ |
| `\overline{z}`| $\overline{z}$|
| `\underset{\sim}{r}` | $\underset{\sim}{r}$ |
| `\rightleftarrows` |$\rightleftarrows$|
| `\leftrightarrows` |$\leftrightarrows$|
| `\leftrightarrow` |$\leftrightarrow$|
| `\Leftrightarrow` |$\Leftrightarrow$|
| `\leftrightharpoons` |$\leftrightharpoons$|
| `\rightleftharpoons` |$\rightleftharpoons$|
|`\forall`|$\forall$|
|`\exists`|$\exists$|

### 17. 希腊字母表
| 字母名称| 大写 LaTeX | 大写显示 | 小写 LaTeX | 小写显示|
|----------------|------------|----------|------------|--------------|
| Alpha| `A`| $A$| `\alpha`| $\alpha$|
| Beta| `B`| $B$| `\beta`| $\beta$|
| Gamma| `\Gamma`| $\Gamma$ | `\gamma`| $\gamma$|
| Delta| `\Delta`| $\Delta$ | `\delta`| $\delta$|
| Epsilon| `E`| $E$| `\epsilon` | $\epsilon$|
| Zeta| `Z`| $Z$| `\zeta`| $\zeta$|
| Eta| `H`| $H$| `\eta`| $\eta$|
| Theta| `\Theta`| $\Theta$ | `\theta`| $\theta$|
| Iota| `I`| $I$| `\iota`| $\iota$|
| Kappa| `K`| $K$| `\kappa`| $\kappa$|
| Lambda| `\Lambda`| $\Lambda$| `\lambda`| $\lambda$|
| Mu| `M`| $M$| `\mu`| $\mu$|
| Nu| `N`| $N$| `\nu`| $\nu$|
| Xi| `\Xi`| $\Xi$| `\xi`| $\xi$|
| Omicron| `O`| $O$| `\omicron` | $\omicron$|
| Pi| `\Pi`| $\Pi$| `\pi`| $\pi$|
| Rho| `P`| $P$| `\rho`| $\rho$|
| Sigma| `\Sigma`| $\Sigma$ | `\sigma`| $\sigma$|
| Tau| `T`| $T$| `\tau`| $\tau$|
| Upsilon| `\Upsilon` | $\Upsilon$| `\upsilon`| $\upsilon$|
| Phi| `\Phi`| $\Phi$| `\phi`| $\phi$|
| Chi| `X`| $X$| `\chi`| $\chi$|
| Psi| `\Psi`| $\Psi$| `\psi`| $\psi$|
| Omega| `\Omega`| $\Omega$ | `\omega`| $\omega$|

### 18. 几何符号
|写法|效果|
|---|---|
|`\perp`|$\perp$|
|`\parallel`|$\parallel$|
|`\angle`|$\angle$|
|``||
|``||

## 其他Markdown语法

### 锚点链接
| 语法 | 效果 |
|------|------|
| `[1. 算法介绍](#1-算法介绍)` | [1. 算法介绍](#1-算法介绍) |
| `[③左闭右开写法](#③-左闭右开写法-left-right)` | [③左闭右开写法](#③-左闭右开写法-left-right) |

### 引用
`> 引用内容`
> 引用

### 图片
| 语法 | 效果 |
|------|------|
| `![alt，if fail to load img](img url)` | 显示图片 |

### 分割线
`<br>***<br>`

***

### 复选框
| 语法 | 效果 |
|------|------|
| `- [ ] 任务` |  |
- [ ] 任务

