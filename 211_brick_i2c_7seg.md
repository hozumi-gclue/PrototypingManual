# #211 7Segment LED I2C Brick

<center>![](/img/200_i2c/product/211_7seg_product.png)
<!--COLORME-->

## Overview
７セグメントLEDを使ったBrickです。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/211_7seg_connect.jpg)

I2C拡張ボードを使用して複数の7セグメントBrickを接続する場合は、Brick裏にあるソルダージャンパーでI2Cアドレスを変更します。

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Registor
| A0 | A1 | A2 | Slave Address |
| -- | -- | -- | -- |
| LOW | LOW | LOW | 0x20 |

FaBo Brickでは、初期値に0x20が設定されています。Brick裏面のソルダージャンパーで設定を変更できます。

## Datasheet
| Document |
| -- |
| [Datasheet](http://www.ti.com/jp/lit/gpn/tlc59208f) |

## Schematic
![](/img/200_i2c/schematic/211_7seg_schematic.png)

## Sample Code
PWM出力値は、"0x02"でほぼ視認できる明るさで点灯されます。あまり高い数値にすると、点灯しなくなるおそれがあります。


### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_i2c_7seg
//

#include <Wire.h>

#define ADDR0 0x20

void setup() {
  Wire.begin(); 
  Serial.begin(9600); 
  Serial.println(); 
  Serial.println("RESET");
  ini(ADDR0);
}

void loop() {
  for (int i = 0; i<12; i++) {
    Serial.println(i) ; 
    show(ADDR0, i);
    delay(500);
  }
}

void show(byte addr, int num){
  unsigned char PWM_Value = 0x02;
  switch (num) {
    case 0:
      // 0:ABCDEF
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(PWM_Value); // PWM0 E
      Wire.write(PWM_Value); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(PWM_Value); // PWM6 F
      Wire.write(0x00); // PWM7 G
      Wire.endTransmission();
      break;
    case 1:
      // 1:BC
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(0x00); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(0x00); // PWM5 A
      Wire.write(0x00); // PWM6 F
      Wire.write(0x00); // PWM7 G
      Wire.endTransmission();
      break;
    case 2:
      // 2:ABDEG
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(PWM_Value); // PWM0 E
      Wire.write(PWM_Value); // PWM1 D
      Wire.write(0x00); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(0x00); // PWM6 F
      Wire.write(PWM_Value); // PWM7 G
      Wire.endTransmission();
      break;
    case 3:
      // 3:ABCDG
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(PWM_Value); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(0x00); // PWM6 F
      Wire.write(PWM_Value); // PWM7 G
      Wire.endTransmission();
      break;
    case 4:
      // 4:BCFG
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(0x00); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(0x00); // PWM5 A
      Wire.write(PWM_Value); // PWM6 F
      Wire.write(PWM_Value); // PWM7 G
      Wire.endTransmission();
      break;
    case 5:
      // 5:ACDFG
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(PWM_Value); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(0x00); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(PWM_Value); // PWM6 F
      Wire.write(PWM_Value); // PWM7 G
      Wire.endTransmission();
      break;
    case 6:
      // 6:ACDEFG
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(PWM_Value); // PWM0 E
      Wire.write(PWM_Value); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(0x00); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(PWM_Value); // PWM6 F
      Wire.write(PWM_Value); // PWM7 G
      Wire.endTransmission();
      break;
    case 7:
      // 7:ABCF
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(0x00); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(PWM_Value); // PWM6 F
      Wire.write(0x00); // PWM7 G
      Wire.endTransmission();
      break;
    case 8:
      // 8:ABCDEFG
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(PWM_Value); // PWM0 E
      Wire.write(PWM_Value); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(PWM_Value); // PWM6 F
      Wire.write(PWM_Value); // PWM7 G
      Wire.endTransmission();
      break;
    case 9:
      // 9:ABCDFG
      Wire.beginTransmission(addr);
       Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(PWM_Value); // PWM1 D
      Wire.write(PWM_Value); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(PWM_Value); // PWM4 B
      Wire.write(PWM_Value); // PWM5 A
      Wire.write(PWM_Value); // PWM6 F
      Wire.write(PWM_Value); // PWM7 G
      Wire.endTransmission();
      break;
    case 10:
      // Dot
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(0x00); // PWM1 D
      Wire.write(0x00); // PWM2 C
      Wire.write(PWM_Value); // PWM3 DP
      Wire.write(0x00); // PWM4 B
      Wire.write(0x00); // PWM5 A
      Wire.write(0x00); // PWM6 F
      Wire.write(0x00); // PWM7 G
      Wire.endTransmission();
      break;
    default:
      // off
      Wire.beginTransmission(addr);
      Wire.write(0xA2);
      Wire.write(0x00); // PWM0 E
      Wire.write(0x00); // PWM1 D
      Wire.write(0x00); // PWM2 C
      Wire.write(0x00); // PWM3 DP
      Wire.write(0x00); // PWM4 B
      Wire.write(0x00); // PWM5 A
      Wire.write(0x00); // PWM6 F
      Wire.write(0x00); // PWM7 G
      Wire.endTransmission();
      break;
  }

}

void ini(byte addr){
  Wire.beginTransmission(addr);
  Wire.write(0x80); //
  Wire.write(0x81); // MODE1
  Wire.write(0x03); // MODE2
  Wire.write(0x00); // PWM0
  Wire.write(0x00); // PWM1
  Wire.write(0x00); // PWM2
  Wire.write(0x00); // PWM3
  Wire.write(0x00); // PWM4
  Wire.write(0x00); // PWM5
  Wire.write(0x00); // PWM6
  Wire.write(0x00); // PWM7
  Wire.write(0xFF); // GRPPWM
  Wire.write(0x00); // GRPFREQ
  Wire.write(0xAA); // LEDOUT0
  Wire.write(0xAA); // LEDOUT1
  Wire.write(0x92); // SUBADR1
  Wire.write(0x94); // SUBADR2
  Wire.write(0x98); // SUBADR3
  Wire.write(0xD0); // ALLCALLADR
  Wire.endTransmission();
}
```
### for RaspberryPI
```python
# coding: utf-8
#
# FaBo Brick Sample
#
# brick_i2c_7seg
#

import smbus
import time
  
ADDRESS = 0x20 #TLC59208F device address
CHANNEL = 1

INIT   = 0x80    #設定用
SEGSET = 0xA2    #7segLEDへ出力設定
VALUE  = 0x01    #LED点灯設定
ZERO   = 0x00    #LED消灯設定

#初期設定用
init_set = [0x81, #MODE1 
            0x03, #MODE2
            0x00, #PWM0
            0x00, #PWM1
            0x00, #PWM2
            0x00, #PWM3
            0x00, #PWM4
            0x00, #PWM5
            0x00, #PWM6
            0x00, #PWM7
            0xFF, #GRPPWM
            0x00, #GRPREQ
            0xAA, #LEDOUT0
            0xAA, #LEDOUT1
            0x92, #SUBADR1
            0x94, #SUBADR2
            0x98, #SUBADR3
            0xD0] #ALLCALLADR

#数値出力用
set = [[VALUE,  #PWM0  [0]出力用の設定値 (set[0][0:])
        VALUE,  #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        VALUE,  #PWM5              
        VALUE,  #PWM6              
        ZERO]   #PWM7
         ,
       [ZERO,   #PWM0  [1]出力用の設定値 (set[1][0:])
        ZERO,   #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        ZERO,   #PWM5              
        ZERO,   #PWM6              
        ZERO]   #PWM7
         ,
       [VALUE,  #PWM0  [2]出力用の設定値 (set[2][0:])
        VALUE,  #PWM1
        ZERO,   #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        VALUE,  #PWM5              
        ZERO,   #PWM6              
        VALUE]  #PWM7
         ,
       [ZERO,   #PWM0  [3]出力用の設定値 (set[3][0:])
        VALUE,  #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        VALUE,  #PWM5              
        ZERO,   #PWM6              
        VALUE]  #PWM7
         ,
       [ZERO,   #PWM0  [4]出力用の設定値 (set[4][0:])
        ZERO,   #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        ZERO,   #PWM5              
        VALUE,  #PWM6              
        VALUE]  #PWM7
         ,
       [ZERO,   #PWM0  [5]出力用の設定値 (set[5][0:])
        VALUE,  #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        ZERO,   #PWM4              
        VALUE,  #PWM5              
        VALUE,  #PWM6              
        VALUE]  #PWM7
         ,
       [VALUE,  #PWM0  [6]出力用の設定値 (set[6][0:])
        VALUE,  #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        ZERO,   #PWM4              
        VALUE,  #PWM5              
        VALUE,  #PWM6              
        VALUE]  #PWM7
         ,
       [ZERO,   #PWM0  [7]出力用の設定値 (set[7][0:])
        ZERO,   #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        VALUE,  #PWM5              
        VALUE,  #PWM6              
        ZERO]   #PWM7
         ,
       [VALUE,  #PWM0  [8]出力用の設定値 (set[8][0:])
        VALUE,  #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        VALUE,  #PWM5              
        VALUE,  #PWM6              
        VALUE]  #PWM7
         ,
       [ZERO,   #PWM0  [9]出力用の設定値 (set[9][0:])
        VALUE,  #PWM1
        VALUE,  #PWM2
        ZERO,   #PWM3
        VALUE,  #PWM4              
        VALUE,  #PWM5              
        VALUE,  #PWM6              
        VALUE]  #PWM7
         ,
       [ZERO,   #PWM0  [.]出力用の設定値 (set[10][0:])
        ZERO,   #PWM1
        ZERO,   #PWM2
        VALUE,  #PWM3
        ZERO,   #PWM4              
        ZERO,   #PWM5              
        ZERO,   #PWM6              
        ZERO]   #PWM7
         ]

if __name__ == '__main__':

    bus = smbus.SMBus(CHANNEL)

     #初期設定
    bus.write_i2c_block_data(ADDRESS,INIT,init_set)

    time.sleep(0.5)

    while True:
        for num in range(0 , 11):
           #ログ出力
           print "output:%d" % (num)
           #7segLEDへの表示
           bus.write_i2c_block_data(ADDRESS,SEGSET,set[num][0:])
 
           time.sleep(1)
```

## Parts
- 7セグメントLED
- I2C LEDドライバIC
