# #301 BLE Serial Brick
<center>![](/img/300_serial/product/301_ble_product.jpg)
<!--COLORME-->

## Overview
BLE113を使用したBLE（Bluetooth Low Energy）のBrickです。
シリアルにて制御できるFirmwareが書き込まれているため、Arduino等からシリアル通信にてBLEを制御することができます。

BLEの転送レートは9600bpsに設定してあります。

## Connecting
Serialコネクタへ接続します。

Arduino、RaspberryPI、IchigojamのOUT/INシールドは、Serialコネクタが１箇所ずつ存在します。

![](/img/300_serial/connect/301_ble_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|◯|

## Schematic
![](/img/300_serial/schematic/301_ble_schematic.png)

## Sample Code
### for Arduino(Advertise)
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
// brick_serial_ble_scan
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

    // 検索開始 (02620が返って来れば成功、BLEを検索します。)
    bleShield.write((byte)0x05);
    bleShield.write((byte)0x00);
    bleShield.write((byte)0x01);
    bleShield.write((byte)0x06);
    bleShield.write((byte)0x02);
    bleShield.write((byte)0x02);
    delay(1000);
  }
  int count = 0;
  // 返答を出力
  while (bleShield.available()) {
    if (count==5){
      Serial.write('\n');
    }    
    Serial.print(bleShield.read(), HEX);
    count++;

  }
  delay(100);
  
  // 検索終了 (02640が返って来れば成功、検索を終了します)
  bleShield.write((byte)0x04);
  bleShield.write((byte)0x00);
  bleShield.write((byte)0x00);
  bleShield.write((byte)0x06);
  bleShield.write((byte)0x04);
  delay(100);
  // 返答を出力
  Serial.write('\n');
  while (bleShield.available()) {
    Serial.print(bleShield.read(), HEX);
  }
  Serial.write('\n');
}
```

## Parts
- BluetoothLE ModuleIC