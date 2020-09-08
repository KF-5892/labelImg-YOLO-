# labelImg-YOLO-
labelImgを使用して自前で用意した画像にラベル付けする# YOLOv5用カスタムデータの自作(labelImg)

## 概要

YOLOv5で使用できるカスタムデータを自作して、プリセットにない物体を認識させる。

### 環境

Mac OS Catalina 10.15.5

仮想環境としてVirtualenv

## 手順

1. 仮想環境作成
2. labelImgのインストール
3. 画像のアノテーション作成
4. 「train」「valid」「test」にデータを振り分け
5. 学習・推定

### 仮想環境作成

最初に、仮想環境を作成したいフォルダでターミナルを開く

仮想環境フォルダの作成。今回は「labelImg_test001」という名前でフォルダを作成する

```
python -m venv labelImg_test001
```

仮想環境フォルダ移動

```
cd labelImg_test001
```

仮想環境の実行

```
source bin/activate
```

githubからlabelImgをダウンロード

```
git clone https://github.com/tzutalin/labelImg.git
```

labelImgフォルダに移動＋pyqt5インストール

```
cd labelImg
pipenv run pip install pyqt5
```

実行

```
python3 labelImg.py
```

この画面が出てきたら成功。

### 画像のアノテーション作成

labelImgフォルダ内に、任意のフォルダを作成し、中に学習用の画像を入れる。

ここでは「test01」というフォルダを作成して説明する。

「labelImg」フォルダ内の「data」フォルダ内にある「predefined_classes.txt」の内容を削除し、使用したいカテゴリを入力する。ここでは「oversway」と入力

labelImgの画面左のリストから「open Dir」を選択。先ほど作成した「test01」を選択する。(画像赤丸部分)

<img width="393" alt="スクリーンショット 2020-09-08 14 33 45" src="https://user-images.githubusercontent.com/68985919/92439978-b9312800-f1e6-11ea-8afe-c0766680f5e8.png">


画像赤丸より１つ下の「Change Save Dir」を、先ほど作成した「test01」に設定。

1. w　四角を作る
2. ctrl+s　保存
3. d　次の画面に移動する

の順番で、全ての画像のアノテーションが終わるまで続ける。



### データ分割

別の場所に任意のフォルダを作成。（ここでは「test_dataset」という名前で作成）

「test_dataset」内に「train」「valid」「test」フォルダを作成。

また、それぞれのフォルダ内に「images」「labels」フォルダを作成

「test_dataset」内にテキストエディタで「data.yaml」を作成。（他のカスタムデータセットをコピーして編集すると楽）

以下のように入力する。

```
train: ../train/images
val: ../valid/images

nc: 1
names: ['oversway']
```

ここまでのフォルダ構成

- test_dataset
  - train
    - images
    - labels	
  - valid
    - images
    - labels
  - test
    - images
    - labels
  - data.yaml	

「train」「valid」「test」フォルダにそれぞれ画像と、対になるtxtファイルを

train：valid：test =７：２：１ぐらいの割合で入れる。「image」フォルダには画像を、「labels」フォルダにはtxtフォルダを入れる。

### 完成


