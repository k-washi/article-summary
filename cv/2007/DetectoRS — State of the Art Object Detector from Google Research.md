[DetectoRS — State of the Art Object Detector from Google Research](https://medium.com/visionwizard/detectors-state-of-the-art-object-detector-from-google-research-e0b89abdd1fc)

https://arxiv.org/pdf/1906.09756.pdf

## 導入

+ 最近、thinking and looking twice mechanism の2ステージODが有用と証明されている。
+ FasterRCNNなどのODは、最初に、foreground と backgroundの分類に基づいてオブジェクトの検出を行い、後のステージで、セマンティックごとの分類/検出を行う。
+ Fig.1 のように、2ステージメカニズムの後 Cascade RCNNは、predictの閾値問題に対処するため、複数の閾値で学習させている。(左：推論時、右：B1->B3に向かうほど、学習時のIoUが大きくなり、ざっくりとした予測から、次第に正確な予測へ移動する。)

## ASPP（Atrous Spatial Pyramid Pooling)
    ネットワークの受容フィールドを増やすために使用される。異なるatrousレートで拡張されたカーネルサイズの畳み込みが行われる。
## Fusion Module。
Fig.9 グモイド関数は、現在の機能の中間アテンションマップを生成し、両方の入力の集計に使用されます。
