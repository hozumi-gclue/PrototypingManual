# #307 BLE Nordic Serial Brick

<center>
![](/img/300_serial/product/307.jpg)
<!--COLORME-->

## Overview
NRF51モジュールを使用したBLE（Bluetooth Low Energy）のBrickです。

シリアルにて制御できるFirmwareが書き込まれているため、Arduino等からシリアル通信にてBLEを制御することができます。

BLEの転送レートは115200bpsに設定してあります。

## Connecting
Serialコネクタへ接続します。

![](/img/300_serial/connect/307_ble_nordic_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|◯|×|

## MDBT40 Datasheet

|Document|
|--|
|[MDBT40 Datasheet](http://www.raytac.com/download/MDBT40/MDBT40%20spec-Version%20A4.pdf)|

## Schematic
![](/img/300_serial/schematic/307_ble_nordic.png)

## Library

### for Arduino
- [Arduino IDEからインストール](http://fabo.io/library_install.html)

  ライブラリ名：「FaBo 307 BLE Nordic」

- [Library GitHub](https://github.com/FaBoPlatform/FaBoBLE-Nordic-Library)
- [Library Document](http://fabo.io/doxygen/FaBoBLE-Nordic-Library/)


## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/307_ble_nordic
