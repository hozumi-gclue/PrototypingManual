# #110 Tilt Brick

<center>![](/img/100_analog/product/110_tilt_product.png)
<!--COLORME-->

## Overview
傾斜センサーを使用したBrickです。

I/Oピンより傾斜センサーの状態をデジタル値(0〜1)取得することができます。
黒い部分の中に玉が入っていて傾くとデジタル値が変化します。


## Connecting
![](/img/100_analog/connect/110_tilt_connect.jpg)

A0コネクタに接続したTilt Brickの傾きによって、A1コネクタに接続したLED Brickを点灯/消灯させています。

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Schematic
![](/img/100_analog/schematic/110_tilt_schematic.png)

## Sample Code
### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_analog_tilt
//

int buttonPin = A0;
int ledPin = A1;

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

