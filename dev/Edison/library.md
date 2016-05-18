# ライブラリの設定

ここではIntel社から提供されている「mraa」というライブラリを使用します。

## Wi-Fiの設定
ライブラリをインストールするためにはネットワークの設定を行う必要があります。

下記を参考にWi-Fiの設定を行って下さい。

 * Windows (Step3〜4)

http://edison-lab.jp/gettingstarted/edison-arduino/windows/

 * MacOS (Step3)

http://edison-lab.jp/gettingstarted/edison-arduino/mac/


## 設定ファイルの変更

下記のコマンドより、設定ファイルを開きます。(存在しない場合は作成)
```
vi /etc/opkg/mraa-upm.conf
```

mraa-upm.confに下記の内容を追加します。
```
src mraa-upm http://iotdk.intel.com/repos/2.0/intelgalactic
```

## インストール

下記のコマンドにより、mraaのライブラリをインストールします。
```
opkg update
opkg upgrade
```
