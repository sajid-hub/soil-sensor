# soil-sensor
#define SensorPin A0 
float sensorValue = 0; 
void setup() { 
 Serial.begin(9600); 
} 
void loop() { 
 for (int i = 0; i <= 100; i++) 
 { 
   sensorValue = sensorValue + analogRead(SensorPin); 
   delay(1); 
 } 
 sensorValue = sensorValue/100.0; 
 Serial.println(sensorValue); 
 delay(30); 
}
01:30
const int trigPin = 12;
const int echoPin = 11;
const int buzzer = 10;
const int ledPin = 13;
int pir = 9;
int buzz =8;
int state;
 
// defines variables
long duration;
int distance;
int safetyDistance;
 
 
void setup() {
  pinMode(pir, INPUT);
  pinMode(buzz, OUTPUT);
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(buzzer, OUTPUT);
pinMode(ledPin, OUTPUT);
Serial.begin(9600); // Starts the serial communication
}
 
 
void loop() {
  state = digitalRead(pir);
  digitalWrite(buzz, state);
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
 
// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
 
// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);
 
// Calculating the distance
distance= duration*0.034/2;
 
safetyDistance = distance;
if (safetyDistance <= 5){
  digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin, HIGH);
}
else{
  digitalWrite(buzzer, LOW);
  digitalWrite(ledPin, LOW);
}
 
// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
}
#include <LiquidCrystal.h>
const int rs = 7, en = 6, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int j=0;
int prev=0;
int pres=0;
void setup() 
{
  lcd.begin(16, 2);
  lcd.setCursor(0,0);
  lcd.print(" Soil Moisture  ");
  Serial.begin(9600);
}

void loop() 
{
  j=analogRead(A0);
  j=map(j,0,982,148,0);
  pres=j;
  if(j>100)
  j=100;
  else if(j<0)
  j=0;
  lcd.setCursor(6,1);
  lcd.print(j);
  lcd.print("%  ");
  Serial.println(j);

  prev=j;
  delay(500);
  
}
