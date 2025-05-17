以下の値を求めます。

<img src="https://latex.codecogs.com/svg.image?\bg{white}\sum_{i=0}^{N}\sum_{j=0}^M&space;f(i)\oplus&space;g(j)">

このとき、次の式変形をします。ただし、 $f, g \lt 2^X$ とします。また、 $b(a, i)$ を $a$ の $i$ ビット目を取り出す関数とします。

<img src="https://latex.codecogs.com/svg.image?\bg{white}\begin{align}&\sum_{i=0}^{N}\sum_{j=0}^M&space;f(i)\oplus&space;g(j)\\&=\sum_i\sum_j\sum_{k=0}^X&space;b\big(f(i)\oplus&space;g(j),k\big)\times&space;2^k\\&=\sum_k\Big(\sum_i\sum_j&space;b\big(f(i)\oplus&space;g(j),k\big)\Big)\times&space;2^k\\&=\sum_k\Big(\sum_i&space;1_{b(f(i),k)=1}\times\sum_j&space;1_{b(g(j),k)=0}&plus;\sum_{i}1_{b(f(i),k)=0)}\times\sum_j&space;1_{b(g(j),k)=1}\Big)\times&space;2^k\end{align}
">

これは、 $i, j$ の総和部分を前計算することで、 $O(X(N + M))$ で求めることができます。
$f = g$ のときは、 $0 \le i \lt j \lt N$ のように総和を取る範囲が変わっても $i = j$ が必ず $0$ になることにより $\div 2$ で求めることができます。
```Rust
fn xor_2d_sum(f: &[u64], g: &[u64]) -> u64 {
	let n = f.len();
	let m = g.len();

	let mut cnt_f = vec![0u64; 64];
	let mut cnt_g = vec![0u64; 64];
	for (k, cnt_f) in cnt_f.iter_mut().enumerate() {
		for f in f {
			if (f >> k) & 1 == 1 {
				*cnt_f += 1;
			}
		}
	}
	for (k, cnt_g) in cnt_g.iter_mut().enumerate() {
		for g in g {
			if (g >> k) & 1 == 1 {
				*cnt_g += 1;
			}
		}
	}

	(0..64)
		.map(|k| 
			(cnt_f[k] * (m as u64 - cnt_g[k]) + (n as u64 - cnt_f[k]) * cnt_g[k]) 
			* (1 << k)
		)
		.sum::<u64>()
}
```

## 問題例
- https://atcoder.jp/contests/abc201/tasks/abc201_e
	- 総和の形に持っていくまでが難しいです。
