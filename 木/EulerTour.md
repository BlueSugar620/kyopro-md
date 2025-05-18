$V, E$ を木とし、親を返す関数を $p$ , 子の集合を返す関数を $C$ とします。 
根 $r$ からの行きがけと帰りがけの時間を各頂点に対して記録します。それらを返す関数を $in, out$ とします。
```Rust
let mut in_time = vec![0; n];
let mut out_time = vec![0; n];
dfs(
	根,
	初期時間,
	隣接リスト,
	&mut in_time,
	&mut out_time,
);

fn dfs(
    i: usize,
    t: &mut usize,
    e: &Vec<Vec<usize>>,
    in_time: &mut [usize],
    out_time: &mut [usize],
) {
    in_time[i] = *t;
    *t += 1;
    for j in &e[i] {
        dfs(*j, t, e, in_time, out_time);
    }
    out_time[i] = *t;
    *t += 1;
}
```

# 子の判定

<img src="https://latex.codecogs.com/svg.image?\bg{white}v\in&space;C(u)\iff&space;in(u)<in(v)<out(v)<out(u)">
が成り立ちます。
# 部分木クエリ
Euler Tour Tree を使い区間クエリに帰着させることで、更新と取得を高速に行います。
# 問題例
- https://atcoder.jp/contests/abc202/tasks/abc202_e
	- $in$ を深さごとに分けて、二分探索で個数を求める問題。
- https://atcoder.jp/contests/abc406/tasks/abc406_f
	- 頂点加算、部分木総和クエリを行う問題。
	- EulerTour + Fenwick Tree