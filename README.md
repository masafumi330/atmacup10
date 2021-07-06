![comp](./info/001.png)
# atmacup10
atmacup#10 美術作品のいいね数の予測

## Basics

## info

## Overview

## Evaluation
評価指標はRMLSE.

![comp](./info/002.png)

## Datasets

![comp](./info/003.png)


# Log

### 20210705
- join
- data download

- nb001
    - データをgoogleスプレッドシートで眺めてみる。
    - __train.csv__
        - sub_title: cmとmmで、単位が揃っていない。
        - copyright_holder: ほとんどが欠損。全く埋まってない。
        - acquisition_method: unknown(収集方法不明)とかもあるんだな。
        - acquisition_credit_line: (収集に際して資金提供などを行った場合の情報)も空欄が多いかな。
        - dating_presenting_date: 制作期間がきちんと書かれている（ex. 1990-2000）のもあるが、c. 1619 - c. 1625や、1999（代表年だけ？）のものもあり、表記が揃っていない。

### 20210706
- データ確認の続き
    - test.csv
        - train.csvと似たような感じ
        - acquisition_dateもちょくちょく抜けているな

    - material.csv
        - 同一のobject_idに対して複数のname　・・・　複数のマテリアルで作られてるのがほとんどだな
        - 何の紙に書いているか（paper, photographic paper, canvas, etc.)と、何で書いているか？(oil paint)

    - maker.csv
        - データほとんど欠損
        - 名前と誕生日〜死亡した場所まで書かれている人と、名前しか書かれていない人の両極端
        - 国籍はほとんどの作家が不明
        - 死亡した場所：アムステルダム、パリ、など

    - production_place.csv
    - historical_person.csv
        - 人物の名前で、かっこ付けで長く表記されている人がちらほら見られるがどういう意味のかっこだ？
        - Elisabeth Stuart (keurvorstin van de Palts, koningin van Bohemen) めちゃくちゃ長い

    - object_collection.csv
        - 作品の形式タイプ
        - paintings, musical instrumentsとかもあるんだ、
        - 10種類ほど

    - principal_maker.csv
        - idカラムが、principal_maker_occupation.csvのidと紐づく
        -  qualification(どのような関わり方をしたか？)：mentioned on object、workshop of... 欠損ちらほら
        - qualiication, roles, productionPlaces が同時に空のものもある

    - principal_maker_occupation.csv
    - technique.csv
    
- 現象の理解
    - このデータはどういうふうに作られているか？
    - train.csv[acquisition_method]を見ると、さまざまな収集方法がある。いいね数で比較すると、いいねが多い作品は"loan", "purchase", "bequest(遺贈された)"などが多い印象。対していいねが少ない作品は"transfer"などが多いような。
    
    
    <span style="font-size: 180%; color: red;">つまり、状態が良い作品にはいいねしたくなるのではないか？</span>

- 予測対象の確認
    - 予測対象　＝　いいねの数
    - よって、出力値は０以上の整数
    
- 評価指標の確認
    - 評価指標　＝　RMSLE
    - だが、RMSLEは一度log1p変換をするとRMSEとして取り扱えるらしい
    - log1pってなんぞ？？
        - おそらく、　log(1+x) ≒ x とすること？
        
        そう考えれば、RMSLEとRMSEは等価だと考えられるのではないか
        
        ![comp](./info/002.png)
        
        ![comp](./info/004.png)
        
    - 一般的なモデルの損失関数ではRMSEが使えるからRMSEで取り回したほうが良さそう