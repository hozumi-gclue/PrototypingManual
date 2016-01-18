# #107 LimitSwitch Brick

<center>![](/img/100_analog/product/107_limitswitch_product.jpg)
<!--COLORME-->

## Overview
リミットスイッチを使ったBrickです。

I/OピンよりスイッチのON/OFFの状態を取得することができます。
機械の自動停止や位置検出の際に使用します。

## Connecting
LimitSwitch BrickをA0コネクタに接続し、A1コネクタに接続したLED Brickの点灯/消灯のスイッチとして使用しています。

![](/img/100_analog/connect/107_limitswitch_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Schematic
![](/img/100_analog/schematic/107_limitswitch_schematic.png)

## Sample Code
### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_analog_limitswitch
//

#define buttonPin A0 // リミットスイッチピン
#define ledPin A1    // LEDピン

// リミットスイッチの状況取得用
int buttonState = 0;

void setup() {
  // リミットスイッチピンを入力用に設定
  pinMode(buttonPin, INPUT); 
  // LEDピンを出力用に設定
  pinMode(ledPin, OUTPUT);         
}

void loop(){
  // リミットスイッチの押下状況を取得
  buttonState = digitalRead(buttonPin);

  // リミットスイッチ判定
  if (buttonState == LOW) {        
    // LED点灯
    digitalWrite(ledPin, HIGH);  
  } 
  else {
    // LED消灯
    digitalWrite(ledPin, LOW); 
  }
}
```

### for RaspberryPI

```python
# coding: utf-8
#
# FaBo Brick Sample
#
# brick_analog_limitswitch
#

import RPi.GPIO as GPIO
import time

LEDPIN = 4 
LSPIN = 7   #LimitSwitch pin

led_state = 0	

GPIO.setwarnings(False)
GPIO.setmode( GPIO.BCM )
GPIO.setup( LEDPIN, GPIO.OUT )
GPIO.setup( LSPIN, GPIO.IN)

while True:
    if( GPIO.input( LSPIN ) ):
         led_state = 1 - led_state
    GPIO.output( LEDPIN, led_state )
    print "led_state: %d " % led_state
    time.sleep(0.2)
```

## Parts
