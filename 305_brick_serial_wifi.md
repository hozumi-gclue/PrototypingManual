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

ATコマンド（基本コマンド）

| AT | テストコマンド |
| AT+RST |　モジュールリセット |
| AT+GMR | ViewVisionInfo |
| AT+GSLP | スリープコマンド |
| ATE | エコーコマンド |
| AT+RFPOWER | RF TXパワー設定 |
| AT+RESTORE | 工場設定にリセット |
| AT+SLEEP | スリープモード |
| 0:8 | 1:8 |
| 0:9 | 1:9 |
| 0:10 | 1:10 |

ATコマンド(Wifiコマンド）

| AT+CWMODE | WIFI mode |
| -- | -- |
| 0:2 | 1:2 |
| 0:3 | 1:3 |
| 0:4 | 1:4 |
| 0:5 | 1:5 |
| 0:6 | 1:6 |
| 0:7 | 1:7 |
| 0:8 | 1:8 |
| 0:9 | 1:9 |
| 0:10 | 1:10 |



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
ArduinoUNOとWifiBruck通信はソフトウェア通信を行っています。115200bps（デフォルト）では文字化けしやすいので、＃305 Wifi BrickとArduinoShield間の通信速度を9600bpsに変更し、Ardunoとパソコン間の通信は115200pbsとします。


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
