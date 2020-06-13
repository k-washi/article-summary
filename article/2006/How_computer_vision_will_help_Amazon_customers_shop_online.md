# [How computer vision will help Amazon customers shop online](https://www.amazon.science/blog/how-computer-vision-will-help-amazon-customers-shop-online?utm_campaign=piqcy&utm_medium=email&utm_source=Revue%20newsletter)


[Image Search with Text Feedback by Visiolinguistic Attention Learning](https://assets.amazon.science/01/7b/af090cd94d609a6d9d5a75764e1d/scipub-1303.pdf), [Fashion Outfit Complementary Item Retrieval](https://assets.amazon.science/72/77/286db9ed405b859ba6cf161fec31/scipub-1282.pdf), [Image Based Virtual Try-on Network from Unpaired Data](https://assets.amazon.science/1a/2b/7a4dd8264ce19a959559da799aff/scipub-1281.pdf)の3つの論文を紹介

1. 言語による画像検索(もうちょい明るい色の服など、)
2. 補完的アイテム検索（このアウターに合わせるインナー）
3. 仮想試着（画像の生成）

## 課題

テキストを用いて製品クエリに一致する画像を探索する課題は、
1. テキストによる説明と画像の特徴を1つの表現に埋め込む
2. 1の埋め込むを様々な解像度で行うこと
3. ネットワークの訓練を通して、一部の画像特徴を維持しながら、指示に従って他の特徴を変更すること

