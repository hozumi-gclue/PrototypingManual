# Botkit

ボットを作成するためのフレームワーク。  
node.jsで動作する。


## BotUserの作成

1. 左のチーム名をクリックすると出てくるメニューから「Apps & Custom Integrations」を選択する。
 ![](slack-iw-001.png)

2. Botsを探してクリックする。
 ![](slack-bu-002.png)

3. Installボタンをクリックする。
 ![](slack-bu-003.png)

4. Botの名前を入力する。
 ![](slack-bu-004.png)

5. API Tokenを覚えておく。
 ![](slack-bu-005.png)


## Botkitのインストール

node.jsとnpmはすでに入っている前提で、任意のフォルダ上で下記コマンドを実行する。

```
npm install --save botkit
```


## HelloWorldプログラム


```
var Botkit = require('botkit');
var controller = Botkit.slackbot();
var bot = controller.spawn({
  // ここを取得したAPI Tokenで書き換える
  token: "xoxb-18479736242-TvtKTRq8Y4xg474FhHCfE32Q"
})
bot.startRTM(function(err,bot,payload) {
  if (err) {
    throw new Error('Could not connect to Slack');
  }
});

// hello/hiの呼びかけに応じる
controller.hears(['hello','hi'],'direct_message,direct_mention,mention',function(bot, message) {
  // 単純にHelloを返すだけ
  bot.reply(message,'Hello.');
});
```


作成したBotに"hi"のダイレクトメッセージを送ると"Hello."と返信する。
![](slack-bu-008.png)