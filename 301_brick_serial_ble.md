# #301 BLE Serial Brick
<center>![](/img/300_serial/product/301_ble_product.jpg)
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

SoftwareSerial bleShield(12, 13);

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
### for Arduino(Scan)
```c
//
// FaBo Brick Sample
//
// Scan
//
#include <SoftwareSerial.h>

SoftwareSerial bleShield(12, 13);

long previousMillis = 0;
long interval = 1000; 

void setup()
{
  // BLEとの通信用
  bleShield.begin(9600);
  // ログ出力用
  Serial.begin(9600);
  Serial.write("Scan start!");
}

void loop()
{
  // 一定時間ごとにコマンド実行
  unsigned long currentMillis = millis();
  if(currentMillis - previousMillis > interval) {
    Serial.write("*\n");

    previousMillis = currentMillis;   

    //***Set Scan Parameters***
    //Byte
    bleShield.write((byte)0x09);
    //hilen
    bleShield.write((byte)0x00);
    //lolen
    bleShield.write((byte)0x05);
    //class
    bleShield.write((byte)0x06);
    //method
    bleShield.write((byte)0x07);
    //scan_interval 0x4 -0x4000
    bleShield.write((byte)0x40);
    bleShield.write((byte)0x00);
    //scan_window 0x4 - 0x4000
    bleShield.write((byte)0x40);
    bleShield.write((byte)0x00);
    //active 0 Passive scanning,1 Active scanning
    bleShield.write((byte)0x01);
    //***Discover***
    //Byte
    bleShield.write((byte)0x05);
    //hilen
    bleShield.write((byte)0x00);
    //lolen
    bleShield.write((byte)0x01);
    //class
    bleShield.write((byte)0x06);
    //method
    bleShield.write((byte)0x02);
    //mode GAP DiscoverMode
    //gap_non_discoverable      0
    //gap_limited_discoverable  1
    //gap_general_discoverable  2
    //gap_broadcast             3
    //gap_user_data             4
    //gap_enhanced_broadcasting 0x80
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