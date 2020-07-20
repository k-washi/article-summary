[4 Ways to Debug your Deep Neural Network](https://blog.cardiogr.am/4-ways-to-debug-your-deep-neural-network-e5edb14a12d7)

モデルをどのようにしてデバッグするのか。

[Cardiogram](https://apps.apple.com/jp/app/cardiogram-heart-rate-monitor/id1000017994)で使用した、デバッグ方法を紹介。

1. 合成出力タスク (std(daytime HRs) - std (nighttime HRs))
2. アクティベーションの視覚化　(アクティべションが活性化しているセルを見る)
   [Four Experiments in Handwriting with a Neural Network](https://distill.pub/2016/handwriting/)
   => 時間がたっても変化しない（入力の影響を受けない）「ニューロンの死」
   畳み込み層が全て0を出力する結果、バイアスだけ出力(Reluで、めっちゃ負になったから)
   => Leaky Reluに置き換えることで修正

   ↑のようなバクが見つかる。

3. 勾配分析
   勾配分析を使用して、DNNがデータの長期的な依存関係を捕捉できるかどうかを判断した。

   > モデルが長期間の依存関係を追跡できるかどうかの簡単な尺度は、出力予測に対する入力データの各タイムステップの影響をチェックすることです。後のタイムステップの影響が劇的に大きい場合、モデルは前のデータを効果的に使用していない可能性があります。

4. モデル予測を分析する

