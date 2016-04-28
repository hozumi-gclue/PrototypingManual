# #212 LCD I2C Brick

<center>![](/img/200_i2c/product/212_lcd_product.jpg)
<!--COLORME-->

## Overview
LCDを使用したBrickです。

I2Cで表示データを制御できます。


## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/212_lcd_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## PCF8574 Datasheet
| Document |
|:--|
| [PCF8574 Datasheet](http://www.tij.co.jp/jp/lit/ds/symlink/pcf8574.pdf) |

## Register
| A0 | A1 | A2 | Slave Address |
| -- | -- | -- | -- |
| LOW | LOW | LOW | 0x20 |

FaBo Brickでは、初期値に0x20が設定されています。Brick表面のソルダージャンパーで設定を変更できます。

## Schematic
![](/img/200_i2c/schematic/212_lcd_schematic.png)

## Parts
- PCF8574
- LCD 1602A

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/212_lcd
