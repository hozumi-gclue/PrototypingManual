# #205 Proximity I2C Brick

<center>![](/img/200_i2c/product/205_proximity_product.jpg)
<!--COLORME-->

## Overview
近接センサーを使ったBrickです。

I2Cでデータを取得できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/205_proximity_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## VCNL4010 Datasheet
| Document |
|:--|
| [VCNL4010 Datasheet](https://www.adafruit.com/images/product-files/466/vcnl4010.pdf) |

## Register
| I2C Slave Address |
|:-- |
| 0x13 |

## Schematic
![](/img/200_i2c/schematic/205_proximity_schematic.png)

## Library
### for Arduino
- [Arduino IDEからインストール](http://fabo.io/library_install.html)

  ライブラリ名：「FaBo 205 Proximity VCNL4010」

- [Library GitHub](https://github.com/FaBoPlatform/FaBoProximity-VCNL4010-Library)
- [Library Document](http://fabo.io/doxygen/FaBoProximity-VCNL4010-Library/)

## Sample Code
### for Arduino
上記のArduino Libraryをインストールし、スケッチの例から、「FaBo 205 Proximity VCNL4010」→「proximity」を選択してください。

### for Edison
I2Cコネクタに接続したProximity I2C Brickより、センサーから物体までの距離と明るさを取得し、コンソールに出力します。
```js
//
// FaBo Brick Sample
//
// #205 Proximity i2c Brick
//

var m = require('mraa');

var i2c = new m.I2c(0);

i2c.address(0x13);

i2c.writeReg(0x31, 0x00);
i2c.writeReg(0x2d, 0x08);

// Set Enable
i2c.writeReg(0x80, 0x07)
// PROX_RATE
i2c.writeReg(0x82, 0x07);
// LED_CRNT
i2c.writeReg(0x83, 20);
// AMBI_PARM
i2c.writeReg(0x84, 0x7F);

loop();

function loop()
{
    // proximity
    if ( i2c.readReg(0x80) & 0x20 ) {
        var prox_buff = i2c.readBytesReg(0x87, 2);
        var prox = prox_buff[0] << 8 | prox_buff[1];

        console.log("Prox:" + prox);
    }

    // ambient
    if ( i2c.readReg(0x80) & 0x40 ) {
        var ambi_buff = i2c.readBytesReg(0x85, 2);
        var ambi = ambi_buff[0] << 8 | ambi_buff[1];

        console.log("ambi:" + ambi);
    }
    console.log("");
    setTimeout(loop,500);
}
```

## Parts
- Vishay VCNL4010

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/205_proximity
