# Edison kit for Arduino

ここではEdison kit for ArduinoのMacでの設定について記述します。

Windowsの設定については下記を参考に行って下さい。

http://edison-lab.jp/gettingstarted/edison-arduino/windows/

## 初期化

設定を行う前に、Edisonの初期化を行う必要があります。

「アプリケーション」フォルダ内の「ユーティリティ」フォルダにある、ターミナル.appを実行します。

![](/img/dev/edison/setup001.png)

下記のコマンドを実行し、Edisonのフォルダに移動します。
```
cd /Volumes/Edison
```

![](/img/dev/edison/setup002.png)

Edisonのフォルダに移動したことを確認後、不要なファイルを削除するため、下記のコマンドを実行します。

```
rm –rf *
rm -rf \.*
```

![](/img/dev/edison/setup003.png)

削除が完了後、「exit」を入力し、処理を終了します。

![](/img/dev/edison/setup004.png)

「アプリケーション」フォルダ内の「ユーティリティ」フォルダにある、ディスクユーティリティ.appを実行します。

ここでEdisonを選択し、「消去」ボタンを押します。
![](/img/dev/edison/setup005.png)

名前に「Edison」を入力、フォーマットで「MS-DOS(FAT)を選択し、「消去」ボタンを押します。
![](/img/dev/edison/setup006.png)

終了したら「完了」ボタンを押して終了です。
![](/img/dev/edison/setup007.png)

## サポートツールのダウンロード

下記URLより、OSに合ったソフトウェアのダウンロードを行います。

https://software.intel.com/en-us/iot/hardware/edison/downloads

![](/img/dev/edison/setup011.png)

ダウンロードしたファイルを実行し、Edisonの最新のイメージを書き込みます。
内容確認後に「Next」ボタンを押し、次へ進みます。

![](/img/dev/edison/setup012.png)

記述内容に同意して「Next」ボタンを押します。

![](/img/dev/edison/setup013.png)

「flash firmware」ボタンを押します。

![](/img/dev/edison/setup015.png)

上側にチェックをつけた状態で「Next」ボタンを押します。

![](/img/dev/edison/setup016.png)

自動的に設定が行われるので完了するまで待ちます。
この設定には１０分程度の時間がかかります。

![](/img/dev/edison/setup017.png)

完了すると下記のメッセージが表示されるので「OK」を押します。

![](/img/dev/edison/setup018.png)

「Finish」ボタンを押して設定完了です。

![](/img/dev/edison/setup019.png)
