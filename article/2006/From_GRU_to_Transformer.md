# [From GRU to Transformer ](https://ogunlao.github.io/blog/2020/06/12/from_gru_to_transformer.html?utm_campaign=piqcy&utm_medium=email&utm_source=Revue%20newsletter)

Transformersで自己アテンション機構がどのように適用されているかを理解するには、既知のもの、すなわちLSTMやGRUなどのリカレントニューラルネットワークから、Transformerのような自己アテンションネットワークへとステップバイステップでビルドアップしていくのが、数学的な観点からは直感的かもしれません。

別の切り口で説明したブログ
 + [The Annotated Transformer](http://nlp.seas.harvard.edu/2018/04/03/attention.html)
 + [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)

LSTMやGRUなどゲートを持つRNNは、Vanilla-RNNの消失問題や長期依存性問題を解決するのに役立つ。アテンション機構も同様。しかし、再起的な計算にいまだ依存している。

## Gated Recurrent Neural Networks

$$
  h_t = u_t \odot h_{t-1} + (1 - u_t) \odot \tilde{h}_t
$$

1. $u_t$が0だと、前の情報は忘れて現在のコンテキベクトル$\tilde{h}_t$に依存する
2. $u_t$が1だと、前の情報（隠れ層）$h_{t-1}$のコピー


$\tilde{h}_t$は、入力xと前の隠れ層hによる関数され、これはリセットゲートを無視した単純なGRUの更新式が以下で表される。
$\tilde{h_t} = f(x_t, h_{t-1}) = tanh(\textbf{W} x_t + \textbf{U}h_{t-1} + b)$

加法更新の解釈は、現在の状態の隠れベクトルと以前の状態の間に線形のショートカット接続を作成するのに役立つということです。（ResNetのような一般的なニューラルネットワークアーキテクチャに見られる残差接続に似ています）。

## What are these shortcut connections

一つ前の隠れ層は、それ以前の全ての隠れ層の重み付けの組み合わせで形成されている。
$$
  h_t = u_t \odot \left(u_{t-1} \odot \left(u_{t-2} \odot h_{t-3}+(1-u_{t-2})\odot \tilde{h_{t-2}} \right) + (1-u_{t-1})\odot \tilde{h}_{t-1}) \right) +(1-u_t)\odot\tilde{h}_t
$$

## Gated Recurrent Units to Causal Attention

GRUは、多くのパラメータとコンポーネントの間に依存関係がある。これを紐解いていく。(以下の式)

$$
h_t = \sum_{i=1}^t \left(\prod_{j=1}^{t-i+1} u_j \right) \left(\prod_{k=1}^{i-1} (1-u_k) \right) \tilde{h}_i
$$

GRUsでは、$u_t$は、以下の式で表される。

$$
u_t = \sigma(W_x x_{t-1} + U_h h_{t-1} + b_u)
$$

$$
h_t = f(h_{t-1}, x_{t-1}) = u_t \odot \tilde{h_t} + (1-u_t)\odot h_{t-1}
$$

$u_t$を観測でき、$h_{t-1}$に依存していることが分かる。

$u_t$を$h_{t-1}$から分離するため、現在のコンテキストベクトル$h_t$を候補ベクトル$h_i$の組み合わせ重みとして学習することができる。以下の式は、暗に、現在や前の候補ベクトルは、隠れそうを評価している。

$$
h_t = \sum_{i=1}^t \alpha_i \tilde{h}_i
$$
$$
\alpha_i \propto exp\left(ATT\left(\tilde{h}_i, x_t\right)\right)
$$

## Let’s free up candidate vectors

$\tilde{h_t} = f(x_t, h_{t-1})$では、$\tilde{h_t}$は$h_{t-1}$に依存し、$h_{t-1}$は$\tilde{h_{t-1}}$に依存している。

=> $\tilde{h_t}$は$\tilde{h_{t-1}}$に依存

これをなくすため、$h_t = \sum_{i=1}^t \alpha_i \tilde{h}_i$において、候補ベクトルを$f(x_i)$に置き換える。

$$
\alpha_i \propto exp\left(ATT\left(f(x_i), f(x_t)\right)\right)
$$

$f(x_i)$, $f(x_t)$はkey vectorで、$ATT(.,.)$はアテンション機構のQuery vectorです。

$h_t = \sum_{i=1}^t \alpha_i f(x_i)$, $f(x_i)$はvalue vectorです。

Query, Key, Valueを計算するために必要なものは、$f(.)$, $x_{t}$, $x_{i}$である。
$f(.)$はembeding layerになる。

## Let’s separate Keys and Values

以下、単一のアテンション機構にするようにQ, K, Vを分離。
しかし、これではモデルの表現力が不十分かもしれないので、複数のアテンションヘッドを持つのは良いアイデア。

## Let’s have multiple attention heads

$$
h_t = \left[h_t^1;~ h_t^2;~ …;~ h_t^N \right]
$$

$h_t^n = \sum_{i=1}^t \alpha_i^n V^n(f(x_i))$and, $\alpha_i^n \propto exp(ATT(K^n(f(x_i)), Q^n(f(x_t))))$

## Let’s give a sense of position to the attention mechanism
ポジションについて

## Let’s use Non-Linear Attention
線形だと、アテンションを操作して複雑な組み合わせを見つけるのは難しい。解決策としては，アテンション後に非線形関数を適用することになります．

$$
h_t = \left[g(h_t^1);~ g(h_t^2);~ …;~ g(h_t^N) \right]
$$




以下、式ばかりなので、ブログ本文参照。


