# #203 Color Sensor I2C Brick

<center>![](/img/200_i2c/product/203_color_product.png)
<!--COLORME-->

## Overview
カラーセンサを使用したBrickです。

センサーより読み取った赤、緑、青、赤外線(明るさ)の4つのデータを、I2Cにて取得することができます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/203.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|○|○|○|

## Registor
| Slave Address |
| -- |
| 0x2A |

## Datasheet
| Document |
| -- |
| [Datasheet](http://www.hamamatsu.com/resources/pdf/ssd/s11059-02dt_etc_kpic1082j.pdf) |

## Schematic
![](/img/200_i2c/schematic/203_color_schematic.png)

## Sample Code
### Arduino

```c
//
// FaBo Brick Sample
//
// brick_i2c_color
//
#include <Wire.h>

#define DEVICE_ADDR 0x2A // スレーブデバイスのアドレス
#define CTLREG 0x00      

uint16_t red = 0;
uint16_t green = 0;
uint16_t blue = 0;
uint16_t infrared = 0;

void setup()
{
  Serial.begin(9600); //シリアル開始 表示用
  Wire.begin();       //I2C開始
}

void loop()
{
  //色の取得
  getColor();

  //色の出力
  Serial.print("R:[");
  Serial.print(red);
  Serial.print("] G:[");
  Serial.print(green);
  Serial.print("] B:[");
  Serial.print(blue);
  Serial.print("] IR:[");
  Serial.print(infrared);
  Serial.println("]");

  delay(500);
}

void getColor()
{
  uint16_t color= 0;

  // 待機解除
  Wire.beginTransmission(DEVICE_ADDR);
  Wire.write(CTLREG);
  Wire.write(0x83); // ADC reset wakeup
  Wire.endTransmission(false);

  Wire.beginTransmission(DEVICE_ADDR);
  Wire.write(CTLREG);
  Wire.write(0x03);
  Wire.endTransmission(true);

  delay(500);

  Wire.beginTransmission(DEVICE_ADDR);
  Wire.write(0x03);
  Wire.endTransmission(false);

  Wire.requestFrom(0x2A,8,true);
 
  //色データの取得

  // 赤
  color = Wire.read() << 8;
  color |= Wire.read();
  red = color;

  // 緑
  color =0;
  color = Wire.read() << 8;
  color |= Wire.read();
  green = color;

  // 青
  color =0;
  color = Wire.read() << 8;
  color |= Wire.read();
  blue = color;

  // 赤外
  color =0;
  color = Wire.read() << 8;
  color |= Wire.read();
  infrared = color;

  return;
}
```

### RaspberryPI

```python
# coding: utf-8
#
# FaBo Brick Sample
#
# brick_i2c_color
#

import smbus
import time
  
ADDRESS = 0x2A #S11059 device address
CHANNEL = 1
CTLREG = 0x00
OUTREG = 0x03
RESET = 0x83
RESTART = 0x03

class S11059:
    def __init__(self, bus, addr):
        self.bus = smbus.SMBus(bus)
        self.addr = addr

    def writebyte(self, cmd, data):
        self.bus.write_byte_data(self.addr, cmd, data)

    def readblock(self, cmd, len):
        return self.bus.read_i2c_block_data(self.addr, cmd, len)
 
if __name__ == '__main__':

    dev = S11059(CHANNEL, ADDRESS)

     #初期化
    dev.writebyte(CTLREG,RESET)
    dev.writebyte(CTLREG,RESTART)

    time.sleep(2.5)

    dev.writebyte(OUTREG,CTLREG)

    while True:
        #データ取得
        read_data = dev.readblock(CTLREG, 11)

        #データ設定
        red = read_data[3] << 8 | read_data[4]
        green = read_data[5] << 8 | read_data[6]
        blue = read_data[7] << 8 | read_data[8]
        infrared = read_data[9] << 8 | read_data[10]

        #データ出力
        print "R:%x G:%x B:%x I:%x" % (red,green,blue,infrared)
        print
        time.sleep(0.5)
```

### IchigoJam

```basic
ここにコード書く
```

## Parts
- S11059
