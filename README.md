# -ultrasonic-servo-arduino-

#include <Servo.h>

Servo myServo;        
int trigPin = 5;      
int echoPin = 6;      
int servoPin = 7;     

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);   
  pinMode(echoPin, INPUT);    
  myServo.attach(servoPin);   
  myServo.write(0);           
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  duration = pulseIn(echoPin, HIGH);
  
  distance = duration * 0.034 / 2;
  
  if (distance > 0 && distance <= 30) {
    myServo.write(90);  
    delay(3000);        
  } else {
    myServo.write(0);   
    delay(50);          
  }
}