# #214 OLED I2C Brick

<center>![](/img/200_i2c/product/214_oled_product.png)
<!--COLORME-->

## Overview
有機ELモジュールを使用したBrickです。

I2Cで表示データを制御できます。

## Connecting
I2Cコネクタへ接続します。

![](/img/200_i2c/connect/214_oled_connect.png)

## Support
| Arduino | RaspberryPI | IchigoJam |
| -- | -- |
| <center>○ | <center>○ | <center>○ |

## Registor
| Slave Address |
| -- |
| 0x3C |

## Datasheet
| Document |
| -- |
|  |

## Schematic
![](/img/200_i2c/schematic/214_oled_schematic.png)

## Sample Code
### for Arduino
このサンプルコードでは外部ライブラリを使用します。

https://github.com/olikraus/u8glib/wiki よりU8glibライブラリをインストールしてください。

```c
//
// FaBo Brick Sample
//
// brick_i2c_oled
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
