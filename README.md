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

### 20210703
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
        - 