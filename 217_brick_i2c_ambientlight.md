# #217 Ambient Light I2C Brick

<center>![](/img/200_i2c/product/217_ambientlight_product.jpg)
<!--COLORME-->

## Overview
照度センサーを使ったBrickです。

I2Cで明るさを取得することができます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/217_ambientlight_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## ISL29034 Datasheet
| Document |
| -- |
| [ISL29034 Datasheet](http://www.intersil.com/content/dam/Intersil/documents/isl2/isl29034.pdf) |

## Register
| Slave Address |
| -- |
| 0x44 |

## Schematic
![](/img/200_i2c/schematic/217_ambientlight_schematic.png)

## Library
### for Arduino
- [Arduino IDEからインストール](http://fabo.io/library_install.html)

  ライブラリ名：「FaBo 217 Ambient Light ISL29034」

- [Library GitHub](https://github.com/FaBoPlatform/FaBoAmbientLight-ISL29034-Library)
- [Library Document](http://fabo.io/doxygen/FaBoAmbientLight-ISL29034-Library/)

## Sample Code
### for Arduino
上記のArduino Libraryをインストールし、スケッチの例、「FaBo 217 Ambient Light ISL29034」からお選びください。

## Parts
- Intersil ISL29034

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/217_ambientlight
