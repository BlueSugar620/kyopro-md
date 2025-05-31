# 概要

数列 $A, B$ に対して、以下のように数列 $C$ を定義します。ただし、 $A_0 = 0, B_0 = 0$ とします。

<img src="https://latex.codecogs.com/svg.image?\bg{white}&space;C_k=\sum_{\gcd(i,j)=k}A_i&space;B_j">

この $C$ を高速に計算します。

# 理論

数列から数列への関数 $\mathcal{F}$ を

<img src="https://latex.codecogs.com/svg.image?\bg{white}\mathcal{F}(A)=\Big\{\sum_{k|i}A_i\Big\}_k">

と定義します。

<img src="https://latex.codecogs.com/svg.image?\bg{white}\mathcal{F}(C)_i=\mathcal{F}(A)_i\times\mathcal{F}(B)_i">

が成り立ちます。よって、 $\mathcal{F}$ の逆変換が存在すれば $C$ を求めることができます。

# 問題例

- https://atcoder.jp/contests/abc206/tasks/abc206_e
	- 包除原理を用いると、  $\gcd(x, y) = 1$ なる $(x, y)$ の数え上げとなります。これは、 $A_i = 1_{l \le i \lt r}$ に対して $A$ と $A$ の GCD convolution によって求めることができます。