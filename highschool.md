# HighSchool

# 基礎トレーニング



# 最終課題

風車のサンプル


### for Arduino

```c

//
// FaBo Brick Sample
//
// brick_analog_button
//

#define buttonPin A0 // ボタンピン
#define ledPin A1    // LEDピン

// ボタンの押下状況取得用
int buttonState = 0;

void setup() {
  // ボタンピンを入力用に設定
  pinMode(buttonPin, INPUT); 
  // LEDピンを出力用に設定
  pinMode(ledPin, OUTPUT);  
  
  // DCモーター1
  pinMode(2, OUTPUT); // モーター1のピン1(前進用)
  pinMode(3, OUTPUT); // モーター1の出力設定用
  pinMode(4, OUTPUT); // モーター1のピン2(後退用)
}

void loop(){
  // ボタンの押下状況を取得
  buttonState = digitalRead(buttonPin);

  // ボタン押下判定
  if (buttonState == HIGH) {        
     // モーター1の設定(HIGH/LOW:前進)
    digitalWrite(2, HIGH); 
    digitalWrite(4, LOW);   
    analogWrite(3, 255); // 0-255 強さ  
  } 
  else {
     // モーター1の設定(LOW/HIGH:後進)
    digitalWrite(2, LOW); 
    digitalWrite(4, HIGH);   
    analogWrite(3, 255); // 0-255 強さ
  }
}
```

# 課題
Angle Brickをつかって回転の速度を調節してみよう