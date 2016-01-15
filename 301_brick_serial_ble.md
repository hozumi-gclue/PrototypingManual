# #301 BLE Serial Brick
<center>![](/img/300_serial/product/301_ble_product.png)
<!--COLORME-->

## Overview
BLE通信ができるBrickです。

## Connecting
Serialコネクタへ接続します。

![](/img/300_serial/connect/301_ble_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Schematic
![](/img/300_serial/schematic/301_ble_schematic.png)

## Sample Code
### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_serial_ble
//
#include <SoftwareSerial.h>

SoftwareSerial bleShield(10, 11);

long previousMillis = 0;
long interval = 1000; 

void setup()
{
  // BLEとの通信用
  bleShield.begin(9600);
  // ログ出力用
  Serial.begin(9600);
  Serial.write("start!");
}

void loop()
{
  // 一定時間ごとにコマンド実行
  unsigned long currentMillis = millis();
  if(currentMillis - previousMillis > interval) {
    Serial.write("*\n");

    previousMillis = currentMillis;   

    // アドバタイズ開始 (026100が返って来れば成功、BLEを検索すると見つかります)
    bleShield.write((byte)0x06);
    bleShield.write((byte)0x00);
    bleShield.write((byte)0x02);
    bleShield.write((byte)0x06);
    bleShield.write((byte)0x01);
    bleShield.write((byte)0x02);
    bleShield.write((byte)0x02);

  }
  // 返答を出力
  while (bleShield.available()) {
    Serial.print(bleShield.read(), HEX);
  }
}
```

## Parts
- BluetoothLE ModuleIC