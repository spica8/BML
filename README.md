# BML
Blocks for Machine Learning (Original blocks of Scratch3.0)

------

# 概要
Scratch3.0 の拡張機能と ml5.js [ml5js]('https://ml5js.org/') を利用して、機械学習用のブロックを作成した。

構成
 - BML-TL  (Transfer Learning)   (β版公開)  
      転移学習を行う。特徴量抽出はMobileNet、分類器にはニューラルネットワークを用いる。  
      ml5.jsのfeatureExtractor()を利用したブロック。 
 - BML-kNN (k-nearest neighbors) (作成中)  
      特徴量抽出にはMobileNetを利用し、k近傍法を用いて分類を行う。  
      ml5.jsのfeatureExtractor()とKNNClassifier()を利用したブロック。
 - BML-IC  (Image Classifier)    (作成中)  
      ImageNetの画像を用いてあらかじめ学習したネットワークを用いた分類を行う。  
      ml5.jsのimageClassifier()を利用したブロック。

の３種のブロックからなる。（現在公開中は BML-TL のみ）

# BML-TL (β版)
以下にアクセスしてScratch3.0を実行する。（対応ブラウザはchromeのみ）

[BML](https://spica8.github.io/scratch-gui/)  (https://spica8.github.io/scratch-gui/)  

Scratch3.0が起動したら、左下のアイコン「+」をクリックして「拡張機能」の一覧を表示させ「BML TL」を選択する。

## 学習用データの準備
### データの構成
機械学習ように画像データを用意する。各画像は一つのクラスに属しているものとする。
クラスと画像の対応を表すために、Scratchのスプライトとコスチュームを利用する。
対応のルールを次のように定める。
- Scratchのスプライト１つが、分類クラスの1つに対応する。
- 各スプライトには、そのクラスに属する画像をコスチュームとして登録する。
- 学習時には、全てのスプライトを分類クラスとして扱う。このため、学習時にはデータに利用するスプライト以外を作成しないようにする。

### データ準備手順

0. 学習に用いないスプライトは全て削除する。
1. 分類するクラスと同じ数だけスプライトを追加する。
2. スプライト名をクラス名となるよう変更する。
3. Videoをonにする。（適宜左右反転flipを指定する）
4. 「photo \[スプライト名\]」のブロックでスプライトを指定し、そのクラスに対応する画像を撮影する。→指定したスプライトに画像が追加される。
5. スプライトを確認し、不要な画像は削除する。

## 学習
学習は、「ネットワークモデルのパラメータ設定」→「初期化」→「学習」の順に実施する。
スプライト名をクラス（教師データ）とし、コスチュームを学習画像とした学習を行う。

### ネットワークモデルのパラメータ設定
ここでは、特徴量の抽出に MoblileNet を利用した転移学習 (Transfer Learning) を行う。
設定には「set \[ パラメータ \] as \[ 値 \]」ブロックを用いる。
設定可能なパラメータを以下に示す。

* MobileNetのパラメータ
	* version   : MobileNetのバージョン (1 または 2(現在 ver. 2 のパラメータが取得できない状態))
	* alpha     : width maultiplier のパラメータ (ver.1 では 0.25, 0.50, 0.75, 1.0のいずれか一つ) (0.50を0.5と書くとNG)
* その他のパラメータ
	- hiddenUnits  : 中間層のユニット数
	- numLabels    : ラベル数 (学習するクラスの数 = 用意したスプライトの数)
	- learningRate : 学習率 (更新の割合）
	- batchSize    : バッチサイズ (0.0から1.0 割合で指定)
	- epochs       : エポック数 (学習の回数：全てのバッチの学習を1周終えると1エポック)
* 各パラメータの初期値  
|パラメータ  | 初期値|  
|:-----------|------:|  
|version     |      1|  
|alpha       |   0.25|  
|hiddenUnits |    100|  
|learningRate| 0.0001|  
| epocs      |     20|  
| numLabels  |      2|  
| batchSize  |    0.4|  

### 初期化
上記パラメータを設定して

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
