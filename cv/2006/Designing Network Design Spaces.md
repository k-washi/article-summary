[Designing Network Design Spaces](https://arxiv.org/pdf/2003.13678.pdf)


ネットワークアーキテクチャの全探索は、現実的ではない。
> AnyNet: VGG、ResNet、ResNeXtなどの標準的なモデル・ファミリーを想定して、ネットワークの構造（例えば、幅、深さ、グループなど）を探求することに焦点

AnyNetより単純なモデルを持ち、解釈が容易かつ高精度なモデルが RegNet

## ネットワークに関する得られた知見

+ 最適な深さは 20 ブロック（60 層）で、最適なモデルの深さは計算領域全体で安定していること
+ 最近のモバイルネットワークでは、反転ボトルネックを採用しているのが一般的ですが、反転ボトルネックを使用するとパフォーマンスが低下すること (Inverted Residual Blockのこと？ mobile net v2より導入 - 計算速度の向上には寄与している)

## 性能はどうか

SOTA (State Of The Art) である EfficientNet と同等の性能を持ちながら、infer(ms)が速い。

## 参考
https://blog.kikagaku.co.jp/2020/04/06/network-design-spaces-regnet/