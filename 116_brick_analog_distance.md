# #116 Distance Brick

<center>![](/img/100_analog/product/116_distance_product.jpg)
<!--COLORME-->

## Overview
距離センサー（GP2Y0A21YK）を使用したBrickです。

I/Oピンより距離センサーの正面についているレンズから物体までの距離をアナログ値(0〜1023)で取得することができます。

測定可能な距離は10〜80cmとなっています。

## Connecting
### Arduino
アナログコネクタ(A0〜A5)のいずれかに接続します。
![](/img/100_analog/connect/116_distance_connect.jpg)
### Raspberry PI
アナログコネクタ(A0〜A7)のいずれかに接続します。

### IchigoJam
アナログ用コネクタ(IN2またはANA()で設定したコネクタ)のいずれかに接続します。

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## GP2Y0A21YK Datasheet
| Document |
| -- |
| [GP2Y0A21YK Datasheet](http://www.sharpsma.com/webfm_send/1208) |


## Sample Code

### for Arduino
A0コネクタに接続して、距離を計測します。

```c
//
// FaBo Brick Sample
//
// #116 Distance Brick
//

#define distancePin A0 // 距離センサーピン

int distanceValue = 0;

void setup() {
  // 距離センサーピンを入力用に設定
  pinMode(distancePin, INPUT);
  // シリアル開始 転送レート：9600bps
  Serial.begin(9600);
}

void loop() {
  // センサーより値を取得(0〜1023)
  distanceValue = analogRead(distancePin);
  
  // 取得した値を電圧に変換 (0〜5000mV)
  distanceValue = map(distanceValue, 0, 1023, 0, 5000);

  // 変換した電圧を3200(3.2v)〜500(0.5v)の値に変換後、距離に変換 (10〜80cm)
  distanceValue = map(distanceValue, 3200, 500, 5, 80);

  // 算出した距離を出力
  Serial.println(distanceValue);

  delay(100);
}
```

### for Raspberry PI
A0コネクタに接続し、距離を計測します。
```python
#!/usr/bin/env python
# coding: utf-8

#
# FaBo Brick Sample
#
# #116 Distance Brick
#

import spidev
import time
import sys

# A0コネクタにDistanceを接続
DISTANCE_PIN = 0

# 初期化
spi = spidev.SpiDev()
spi.open(0, 0)

def readadc(channel):
    adc = spi.xfer2([1, (8+channel)<<4, 0])
    data = ((adc[1]&3) << 8) + adc[2]
    return data

def arduino_map(x, in_min, in_max, out_min, out_max):
    return (x - in_min) * (out_max - out_min) // (in_max - in_min) + out_min

if __name__ == '__main__':
    try:
        while True:
            data = readadc(DISTANCE_PIN)
            # 取得した値を電圧(mv)に変換
            volt = arduino_map(data, 0, 1023, 0, 5000)
            # 電圧から距離(cm)に変換
            distance = arduino_map(volt, 3200, 500, 5, 80)
            print("distance : {:3} ".format(distance))
            time.sleep(0.05)
    except KeyboardInterrupt:
        spi.close()
        sys.exit(0)
```