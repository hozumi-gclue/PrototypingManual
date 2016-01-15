# #213 LCD mini I2C Brick

<center>![](/img/200_i2c/product/213_lcdmini_product.png)
<!--COLORME-->

## Overview
8桁×2行のちいさいLCDを使用したBrickです。

I2Cで表示データを制御できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/213_lcdmini_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|○|○|○|

## Datasheet
| Document |
| -- |
| [AQM0802A](http://akizukidenshi.com/catalog/g/gP-06669/) |

## Schematic
![](/img/200_i2c/schematic/213_lcdmini_schematic.png)

## Sample Code
### for Arduino
このサンプルコードでは外部ライブラリを使用します。<br>
https://github.com/tomozh/arduino_ST7032
よりライブラリをインストールしてください。

```c
//
// FaBo Brick Sample
//
// 213_lcd_mini
//
// ST7032 Library Download from
//  https://github.com/tomozh/arduino_ST7032
//

#include <Wire.h>
#include <ST7032.h>

ST7032 lcd;

void setup() {
  lcd.begin(8, 2);
  lcd.setContrast(20);
  lcd.print("Hello!");
  delay(3000);
  lcd.clear();
}

void loop() {
  lcd.home();
  lcd.print("FaBo LCD");
  lcd.setCursor(1,1);
  lcd.print(millis()/1000);
}
```

## Parts
- AQM0802A
