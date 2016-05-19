# #501 OUT/IN Shield for Arduino

<center>![](/img/500_outin/product/501_product.jpg)
<!--COLORME-->

## Overview
OUT/IN Shield for Arduinoは、Arduinoと各種センサーやボタンをケーブルを1本接続するだけで使えるArduino対応シールドです。

Arduino本体、およびArduino UNOケースは含まれません。別途、お買い求めください。

## コネクタ
<center>![](/img/500_outin/connect/501_connect.jpg)

### アナログコネクタ(3pin)
- A0
- A1
- A2
- A3
- A4
- A5

### デジタルコネクタ(3pin)
- D2
- D3(PWM対応)
- D4
- D5(PWM対応)
- D6(PWM対応)
- D7
- D8
- D9(PWM対応)
- D10(PWM対応)
- D11(PWM対応)
- D12(digitalRead使用不可)
- D13(digitalRead使用不可)

### PWM/Servoコネクタ(3pin)
- サーボモータ接続用コネクタ(2.54mmピッチピンヘッダ)

PWMに対応するD3,D5,D6,D9,D10,D11

### シリアルコネクタ(4pin)
SoftwareSerialとして使用するため、RX,TXはそれぞれ、D12,D13になります。

※D12/D13ピンには、5V、3.3V間の電圧レベル変換回路が接続されています。このため、digitalRead()関数は使用不可です。

### I2Cコネクタ(4pin)
Arduino MEGAではR3以降から対応になります。
Arduino UNO R3/R2では使用可能です。

## Schematic
![](/img/500_outin/schematic/501_outin_arduino.png)

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/501_outin_arduino
