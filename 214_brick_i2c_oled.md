# #214 OLED I2C Brick

<center>![](/img/200_i2c/product/214_oled_product.jpg)
<!--COLORME-->

## Overview
有機ELモジュールを使用したBrickです。

I2Cで表示データを制御できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/214_oled_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## ER-OLED0.96 Datasheet
| Document |
| -- |
| [ER-OLED0.96 Datasheet](http://www.buydisplay.com/download/manual/ER-OLED0.96_Series_Datasheet.pdf) |

## Register
| Slave Address |
| -- |
| 0x3C |

## Schematic
![](/img/200_i2c/schematic/214_oled_schematic.png)

## Sample Code
### for Arduino
I2Cコネクタに接続したOLED Brickに、「FaBo」を表示します。

このサンプルコードでは外部ライブラリを使用します。

https://github.com/olikraus/u8glib/wiki よりU8glibライブラリをインストールしてください。

```c
//
// FaBo Brick Sample
//
// #214 OLED I2C Brick
//
// U8glib Library Downloads
// https://github.com/olikraus/u8glib/wiki

#include "U8glib.h"

U8GLIB_SSD1306_128X64 u8g(U8G_I2C_OPT_NONE);	

void draw() {
  u8g.setFont(u8g_font_unifont);
  u8g.drawStr( 0, 20, "FaBo");
}

void setup() {
}

void loop() {
  u8g.firstPage();  
  do {
    draw();
  } while( u8g.nextPage() );
    delay(1000);
}

```

## Parts
- 128x96 0.96OLED Module

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/214_oled
