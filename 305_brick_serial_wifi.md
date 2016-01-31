# #305 Wifi Serial Brick

<center>![](/img/300_serial/product/305_wifi_product.jpg)
<!--COLORME-->

## Overview
Wifi通信ができるBrickです。

## Connecting
Serialコネクタに接続します。
![](/img/300_serial/connect/305_wifi_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
| | | |

## Schematic
![](/img/300_serial/schematic/305_wifi_schematic.png)

####ATコマンド（基本コマンド）
|  |コマンド名  | レスポンス |
| -- | -- | -- |
| テスト | AT | OK |
| ファームウェアのバーション表示 | AT+GMR | バーション表示 |
| コマンドエコー設定 | ATE1 | OK |
| 0:5 | 1:5 | 2:5 |
| 0:6 | 1:6 | 2:6 |
| 0:7 | 1:7 | 2:7 |
| 0:8 | 1:8 | 2:8 |
| 0:9 | 1:9 | 2:9 |
| 0:10 | 1:10 | 2:10 |




####ATコマンド(Wifiコマンド）
|  |コマンド名  | 正常レスポンス |
| -- | -- | -- |
| アクセスポイント一覧 | AT+CWLAP | OK |
| ファームウェアのバーション表示 | AT+GMR | バーション表示 |
| コマンドエコー設定 | ATE1 | OK |
| アクセスポイントに接続| AT+CWJAP | WIFICONNECTED |
| アクセスポイント確認 | AT+CWSAP | SSID名,電波強度,Macアドレス,0:キーなし 2:WPA 3:WPA2  4:WPA_WPA2  |
| 0:7 | 1:7 | 2:7 |
| 0:8 | 1:8 | 2:8 |
| 0:9 | 1:9 | 2:9 |
| 0:10 | 1:10 | 2:10 |





## Sample Code
### for Arduino
Arduino IDEでコマンド入力できる。
```
#include <SoftwareSerial.h>

int bluetoothRx = 13;  // RX-I pin of bluetooth mate, Arduino D11
int bluetoothTx = 12;  // TX-O pin of bluetooth mate, Arduino D10

SoftwareSerial mySerial(bluetoothRx, bluetoothTx); // RX, TX

void setup()  
{
  // Open serial communications and wait for port to open:
  Serial.begin(115200);
  while (!Serial) {
    ; // wait for serial port to connect. Needed for Leonardo only
  }

  Serial.println("Goodnight moon!");

  // set the data rate for the SoftwareSerial port
  mySerial.begin(115200);
}
int c = 0;
void loop() // run over and over
{
  if (mySerial.available()){
    char c = mySerial.read();
    Serial.write(c);

  }
  if (Serial.available())
    mySerial.write(Serial.read());
}
```

### for Arduino
ArduinoUNOとWifiBruckとの通信はソフトウェアシリアル通信を行っています。115200bps（デフォルト）では文字化けしやすいので、＃305 Wifi BrickとArduinoShield間の通信速度を9600bpsに変更し、Ardunoとパソコン間のハードウェアシリアル通信は115200pbsとします。


```
//
// FaBo Brick Sample 2
//
// Wifi Brick
// 115200bps→9600bps
#include <SoftwareSerial.h>
#define TimeInterval 2000
#define ComminucationSpeed_Arduino 9600
#define ComminucationSpeed_bleShield 9600

int bluetoothRx = 13; 
int bluetoothTx = 12; 

SoftwareSerial bleShield(bluetoothRx, bluetoothTx);



void setup()
{
  Serial.begin(ComminucationSpeed_Arduino);
  while (!Serial) {
  }

  Serial.println("bps changed!");

  // set the data rate for the SoftwareSerial port
  bleShield.begin(ComminucationSpeed_bleShield);
}

void ResposeCatch(){
  while(bleShield.available()){
  Serial.write(bleShield.read());
  bleShield.write(Serial.read());
   }
   delay(TimeInterval);
}

void loop()
{
  ResposeCatch();
   delay(TimeInterval);
 
   bleShield.println("AT+UART_DEF=9600,8,1,0,0");
   ResposeCatch();
   Serial.println("Excute");
   while(1){
    }

}
```

## Parts
