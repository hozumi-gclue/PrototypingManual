# #214 OLED I2C Brick

<center>![](/img/200_i2c/product/214.jpg)
<!--COLORME-->

## Overview
有機ELモジュールを使用したBrickです。

I2Cで表示データを制御できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/214_oled_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## ER-OLED0.96 Datasheet
| Document |
| -- |
| [ER-OLED0.96 Datasheet](http://www.buydisplay.com/download/manual/ER-OLED0.96_Series_Datasheet.pdf) |

## Register
| Slave Address |
| -- |
| 0x3C |

## Schematic
![](/img/200_i2c/schematic/214_oled.png)

## Library
### for Arduino
- [Arduino IDEからインストール](http://fabo.io/library_install.html)

  ライブラリ名：「FaBo 214 OLED EROLED096」

- [Library GitHub](https://github.com/FaBoPlatform/FaBoOLED-EROLED096-Library)
- [Library Document](http://fabo.io/doxygen/FaBoOLED-EROLED096-Library)

## Sample Code
### for Arduino
上記のArduino Libraryをインストールし、スケッチの例、「FaBo 214 OLED EROLED096」からお選びください。

### for Ichigojam
I2CコネクタにOLED I2C Brickを接続し、文字を表示します。

```
30 CLS
110 D=#3C

210 POKE #800,0,#40,#B0,#21,0,127
220 'Init data set
230 POKE #810,#AE,#D5,#80,#A8,#3F,#D3,#00,#40,#8D,#14,#A1,#C8,#DA,#12,#81,#CF,#D9,#F1,#DB,#20,#A4,#A6,#AF

250 'output data
260 POKE#840,#40,#48,#48,#48,#7F:'F
270 POKE#850,#0F,#15,#15,#15,#02:'a
280 POKE#860,#36,#49,#49,#49,#7F:'B
290 POKE#870,#0E,#11,#11,#11,#0E:'o

300 ?"Init"
310 FOR B=0 TO 23
320  A=I2CW(D,#800,1,#810+B,1)
330 NEXT

400 ?"Clear Display"
410 FOR I=0 TO 7
420  POKE #802,#B0|I
430  A=I2cW(D,#800,1,#802,4)
440  FOR J=0 TO 127
450   A=I2CW(D,#801,1,#800,1)
460  NEXT
470 NEXT

500 POKE #802,#B0+I,21
510 A=I2CW(D,#800,1,#802,5)

600 ?"Output"
620 FOR l=0 TO 4
630  GSB 700
640 NEXT
650 ?"End"
660 END

700 A=I2CW(D,#801,1,#800,1)
710 A=I2CW(D,#801,1,#800,1)
720 A=I2cW(D,#801,1,#870-l*16,1)
730 A=I2cW(D,#801,1,#871-l*16,1)
740 A=I2cW(D,#801,1,#872-l*16,1)
750 A=I2cW(D,#801,1,#873-l*16,1)
760 A=I2cW(D,#801,1,#874-l*16,1)
770 A=I2CW(D,#801,1,#800,1)
780 RTN
```

## Parts
- 128x96 0.96OLED Module

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/214_oled
