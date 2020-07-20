[Understanding Deep Self-attention Mechanism in Convolution Neural Networks](https://medium.com/ai-salon/understanding-deep-self-attention-mechanism-in-convolution-neural-networks-e8f9c01cb251)

## まとめ

+ セマンティックセグメンテーションとエンコーダーデコーダーアーキテクチャについて説明
+ 標準のCNNアルゴリズムの改善点を挙げている

## 問題点

エンコーダとデコーダの同じ位置ピクセル間では、グローバル情報が保持されないため、ローカル情報のみを利用して宛先ピクセルを計算している。

>フィーチャーマップの各ピクセルを確率変数と見なし、すべてのピクセル間のすべてのペアの共分散を計算すると、画像内の他の各ピクセルとの類似性に従って各予測ピクセル値を強化または弱めることができます。 類似のピクセルはトレーニングと予測の際に利用されますが、異なるピクセルは無視されます。このメカニズムは自己注意と呼ばれます。

モデルは、ページ先を参照。