# #213 LCD mini I2C Brick

<center>![](/img/200_i2c/product/213_lcdmini_product.jpg)
<!--COLORME-->

## Overview
8桁×2行の小さいLCDを使用したBrickです。

I2Cで表示データを制御できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/213_lcdmini_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## AQM0802A Datasheet
| Document |
| -- |
| [AQM0802A Datasheet](http://akizukidenshi.com/catalog/g/gP-06669/) |

## Register
| I2C Slave Address |
|:-- |
| 0x3E |

## Schematic
![](/img/200_i2c/schematic/213_lcdmini_schematic.png)

## Library
### for Arduino
- [Library GitHub](https://github.com/FaBoPlatform/FaBoGPIO-PCAL6408-Library)
- [Library Document](http://fabo.io/doxygen/FaBoGPIO-PCAL6408-Library/)

## Sample Code
### for Arduino
上記のArduino Libraryをインストールし、スケッチの例「FaBo 213 LCD mini AQM0802A」から選択してください。

## Parts
- AQM0802A

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/213_lcd_mini
