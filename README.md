# BML
Blocks for Machine Learning (Original blocks of Scratch3.0)

------

# 概要
Scratch3.0 の拡張機能を利用して、機械学習用のブロックを作成した。
内部的には ml5.js を利用している。

構成として
 - BML-TL  (Transfer Learning)   (β版公開)  
      転移学習を行う。特徴量抽出はMobileNet、分類器にはニューラルネットワークを用いる。
 - BML-kNN (k-nearest neighbors) (作成中)  
      特徴量抽出にはMobileNetを利用し、k近傍法を用いて分類を行う。
 - BML-IC  (Image Classifier)    (作成中)  
      ImageNetの画像を用いてあらかじめ学習したネットワークを用いた分類を行う。

の３種のブロックからなる。

# BML-TL (β版)
以下にアクセスして実行（ブラウザはchromeのみ対応）

[BML](https://spica8.github.io/scratch-gui/)  (https://spica8.github.io/scratch-gui/)  

Scratchが起動したら、左下のアイコン「+」をクリックして「拡張機能」の一覧を表示させ、「BML TL」を選択する。

## データの準備
- Scratchのスプライト１つが、分類クラスの1つにに対応している。
- 各スプライトには、そのクラスに対応する画像をコスチュームとして登録する。
- スプライトを必要な数だけ追加する。スプライト名をクラス名となるよう変更する。
- videoをon（適宜左右反転flipを指定する）
- photo「スプライト名」のブロックで撮影→指定スプライトに画像登録ができる。

## 学習
- コスチュームを学習画像とし、クラスをスプライト名（教師データ）に対応づける学習を行う。
- set「option」as ○ ブロックで、ネットワークのパラメータを設定できる
	- version : MobileNetのバージョン (1 or 2)
	- alpha: 0.25, 0.50, 0.75, 1.0
	- learningRate: 学習率
	- hiddenUnits: 隠れ層のユニット数
	- epochs: エポック数
	- numLabels: ラベル数
	- batchSize: バッチサイズ

- 学習実行（用意したスプライト（クラス名）とコスチューム（画像データ）を用いた学習実行）

## 分類
- ネットワークの学習後、あるいは既存の学習済みデータの読み込み後、分類実行できる。
- videoをon（適宜左右反転flipを指定する）とし、classifyブロックを実行した瞬間の画像についての分類を行う。

## モデルの保存と読み込み
- 学習済みモデルを保存できる。その際 model.jsonとmodel.weights.binの２つのファイルができる。
- モデル読み込みには上記２つのファイルを同時に指定する。


# Licence

[MIT]

# Author

[spica8](https://github.com/spica8)
