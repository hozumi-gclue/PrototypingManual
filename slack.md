# Slack API


## Incoming Webhooks

一番簡単に外部からメッセージを投稿できる方法。  
HTTPで指定のアドレスにJSONをPOSTする。


## Slash Commands

/から始まるコマンドを自作できる。  
コマンドが入力されると指定のアドレスにPOSTされる。


## Bot Users

ログインできないボットユーザーを作成できる。  
Real Time Messaging APIを利用利用してユーザーと対話形式で処理を行う。


## Outgoing Webhooks

Channelや単語を指定して、投稿があったら指定のアドレスにPOSTされる。  
POSTの返信でメッセージを投稿する事も可能。


## Web API

Channelの作成など投稿以外にも様々な事が可能。  
OAuth2で認証。


## Real Time Messaging API

WebSocketを利用してリアルタイムにユーザーとのやり取りを行う事ができる。


## Botkit

ボットを作成するためのフレームワーク。
node.jsで動作する。


## slacker

WebAPIをPythonで利用しやすくしたラッパー。



