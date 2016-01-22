# #108 Temperature Brick
<center>![](/img/100_analog/product/108_temperature_product.jpg)
<!--COLORME-->

温度を計測するBrickです。

アナログ値(0〜1023)を取得でき、変換することで−30度から100度までの温度を計測することができます。
<br>

## Connecting
A0コネクタにTemperatureを接続して、温度を計測します。
![](/img/100_analog/connect/108_temperature_connect.png)

## Support
| Arduino | RaspberryPI | IchigoJam |
| -- | -- | -- |
| <center>○ | <center>◯ | <center>○ |

## Schematic
![](/img/100_analog/schematic/108_temperature_schematic.png)


## Sample Code
### Arduino
```c
//
// FaBo Brick Sample
//
// brick_analog_temp_lm61ciz
//

int tempValue = 0;

void setup() {
   // シリアル開始 転送レート：9600bps
   Serial.begin(9600);
}

void loop() {
  // センサーより値を取得(0〜1023)
  tempValue = analogRead(A0);
  
  // 取得した値を電圧に変換 (0〜5000mV)
  tempValue = map(tempValue, 0, 1023, 0, 5000);

  // 変換した電圧を300〜1600の値に変換後、温度に変換 (−30〜100度)
  tempValue = map(tempValue, 300, 1600, -30, 100);

  // 算出した温度を出力
  Serial.println(tempValue);

  delay(100);
}

```

####出力データの確認方法

Serial.printlnなどで出力した内容はシリアルモニタを使用して確認します。
シリアルモニタはArduinoIDEのメニューより[ツール]->[シリアルモニタ]を選択することで起動できます。
<br>
Arduinoのコードを書く画面の右上にある虫メガネマークをクリックしても起動することができます。
起動後、画面右下に転送レートを選択する箇所があるので、その箇所をコードに合わせて変更してください。

サンプルコードの転送レートを設定している箇所
```
Serial.begin(9600);
```

### Raspberry Pi
```python
#!/usr/bin/env python
# coding: utf-8

#
# FaBo Brick Sample
#
# #108 Temperature Brick
#

import spidev
import time
import sys

# A0コネクタにTemperatureを接続
TEMPPIN = 0

# 初期化
spi = spidev.SpiDev()
spi.open(0,0)

def readadc(channel):
	adc = spi.xfer2([1,(8+channel)<<4,0])
	data = ((adc[1]&3) << 8) + adc[2]
	return data

def arduino_map(x, in_min, in_max, out_min, out_max):
	return (x - in_min) * (out_max - out_min) // (in_max - in_min) + out_min

if __name__ == '__main__':
	try:
		while True:
			data = readadc(TEMPPIN)
			volt = arduino_map(data, 0, 1023, 0, 5000)
			temp = arduino_map(volt, 300, 1600, -30, 100)
			print("temp : {:8} ".format(temp))
			time.sleep( 0.5 )
	except KeyboardInterrupt:
		spi.close()
		sys.exit(0)
```

### IchigoJam

#####注意<br>アナログはIN2のみで数値取得可能です。
デジタルの場合はIN(2)、アナログの場合がANA(2)とします。

- デジタル<br>
温度の変化によって0か1を返します。<br>
- アナログ<br>
光の温度化によって0から1023を返します。<br>

```Basic
100 'TEMP_sample_program
110 CLS
120 LOCATE 10,8:PRINT "Digital =";IN(2)
130 LOCATE 10,9:PRINT "Analog  =";ANA(2);"  "
140 GOTO 120
```

画面に数字が2つ表示されます。<br>
それぞれリアルタイムで温度の変化で数値が変化します。
デジタル数値は寒いと0、暖かいと1に変化し、アナログ数値は寒いと小さい値（0に近づく）に、暖かいと大きい値（1023に近づく）に変化します。

## Parts
- IC温度センサ
