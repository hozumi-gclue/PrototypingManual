# #210 GPIO I2C Brick

<center>![](/img/200_i2c/product/210_gpio_product.png)
<!--COLORME-->

## Overview
汎用I/O拡張チップを使用したBrickです。

I2Cで8個のLEDを制御できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/210_gpio_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|○|○|○|

## Registor
| Slave Address |
| -- |
| 0x20 |

## Datasheet
| Document |
| -- |
| [Datasheet](http://www.jp.nxp.com/documents/data_sheet/PCAL6408A.pdf) |

## Schematic
![](/img/200_i2c/schematic/210_gpio_schematic.png)

## Sample Code
### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_i2c_gpio
//

#include <Wire.h>

#define DEVICE_ADDR 0x20 // スレーブデバイスのアドレス

void setup() {
  Wire.begin(); // I2C開始

  Serial.begin(9600);
  Serial.println();
  Serial.println("RESET");
  Serial.println();

  Wire.beginTransmission(DEVICE_ADDR); // 初期化
  Wire.write(0x03);
  Wire.write(0x00);
  Wire.endTransmission();
}

void loop() {
  int c = 1;

  for (int i=0; i<8; i++) {
    Serial.println(c);
    Wire.beginTransmission(DEVICE_ADDR); // 順番に点滅させる
    Wire.write(0x01);
    Wire.write(c);
    Wire.endTransmission();
    c = c << 1;
    delay(100);
  }

}

```

## Parts
- 汎用I/O拡張IC
