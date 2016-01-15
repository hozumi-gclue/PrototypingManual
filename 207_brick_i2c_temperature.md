# #207 Temperature I2C Brick

<center>![](/img/200_i2c/product/207_temperature_product.png)
<!--COLORME-->

## Overview
温度センサを使用したBrickです。
I2Cでデータを取得できます。

計測できる範囲は−55度〜150度です。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/207_temperature_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Registor
| Slave Address |
| -- |
| 0x48 |

## Datasheet
| Document |
| -- |
| [Datasheet](http://www.analog.com/media/en/technical-documentation/data-sheets/ADT7410.pdf) |

## Schematic

![](/img/200_i2c/schematic/207_temperature_schematic.png)

## Sample Code
### Arduino
```c
//
// FaBo Brick Sample
//
// brick_i2c_temperature
//

#include <Wire.h>
#define DEVICE_ADDR (0x48)

void setup() {
  Serial.begin(9600);
  Wire.begin();
 
  Wire.beginTransmission(DEVICE_ADDR);
  Wire.write(0x03);
  Wire.write(0x80);
  Wire.endTransmission();
 
}
 
void loop() {
  uint16_t val;
  float tmp;
  long  l_val;
  
  Wire.requestFrom(DEVICE_ADDR, 2);
  
  val = (uint16_t)Wire.read() << 8;   // read(上位8bit)
  val |= Wire.read();                 // read(下位8bit)
 
  l_val = (long)val;
  if(val & 0x8000) {         // 符号の判定    
    l_val = l_val - 65536;     // マイナスの場合
  }
 
  tmp = (float)l_val * 0.0078125;   // ival / 128

  Serial.print("tmp:");
  Serial.println(tmp);
  delay(500);
}

```

### RaspberryPI

```python
# coding: utf-8
#
# FaBo Brick Sample
#
# brick_i2c_temp
#

import smbus
import time
  
ADDRESS = 0x48 #ADT7410 device address
CHANNEL  = 1

class ADT7410:
    def __init__(self, bus, addr):
        self.bus = smbus.SMBus(bus)
        self.addr = addr

    def readblock(self, cmd, len):
        return self.bus.read_i2c_block_data(self.addr, cmd, len)
 
if __name__ == '__main__':

    dev = ADT7410(CHANNEL, ADDRESS)

    while True:
        #データ取得
        read_data = dev.readblock(0x00, 12)
        #上位2バイトのみ取得し、温度データに加工
        temp = (read_data[0] << 8 | read_data[1]) >> 3

        #マイナスの場合の処理
        if(temp >= 4096):
            temp -= 8192;

        #温度出力
        print "temp:%4.2f" % (temp / 16.0)
        print
        time.sleep(1)
```

### IchigoJam

```basic
コードはここに書く
```


## Parts
- 16bit温度センサーIC
