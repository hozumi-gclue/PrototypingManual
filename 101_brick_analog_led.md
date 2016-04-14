# #101 LED Brick

<center>![](/img/100_analog/product/101_led_product.jpg)
<!--COLORME-->

## Overview
LEDのBrickです。

発光色は5色（青・緑・赤・白・黄）あります。Lチカのおともにもどうぞ。

※購入時は色の間違いにご注意ください。

## Connecting
### Arduino
アナログコネクタ(A0〜A5)、またはデジタルコネクタ(2〜13)のいずれかに接続します。

![](/img/100_analog/connect/101_led_connect.jpg)

### Raspberry PI
GPIOコネクタのいずれかに接続します。

### IchigoJam
OUTコネクタのいずれかに接続します。

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Schematic
![](/img/100_analog/schematic/101_led_schematic.png)

## Sample Code
### Arduino
D2コネクタにLED Brickを接続し、一定時間ごとに点灯/消灯（Lチカ）させています。
```c
//
// FaBo Brick Sample
//
// #101 LED Brick
//

#define ledPin 2 // LEDピン

void setup() {
  // LED接続ピンを出力に設定
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // LEDを一定時間で点滅
  digitalWrite(ledPin, HIGH);
  delay(1000);
  digitalWrite(ledPin, LOW);
  delay(1000);
}
```

### Raspberry Pi
GPIO4コネクタにLED Brickを接続し、一定時間ごとに点灯/消灯させています。
```python
# coding: utf-8
#
# FaBo Brick Sample
#
# brick_analog_led
#

import RPi.GPIO as GPIO
import time

LEDPIN = 4

GPIO.setwarnings(False)
GPIO.setmode( GPIO.BCM )
GPIO.setup( LEDPIN, GPIO.OUT )

while 1:
	GPIO.output( LEDPIN, True )
	time.sleep( 1.0 )
	GPIO.output( LEDPIN, False )
	time.sleep( 1.0 )
```
GPIO関連の処理は、Rootの権限が必要です。

実行例)
    sudo python led.py
 
### IchigoJam

OUT(n1),n2

n1=ポート番号（1〜6）<br>
n2=スイッチ（0=消灯　1=点灯）

例）<br>
OUT(1),1<br>
結果）<br>
OUT1に接続しているLED brickが点灯する。

```basic
100 'led_sample_program
110 OUT(1),1
120 WAIT 60
130 OUT(1),0
140 WAIT 60
150 GOTO 110
```
60ミリ秒（1秒）間隔で点灯と消灯を繰り返す。

### Nordic

```c
#include "nrf_delay.h"
#include "nrf_gpio.h"

int main() {

    nrf_gpio_cfg_output(1);
    nrf_gpio_pin_set(1);

    while(true) {
        nrf_gpio_pin_toggle(1);
        nrf_delay_ms(1000);
    }
}

```
GPIO abstraction
* [nrf_gpio_cfg_output](http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.sdk51.v10.0.0%2Fgroup__nrf__gpio.html&resultof=%22nrf_gpio_cfg_output%22%20)
* [nrf_gpio_pin_set](http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.sdk51.v10.0.0%2Fgroup__nrf__gpio.html&resultof=%22nrf_gpio_cfg_output%22%20)
* [nrf_gpio_pin_clear](http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.sdk51.v10.0.0%2Fgroup__nrf__gpio.html&resultof=%22nrf_gpio_cfg_output%22%20)

### Cylon.js

```js
var Cylon = require('cylon');

Cylon.robot({
        connections: {
                arduino: { adaptor: 'firmata', port: '/dev/tty.usbmodem1411' }
        },

        devices: {
                led: { driver: 'led', pin: 13},
        },

        work: function(my) {
                every((1).second(), function() {
                        my.led.toggle()
                });
        }
}).start();
```

## Parts
- 5mm LED(各色)
