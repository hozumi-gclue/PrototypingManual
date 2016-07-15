# FaBo Pythonライブラリのインストール

## Overview

RaspberryPiで使用しているPythonのライブラリはpipコマンドによりインストールすることができます。 対応しているものは、それぞれのBrickのページで案内しています。

## Pythonのバージョンについて

Pythonのライブラリは、RaspberryPiの初期状態でインストールされている2.7系に対応しています。

## インストール方法
ターミナルを起動し、以下のコマンドを実行します。

```
sudo pip install モジュール名
```

例：#201 3Axis i2c Brickのライブラリをインストールする場合
```
sudo pip install FaBo3Axis_ADXL345
```

これでインストール完了です。