# #208 Humidity I2C Brick

<center>![](/img/200_i2c/product/208_humidity_product.jpg)
<!--COLORME-->

## Overview
湿度センサを使用したBrickです。
I2Cでデータを取得できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/208_humidity_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Registor
| Slave Address |
| -- |
| 0x5F |

## HTS221 Datasheet
| Document |
| -- |
| [HTS221 Datasheet](http://www2.st.com/content/ccc/resource/technical/document/datasheet/4d/9a/9c/ad/25/07/42/34/DM00116291.pdf/files/DM00116291.pdf/jcr:content/translations/en.DM00116291.pdf) |

## Schematic
![](/img/200_i2c/schematic/208_humidity_schematic.png)

## Library
### for Arduino
- ArduinoIDEのライブラリマネージャからインストールできます。ライブラリ名称は「FaBo 208 Humidity HTS221」です。
- [ライブラリマネージャからのインストール方法](http://fabo.io/library_install.html)
- [GitHub Repository](https://github.com/FaBoPlatform/FaBoHumidity-HTS221-Library)
- [Document](http://fabo.io/doxygen/FaBoHumidity-HTS221-Library/)

## Sample Code
### Arduino
上記のArduino Libraryをインストールし、スケッチの例から、「FaBo 208 Humidity HTS221」→「humidity」を選択してください。


## Parts
- HTS221