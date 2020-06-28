# [New mobile neural network architectures](https://machinethink.net/blog/mobile-architectures/)

## 問題

鯨の写真が5004頭ぶんあり、既知の鯨の個体であるか、それとも、新しい個体の鯨かを識別する課題。

### 課題
1. データの不均衡 => そのままでは、分類できなかった。
2. 鯨が新しい個体かどうか判断すること

## 初期設定

1. 一部の画像の位置合わせてが全くされていなかった　=> 訓練済のBBoxModelで鯨を検出し、それに応じて画像をトリミング
2. 画像のカラー[ガンマ値](https://ja.wikipedia.org/wiki/%E3%82%AC%E3%83%B3%E3%83%9E%E5%80%A4)が異なるので、グレースケールに変換

## アプローチ

### 1 : [Siamese Networks](https://cpp-learning.com/siamese-network/)

進歩的な学習 => 229x229 -> 384x384 -> 512x512と段階的に学習
データの性質上、ランダムな明るさ、ガウスノイズ、ランダムなクロップ、ランダムなぼかし




