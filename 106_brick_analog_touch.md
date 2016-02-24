# #106 Touch Brick
<center>![](/img/100_analog/product/106_touch_product.jpg)
<!--COLORME-->

## Overview
圧力センサーを使用したタッチセンサーBrickです。

I/Oピンより、感圧部分に加えられた力の大きさの変化をアナログ値(0〜1023)で取得することができます。

## Connecting
![](/img/100_analog/connect/106_touch_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Schematic
![](/img/100_analog/schematic/106_touch_schematic.png)

## Sample Code
### Arduino
A0コネクタに接続したTouch Brickの感圧によって、D2コネクタに接続したLED Brickを点灯/消灯させています。

```c
//
// FaBo Brick Sample
//
// brick_analog_touch
//

#define buttonPin A0
#define ledPin D2

int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT); 
  pinMode(ledPin, OUTPUT);         
}

void loop(){
 
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {        
    digitalWrite(ledPin, LOW);  
  } 
  else {
    digitalWrite(ledPin, HIGH); 
  }
}
```

###RaspberryPI
```python
#!/usr/bin/env python
# coding: utf-8

#
# FaBo Brick Sample
#
# #106 Touch Brick
#
# A0コネクタにTouchを接続して、GPIO4コネクタに接続したLED Brickの明るさ調節に使用しています。


import RPi.GPIO as GPIO
import spidev
import time
import sys

# A0コネクタにTouchを接続
TOUCHPIN = 0

# GPIO4コネクタにLEDを接続
LEDPIN = 4

# GPIOポートを設定
GPIO.setwarnings(False)
GPIO.setmode( GPIO.BCM )
GPIO.setup( LEDPIN, GPIO.OUT )

# PWM/100Hzに設定
LED = GPIO.PWM(LEDPIN, 100)

# 初期化
LED.start(0)
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
			data = readadc(TOUCHPIN)
			print("adc : {:8} ".format(data))
			value = arduino_map(data, 0, 1023, 100, 0)
			LED.ChangeDutyCycle(value)
			time.sleep( 0.01 )
	except KeyboardInterrupt:
		LED.stop()
		GPIO.cleanup()
		spi.close()
		sys.exit(0)
```

###IchigoJam
#####注意<br>アナログはIN2のみで数値取得可能です。
デジタルの場合はIN(2)、アナログの場合がANA(2)とします。
```Basic
100 'TOUCH_sample_program
110 CLS
120 LOCATE 10,8:PRINT "Digital =";IN(2)
130 LOCATE 10,9:PRINT "Analog  =";ANA(2);"  "
140 GOTO 120
```
加圧部分に力を加えると数値が変化します。<br>
指で挟んで力んでみてください。<br>
デジタル数値は、圧が強いと0に変化します。


## Parts
- 圧力センサー

