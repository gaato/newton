---
theme: bricks
background: https://source.unsplash.com/collection/94734566/1920x1080
layout: cover
title: Newton の前進・後退差分公式
css: tailwind
---

# Newton の前進・後退差分公式

東京理科大学 理学部第一部 応用数学科 古谷岳人 (1420090)

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

## はじめに

5.3 節では差分商を用いた Newton 補間公式を扱った．Newton 補間公式は Lagrange 補間公式に比べて新たに点を追加するときの計算量が優れている．

なお，Newton 補間公式と Lagrange 補間公式の結果が同じであることは，$n$ 個の点を通る $n-1$ 次多項式は一意に定まることから分かる．

ここで，分割幅が等間隔の場合，すなわち $x_i = x_0 + ih$，$f_i = f(x_0 + ih)$ のとき，Newton の差分公式を単純化できることを紹介する．


---

## 前進差分 (forward difference)

$1$ 次の前進差分を次のように定義する．
$$
\Delta f(x) = f(x+h) - f(x).
$$
これを用いて $2$ 次の前進差分は
$$
\Delta^2 f(x) = \Delta (\Delta f(x)) = \Delta f(x+h) - \Delta f(x)
$$
と表せ，これを繰り返すと $m$ 次の前進差分は次のように再帰的に定義される．
$$
\Delta^m f(x) = \Delta (\Delta^{m-1} f(x)) = \Delta^{m-1} f(x+h) - \Delta^{m-1} f(x).
$$


---

## 差分商と前進差分の関係

分割幅が等間隔の場合の差分商は前で定義した前進差分を用いると次のように表される．

$$
f[x_0, \dots, x_m] = \frac{1}{m!h^m} \Delta^m f(x_0). \tag{1}
$$

<div v-click>
数学的帰納法により示す．

$m=1$ のとき，
$$
f[x_0, x_1] = \frac{1}{h} (f_1 - f_0) = \frac{1}{1!h} \Delta f(x_0)
$$
より成立．
</div>


---

## 差分商と前進差分の関係（続き）

$(1)$ が $m=n$ のとき成立すると仮定する．$x_{n+1}=x_0+(n+1)$ より，
$$
\begin{aligned}
f[x_0,\dots,x_{n+1}]
&= \frac{1}{(n+1)h} (f[x_1,\dots,x_{n+1}] - f[x_0,\dots,x_n]) \\
&= \frac{1}{(n+1)h} \left(\frac{1}{n!h^n} \Delta^n f(x_0+h) - \frac{1}{n!h^n} \Delta^n f(x_0) \right) \\
&= \frac{1}{(n+1)!h^{n+1}} \Delta^{n+1} f(x_0)
\end{aligned}
$$
となり，$m=n+1$ でも成立する．よって $(1)$ が示された．


---

## 二項係数

二項係数 $\binom{\alpha}{j}$ を次のように定義する．
$$
\begin{aligned}
\binom{\alpha}{j} &= \frac{\alpha (\alpha - 1) \dots (\alpha - j + 1)}{j!} \quad (j \ge 1) \\
\binom{\alpha}{0} &= 1.
\end{aligned}
$$

<span class="bg-yellow-300">$\alpha$ は自然数に限らないことに注意する．</span>

---

## Newton 差分商補間公式（復習）

$$
\begin{aligned}
p_0(x) &= f_0 \\
p_1(x) &= f_0 + (x-x_0) f[x_0,x_1] \\
p_2(x) &= f_0 + (x-x_0) f[x_0,x_1] + (x-x_0)(x-x_1)f[x_0,x_1,x_2] \\
&\vdots \\
p_n(x) &= f_0 + (x-x_0) f[x_0,x_1] + (x-x_0)(x-x_1)f[x_0,x_1,x_2] \\
& \qquad + \dots + (x-x_0)(x-x_1) \cdots (x-x_{n-1}) f[x_0,x_1,\dots,x_n].
\end{aligned}
$$


---

## Newton の前進差分補間公式

$(1)$ より，Newton 差分商補間公式は以下の Newton の前進差分公式になる．<span class="bg-yellow-300">$x_i = x_0 + ih$ に注意する．</span>

$$
\begin{aligned}
&p_n(x_0 + \alpha h) \\
&= f_0 + \alpha h f[x_0, x_1] + \alpha (\alpha - 1) h^2 f[x_0, x_1, x_2] + \dots + \alpha (\alpha - 1) \dots (\alpha - n + 1) h^n f[x_0,\dots,x_n] \\
&= \color{blue}{f_0 + \alpha \Delta f_0 + \frac{\alpha(\alpha - 1)}{2!} \Delta^2 f_0 + \dots + \frac{\alpha(\alpha-1)\dots(\alpha-n+1)}{n!}\Delta^nf_0} \\
&= \color{red}{\sum_{j=0}^n \binom{\alpha}{j} \Delta^j f_0}.
\end{aligned}
$$

<!--
離散版 Tayler 展開
-->

---

## 後退差分 (backward difference)

$1$ 次の後退差分を次のように定義する．
$$
\nabla f(x) = f(x) - f(x-h).
$$
これを用いて $2$ 次の後退差分は
$$
\nabla^2 f(x) = \nabla (\nabla f(x)) = \nabla f(x) - \nabla f(x-h)
$$
と表せ，これを繰り返すと $m$ 次の後退差分は次のように再帰的に定義される．
$$
\nabla^m f(x) = \nabla (\nabla^{m-1} f(x)) = \nabla^{m-1} f(x) - \nabla^{m-1} f(x-h).
$$

---

## 差分商と後退差分の関係

前進差分と同様に，分割幅が等間隔の場合の差分商は前で定義した後退差分を用いると次のように表される．

$$
f[x_n, \dots, x_{n-m}] = \frac{1}{m!h^m} \nabla^m f(x_n). \tag{2}
$$

前進差分の時と同様に数学的帰納法で示せるためここでは省略する．


---

## Newton の後退差分補間公式

前進差分と同様に後退差分でも補間公式を作ることができ，以下のようになる．<span class="bg-yellow-300">$x_i = x_n - ih$ に注意する．</span>

$$
\begin{aligned}
&p_n(x_n+\alpha h) \\
&= f_n + \alpha h f[x_n,x_{n-1}] + \alpha (\alpha + 1) h^2 f[x_n,x_{n-1},x_{n-2}] \\
&\qquad + \dots + \alpha (\alpha + 1) \cdots (\alpha + n - 1) h^n f[x_n, \dots, x_0] \\
&= \color{blue}{f_n + \alpha \nabla f_n + \frac{\alpha(\alpha + 1)}{2!} \nabla^2 f_n + \dots + \frac{\alpha(\alpha+1)\cdots(\alpha+n-1)}{n!}\nabla^nf_n} \\
&= f_n + (-1)(-\alpha)\nabla f_n+(-1)^2\frac{-\alpha(-\alpha-1)}{2!}\nabla^2f_n \\
&\qquad + \dots + (-1)^n\frac{-\alpha(-\alpha-1)\cdots(-\alpha-n+1)}{n!}\nabla^nf_n \\
&= \color{red}{\sum_{j=0}^n(-1)^j\binom{-\alpha}{j}\nabla^jf_n}
\end{aligned}

---

## 例

$(0,0),(1,2),(2,6),(3,8)$ を通る補間多項式を Newton の前進・後退差分公式で求める．

$$
\begin{array}{ccccc}
x_i & f_i & \text{1次} & \text{2次} & \text{3次} \\
0 & 0 \\
& & 2 \\
1 & 2 & & 2 \\
& & 4 & & -4 \\
2 & 6 & & -2 \\
& & 2 \\
3 & 8
\end{array}
$$

---

## 例（前進差分）

$$
\begin{array}{ccccc}
x_i & f_i & \text{1次} & \text{2次} & \text{3次} \\
0 & \red{0} \\
& & \red{2} \\
1 & 2 & & \red{2} \\
& & 4 & & \red{-4} \\
2 & 6 & & -2 \\
& & 2 \\
3 & 8
\end{array}
$$

$x=x_0+\alpha h$ とする．すなわち $\alpha = x$．

$$
\begin{aligned}
p_3(x)
&= \red{0} + \red{2}x+\frac{\red{2}}{2!}x(x-1)-\frac{\red{4}}{3!}x(x-1)(x-2) \\
&= \red{-\frac{1}{3}x+3x^2-\frac23x^3}.
\end{aligned}


---

## 例（後退差分）

$$
\begin{array}{ccccc}
x_i & f_i & \text{1次} & \text{2次} & \text{3次} \\
0 & 0 \\
& & 2 \\
1 & 2 & & 2 \\
& & 4 & & \red{-4} \\
2 & 6 & & \red{-2} \\
& & \red{2} \\
3 & \red{8}
\end{array}
$$

$x=x_n+\alpha h$ とする．すなわち $\alpha = x-3$．

$$
\begin{aligned}
p_3(x)
&= \red{8} + \red{2} (x-3) - \frac{\red{2}}{2!} (x-3)(x-2)-\frac{\red{4}}{3!}(x-3)(x-2)(x-1) \\
&= \red{-\frac{1}{3}x+3x^2-\frac23x^3}.
\end{aligned}


---

## 例（点の追加）

新たに $(4,10)$ という点を追加する．

$$
\begin{array}{cccccc}
x_i & f_i & \text{1次} & \text{2次} & \text{3次} & \color{blue}{\text{4次}} \\
0 & 0 \\
& & 2 \\
1 & 2 & & 2 \\
& & 4 & & -4 \\
2 & 6 & & -2 & & \color{blue}{6} \\
& & 2 & & \color{blue}{2} \\
3 & 8 & & \color{blue}{0} \\
& & \color{blue}{2}\\
\color{blue}{4} & \color{blue}{10}
\end{array}
$$

$$
\begin{aligned}
p_4(x)
&= p_3(x) + \frac{\color{blue}{6}}{4!}x(x-1)(x-2)(x-3) \\
&= \red{-\frac{11}{6}x+\frac{23}{4}x^2-\frac{13}{6}x^3+\frac{x^4}{4}}.
\end{aligned}
$$

---

## Desmos での実験

[Desmos](https://www.desmos.com/calculator/fstl9zcdhu?lang=ja) で実験した．

---

## 参考文献

陳子君・山本哲郎 . 英語で学ぶ数値解析 . コロナ社 , 2002

<!--
(1) の証明を逆向きにする
-->
