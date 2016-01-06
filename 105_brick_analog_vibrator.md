# #105 Vibrator Brick

<center>![](/img/100_analog/product/105_vibrator_product.png)
<!--COLORME-->

振動モーターを使用したBrickです。
<br>
I/Oピンから振動モーターのON/OFFを制御することができます。

## Connecting
A1コネクタに接続したButtonブリックの入力により、A0コネクタに接続したVibratorブリックをON/OFFさせています。
![](/img/100_analog/connect/105_vibrator_connect.png)

## Support
| Arduino | RaspberryPI | IchigoJam |
| -- | -- | -- |
| <center>○ | <center>× | <center>x |

## Schematic
![](/img/100_analog/schematic/105_vibrator_schematic.png)

## Sample Code
### for Arduino
```c
//
// FaBo Brick Sample
//
// brick_analog_vibrator
//

#define buttonPin A1
#define vibratorPin A0

// ボタンの押下状況取得用
int buttonState = 0;

void setup() {
  // ボタンピンを入力用に設定
  pinMode(buttonPin, INPUT); 
  // バイブレーターピンを出力用に設定
  pinMode(vibratorPin, OUTPUT);         
}

void loop(){
 
  // ボタンの押下状況を取得
  buttonState = digitalRead(buttonPin);

  // ボタン押下判定
  if (buttonState == HIGH) {        
    // バイブレーターON
    digitalWrite(vibratorPin, HIGH);  
  } 
  else {
    // バイブレーターOFF
    digitalWrite(vibratorPin, LOW); 
  }
}
```

## Parts
- 振動モーター

