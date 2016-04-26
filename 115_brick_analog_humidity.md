# #115 Humidity Brick

<center>![](/img/100_analog/product/115_humidity_product.jpg)
<!--COLORME-->

## Overview
湿度センサーを使用したBrickです。

温度、湿度の情報を取得することができます。

## Connecting
### Arduino
アナログコネクタ(A0〜A5)のいずれかに接続します。

![](/img/100_analog/connect/115_humidity_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|×|×|

## Schematic
![](/img/100_analog/schematic/115_humidity_schematic.png)

## Sample Code
### for Arduino
A0コネクタに接続して、湿度を計測するサンプルになります。

このサンプルコードでは外部ライブラリを使用します。

https://github.com/adafruit/DHT-sensor-library
よりDHTライブラリをインストールしてください。

ライブラリの組み込み方法 (https://sites.google.com/a/gclue.jp/iot-docs/shi-du)

```c
//
// FaBo Brick Sample
//
// #115 Humidity Brick
//
// DHT Library Downloads
// https://github.com/adafruit/DHT-sensor-library

#include "DHT.h"
DHT dht(A0, DHT11);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {

  delay(1000);

  float h = dht.readHumidity();
  float t = dht.readTemperature();

  Serial.print("Hum: "); 
  Serial.print(h);
  Serial.print(" %");
  Serial.print("  Temp: "); 
  Serial.print(t);
  Serial.println(" *C");
}
```


## Parts
- 湿温度センサモジュールDHT11
