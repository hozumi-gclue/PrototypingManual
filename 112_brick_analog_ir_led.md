# #112 IR LED Brick

<center>![](/img/100_analog/product/112_ir_product.jpg)
<!--COLORME-->

## Overview
赤外線LEDを使ったBrickです。

I/Oピンから赤外線LEDをON/OFFを制御することができます。

## Connecting 1
A0コネクタに赤外線LED Brick、A1コネクタにボタンBrickを接続し、ボタンが押されたら赤外線LEDを発光させます。

![](/img/100_analog/connect/112_ir_connect.jpg)

## Support
|Arduino|RaspberryPI|IchigoJam|
|:--:|:--:|:--:|
|◯|×|◯|

## Schematic
![](/img/100_analog/schematic/112_ir_schematic.png)

## Sample Code
### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_analog_ir_led
//

int ir_ledPin = A0;
int buttonPin = A1;

int buttonState = 0;

void setup() {
  pinMode(ir_ledPin, OUTPUT);
  pinMode(buttonPin, INPUT);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {        
    digitalWrite(ir_ledPin, HIGH);  
  } 
  else {
    digitalWrite(ir_ledPin, LOW); 
  }

}
```
### for IchigoJam

## Connecting 2(#113 IR Reciver Brickを使用した動作確認)
A0 コネクタにIR LED Brick

A1 コネクタにIR Reciver Brick

A2 コネクタにLED Brick

A0からA2に上記のBrickを接続し,IR LED Brickから出る赤外線をIR Reciver Brickで受信できるかを確認します。LED Brickが光れば正常に動作しています。

![](/img/100_analog/112_ir_connect_2.jpg)

### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_analog_ir_led and brick_analog_ir_receive Operation check.
//

int ir_ledPin = A0;
int ir_receivePin = A1;
int ledPin = A2;

int irState = 0;

void setup() {
  pinMode(ir_ledPin, OUTPUT);
  pinMode(ir_receivePin, INPUT);
  pinMode(ledPin, OUTPUT);
}

void loop() {
  irState = digitalRead(ir_receivePin);
    digitalWrite(ir_ledPin, HIGH);
  if (irState == HIGH) {        
    digitalWrite(ledPin, HIGH);  
  } 
  else {
    digitalWrite(ledPin, LOW); 
  }

}
```



## Parts
- 赤外線LED
