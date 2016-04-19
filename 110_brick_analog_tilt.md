# #110 Tilt Brick

<center>![](/img/100_analog/product/110_tilt_product.jpg)
<!--COLORME-->

## Overview
傾斜センサーを使用したBrickです。

I/Oピンより傾斜センサーの状態をデジタル値(0〜1)取得することができます。

黒い部分の中に玉が入っていて傾くとデジタル値が変化します。

LED Brickを点灯/消灯させる際などに使用します。


## Connecting
### Arduino
アナログコネクタ(A0〜A5)、またはデジタルコネクタ(2〜13)のいずれかに接続します。
![](/img/100_analog/connect/110_tilt_connect.jpg)

### Raspberry PI
GPIOコネクタのいずれかに接続します。

### IchigoJam
OUTコネクタのいずれかに接続します。

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Schematic
![](/img/100_analog/schematic/110_tilt_schematic.png)

## Sample Code
### for Arduino

A0コネクタに接続したTilt Brickの傾きによって、D2コネクタに接続したLED Brickを点灯/消灯させています。

```c
//
// FaBo Brick Sample
//
// #110 Tilt Brick
//

#define buttonPin A0
#define ledPin 2

int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT); 
  pinMode(ledPin, OUTPUT);         
}

void loop(){
 
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {        
    digitalWrite(ledPin, HIGH);  
  } 
  else {
    digitalWrite(ledPin, LOW); 
  }
}
```

## Parts
- 振動(傾斜)スイッチ

