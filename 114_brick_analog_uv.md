# #114 UV Brick

<center>![](/img/100_analog/product/114_uv_product.png)
<!--COLORME-->

## Overview
紫外線センサーを使用したBrickです。

I/Oピンより、紫外線の強弱をアナログ値(0〜1023)で取得することができます。

## Connecting
A0コネクタにUV Brick接続し、紫外線の強弱をアナログ値で出力します。

![](/img/100_analog/connect/114_uv_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|×|◯|

## Schematic
![](/img/100_analog/schematic/114_uv_schematic.png)

## Sample Code
### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_analog_uv
//

#define uvPin A0

int uvValue = 0;

void setup() {                
  Serial.begin(9600);    
}

void loop() {
  uvValue = analogRead(uvPin) ;  
  Serial.println(uvValue) ; 
  delay(10);
}
```
###IchigoJam
#####注意<br>アナログはIN2のみで数値取得可能です。
デジタルの場合はIN(2)、アナログの場合がANA(2)とします。
```Basic
100 'UV_sample_program
110 CLS
120 LOCATE 10,8:PRINT "Digital =";IN(2)
130 LOCATE 10,9:PRINT "Analog  =";ANA(2);"  "
140 GOTO 120
```
紫外線に反応して数値が変化します。<br>

## Parts
- GaAsPフォトダイオードG6262
