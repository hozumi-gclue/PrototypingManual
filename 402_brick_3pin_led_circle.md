# #402 3Pin LED Circle

<center>![](/img/400_led/product/402_ledring_product.png)
<!--COLORME-->

## Overview
RGB Color LEDを使ったBrickです。

## Connecting
![](/img/400_led/connect/402_ledring_connect.png)

A0コネクタに接続します。

## Support
| Arduino | RaspberryPI | IchigoJam |
| -- | -- |
| <center>○ | <center>× | <center>× |

## Schematic
![](/img/400_led/schematic/402_ledring_schematic.png)

## Sample Code
### for Arduino
このサンプルコードでは外部ライブラリを使用します。

https://github.com/adafruit/Adafruit_NeoPixel よりAdafruit_NeoPixelライブラリをインストールしてください。

```c
//
// FaBo Brick Sample
//
// brick_3pin_led
//
// Adafruit_NeoPixel Library Downloads
// https://github.com/adafruit/Adafruit_NeoPixel

#include <Adafruit_NeoPixel.h>

int ledPin = A0;
int numPixels = 12;
Adafruit_NeoPixel pixels = Adafruit_NeoPixel(numPixels, ledPin, NEO_GRB + NEO_KHZ800);

void setup() {
  pixels.begin();
  pixels.show();
}

void loop() {
  int i;
  for(i=0; i<pixels.numPixels(); i++) {
    pixels.setPixelColor(i, pixels.Color(128, 0, 0));
  }
  pixels.show();
  delay(500);

  for(i=0; i<pixels.numPixels(); i++) {
    pixels.setPixelColor(i, pixels.Color(0, 128, 0));
  }
  pixels.show();
  delay(500);

  for(i=0; i<pixels.numPixels(); i++) {
    pixels.setPixelColor(i, pixels.Color(0, 0, 128));
  }
  pixels.show();
  delay(500);

}
```

## Parts
- RGB LED WS2812B

