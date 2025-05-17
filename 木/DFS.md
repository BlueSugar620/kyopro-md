$V, E$ を木とし、親を返す関数を $p$ , 子の集合を返す関数を $C$ とします。 
根 $r$ からの行きがけと帰りがけの時間を各頂点に対して記録します。それらを返す関数を $in, out$ とします。

# 子の判定

<img src="https://latex.codecogs.com/svg.image?\bg{white}v\in&space;C(u)\iff&space;in(u)<in(v)<out(v)<out(u)">
が成り立ちます。

## 問題例
- https://atcoder.jp/contests/abc202/tasks/abc202_e
	- $in$ を深さごとに分けて、二分探索で個数を求める問題。