# #209 Ktemp I2C Brick

<center>![](/img/200_i2c/product/209_ktemp_product.jpg)
<!--COLORME-->

## Overview
K型熱電対を接続できるBrickです。
I2Cでデータを取得できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/209_ktemp_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Registor
| Slave Address |
| -- |
| 0x68 - 0x6F |
MCP3421のSlave Addressは0x68〜0x6Fのものが存在し、その値は工場出荷時に決まっており、後から変更することはできません。

FaBoBrickでは、0x68、または0x69の２種類を使用しています。

## MCP3421 Datasheet
| Document |
| -- |
| [MCP3421 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/22003e.pdf) |

## Schematic
![](/img/200_i2c/schematic/209_ktemp_schematic.png)

## Library
### for Arduino
- https://github.com/FaBoPlatform/FaBoKTemp-MCP3421-Library

- [Document](http://fabo.io/doxygen/FaBoKTemp-MCP3421-Library/)

## Sample Code
### for Arduino
I2Cコネクタに接続したKtemp BrickにK型熱電対を接続し、熱電対から取得した値を温度に変換してシリアルモニタに出力します。
```c
//
// FaBo Brick Sample
//
// #209 Ktemp I2C Brick
//

#include <Wire.h>

// スレーブデバイスのアドレス
#define DEVICE_ADDR (0x69)

void setup() {
  Serial.begin(9600);
  Serial.println("RESET");

  Wire.begin();
  Wire.beginTransmission(DEVICE_ADDR); 
  Wire.write(0x9f); // 初期設定
  Wire.endTransmission();
}

void loop() {
  int32_t data;
  uint8_t *p = (uint8_t *)&data;
  uint8_t stat;
  double mv;
  int32_t uv;
  uint16_t mvuv = 1 << (3+2*3);
  int cp = 407;  // プローブ補正値
  double temp;

  Wire.requestFrom(DEVICE_ADDR, 4);
  if (Wire.available() != 4) {
    Serial.println("read failed");
    delay(1000);
  }
  for (int8_t i = 2; i >= 0; i--) {
    p[i] = Wire.read();
  }
  p[3] = p[2] & 0x80 ? 0xff : 0;
  stat = Wire.read();
  Wire.endTransmission();

  if ((stat & 0x80) == 0) {
    mv = (double)data/mvuv;
    uv = (data*1000L)/mvuv;
    temp = (uv + cp) / 40.7;
    Serial.print(mv);Serial.print(" mv, ");
    Serial.print(uv);Serial.print(" uv, ");
    Serial.print(temp);Serial.println(" C");
  }

  delay(500);
}
```

### for Raspberry PI

KTemp Brickはデバイスアドレスはサンプルプログラムと異なることがあります。
(0x68〜0x6F)

i2cのセンサーを接続後、下記コマンドにて確認して下さい。

サンプルでは0x69となっていますので、異なる場合は対象のアドレスに変更してご使用下さい。

```
sudo i2cdetect -y 1
```

このサンプルは、I2Cコネクタに接続したKtemp BrickにK型熱電対を接続し、熱電対から取得した値を温度に変換してシリアルモニタに出力します。

```python
# coding: utf-8
#
# FaBo Brick Sample
#
# #209 Ktemp I2C Brick
#

import smbus
import time
  
ADDRESS = 0x69 #MCP3421 device address 環境に合ったデバイスアドレス
CHANNEL = 1
CTLREG = 0x9f
mvuv = 1 << (3+2*3)
cp = 407  #プローブ補正値

class MCP3421:
    def __init__(self, bus, addr):
        self.bus = smbus.SMBus(bus)
        self.addr = addr

    def writebyte(self, cmd, data):
        self.bus.write_byte_data(self.addr, cmd, data)

    def readblock(self, cmd, len):
        return self.bus.read_i2c_block_data(self.addr, cmd, len)
 
if __name__ == '__main__':

    dev = MCP3421(CHANNEL, ADDRESS)

     #初期化
    dev.writebyte(CTLREG,0)

    while True:
          #データ取得
        read_data = dev.readblock(CTLREG, 4)

          #取得データを結合
        data = (read_data[0] << 16) + (read_data[1] << 8) + read_data[2]

          #取得データを温度に変換
        temp = (data *1000/mvuv + cp) / 40.7

          #温度出力
        print "temp:%3.2f C" % (temp)
        print
        time.sleep(1)
```

## Parts
- MCP3421