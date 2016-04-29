# #113 IR Receiver Brick

<center>![](/img/100_analog/product/113_ir_receiver_product.jpg)
<!--COLORME-->

## Overview
フォトトランジスタを使った赤外線受信Brickです。

I/Oピンから赤外線受信のON/OFFを取得することができます。

## Connecting
### Arduino
アナログコネクタ(A0〜A5)、またはデジタルコネクタ(2〜13)のいずれかに接続します。
![](/img/100_analog/connect/113_ir_receiver_connect.jpg)

### IchigoJam
OUTコネクタのいずれかに接続します。

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|×|◯|

## Schematic
![](/img/100_analog/schematic/113_ir_receiver_schematic.png)

## Sample Code
### for Arduino
A0コネクタに赤外線受信Brick、A1コネクタにLED Brickを接続し、赤外線を受信したらLEDを発光させます。

```c
//
// FaBo Brick Sample
//
// #113 IR Receiver Brick
//

#define ir_receivePin A0
#define ledPin A1

int irState = 0;

void setup() {
  pinMode(ir_receivePin, INPUT);
  pinMode(ledPin, OUTPUT);
}
 
void loop() {
  irState = digitalRead(ir_receivePin);

  if (irState == HIGH) {        
    digitalWrite(ledPin, HIGH);  
  } 
  else {
    digitalWrite(ledPin, LOW); 
  }

}
```

## Parts
- 赤外線フォトトランジスタ

## GitHub
- https://github.com/FaBoPlatform/FaBo/tree/master/113_ir_receive
