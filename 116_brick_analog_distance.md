# #116 Distance Brick

<center>![](/img/100_analog/product/116_distance_product.png)
<!--COLORME-->

GP2Y0A21YK

[http://www.sharpsma.com/webfm_send/1208](http://www.sharpsma.com/webfm_send/1208)


## Sample Code

### Arduino


```c
//
// FaBo Brick Sample
//
// brick_analog_distance
//

int distanceValue = 0;

void setup() {
   // シリアル開始 転送レート：9600bps
   Serial.begin(9600);
}

void loop() {
  // センサーより値を取得(0〜1023)
  distanceValue = analogRead(A0);
  
  // 取得した値を電圧に変換 (0〜5000mV)
  distanceValue = map(distanceValue, 0, 1023, 0, 5000);

  // 変換した電圧を3200(3.2v)〜500(0.5v)の値に変換後、温度に変換 (10〜80cm)
  distanceValue = map(distanceValue, 3200, 500, 5, 80);

  // 算出した温度を出力
  Serial.println(distanceValue);

  delay(100);
}

```