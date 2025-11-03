#include <Servo.h>
const int UD = A0;
int UDMin = 1023; 
int UDMax = 0;

const int LR = A1;
int LRMin = 1023;        
int LRMax = 0;

int SensorUDValue = 0;
int SensorLRValue = 0;

int ServoLPin = 9;
int ServoRPin = 10;

int UDValue;
int LRValue;
int MLRValue;
Servo ServoL;
Servo ServoR;
void setup() {
  Serial.begin(9600);
  pinMode(13, OUTPUT);
  digitalWrite(13, HIGH);
  pinMode(UD, INPUT);
  pinMode(LR,INPUT);

  ServoL.attach(ServoLPin);
  ServoR.attach(ServoRPin); 
  while (millis() < 5000) {
    SensorUDValue = analogRead(UD);
    SensorLRValue = analogRead(LR);

    // record the maximum sensor value
    if (SensorUDValue > UDMax) {
      UDMax = SensorUDValue;
    }
if (SensorLRValue > LRMax) {
      LRMax = SensorLRValue;
    }
    // record the minimum sensor value
    if (SensorUDValue < UDMin) {
      UDMin = SensorUDValue;
    }
    if (SensorLRValue < LRMin) {
      LRMin = SensorLRValue;
    }
  }
  // signal the end of the calibration period
  digitalWrite(13, LOW);
}
void loop() {
  SensorUDValue = analogRead(UD);
  SensorLRValue = analogRead(LR);
  SensorUDValue = constrain(SensorUDValue,UDMin,UDMax);
  SensorLRValue = constrain(SensorLRValue,LRMin,LRMax);
  UDValue = map(SensorUDValue,UDMin,UDMax,135,45);
  LRValue = map(SensorLRValue,LRMin,LRMax,135,45);
  MLRValue = map(LRValue,135,45,45,135);
   Serial.println("LR value");
  Serial.println(LRValue);
  Serial.println(MLRValue);
   Serial.println("UD value");
  Serial.println(UDValue);
   Serial.println("LR");
  Serial.println(LRMin);
  Serial.println(LRMax);
   Serial.println("UD");
  Serial.println(UDMin);
  Serial.println(UDMax);
if ((UDValue<85)||(UDValue>95))
  {
  ServoR.write(UDValue);
  ServoL.write(UDValue);
  delay(15);
  }
  else if(LRValue> 90) 
  {
  ServoR.write(LRValue);
  delay(15);
  ServoL.write(MLRValue);
  delay(15);
  }
  else {
  ServoR.write(MLRValue);
  delay(30);
  ServoL.write(LRValue);
  delay(30);
  }
}
