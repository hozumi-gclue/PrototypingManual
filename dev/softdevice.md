# SoftDevice


## SoftDeviceとは

Nordicが提供しているnRF5xシリーズ向けの[プロトコルスタック](https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%AD%E3%83%88%E3%82%B3%E3%83%AB%E3%82%B9%E3%82%BF%E3%83%83%E3%82%AF)。  


### nRF51シリーズ  

BLE用はPeripheral用のスタックである[S110](https://developer.nordicsemi.com/nRF51_SDK/nRF51_SDK_v8.x.x/doc/8.0.0/s110/html/index.html)や, Central用のスタックである[S120](https://developer.nordicsemi.com/nRF51_SDK/nRF51_SDK_v8.x.x/doc/8.0.0/s120/html/index.html), Periperal/Centeral用のスタックである[S130](http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.s130.api.v1.0.0%2Findex.html)や、ANT/ANT+用のスタックである[S210](https://developer.nordicsemi.com/nRF51_SDK/nRF51_SDK_v8.x.x/doc/8.0.0/s210/html/index.html)、BLEとANT/ANT+のいずれにも対応した[S310](http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.s310.api.v3.0.0%2Findex.html)
などがそないしている。

ARM® CortexTM-M0向け。

### nRF52シリーズ

52シリーズ向けSoftDeviceは現在(2015/9)開発中で、S130をベースとした[S132](http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.s132.api.v0.9.0%2Findex.html)のAlpha版が提供されている。  ANT/ANT+に対応した[S212](http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.s212.api.v0.9.0%2Findex.html)のAlpha版も提供される。

ARM® Cortex-M4F向け。

### SoftDeviceとnRF51 Software Development Kitの対応表

| nRF51 Software Development Kit | S110 |S120 | S130 | S210 | S310 |
| -- | -- | -- | --- | --- | -- | 
| 10.0.0 | v8.0.0 | v2.1.0 | v1.0.0 | v5.0.0 | v3.0.0 |


### 比較  

| SoftDevice | 概要 |
| -- | -- |
| S110 | Peripheral専用 |
| S120 | Central/Peripheral両用。  Centralモードの場合は8つ同時接続可能、Peripheralモードの場合は同時にBroadcasterとしても動作する。|
| S130 | Central/Peripheral同時利用。 Centralとして３接続と１つのPeripheralとして動作する。こちらはObserverとBroadcaster両方になれる。 |
