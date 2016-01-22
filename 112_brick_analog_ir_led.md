# #112 IR LED Brick

<center>![](/img/100_analog/product/112_ir_product.jpg)
<!--COLORME-->

## Overview
赤外線LEDを使ったBrickです。

I/Oピンから赤外線LEDをON/OFFを制御することができます。

## Connecting
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


## Parts
- 赤外線LED
