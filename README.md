#include "DHT.h"
#define DHTPIN A1 // pino do DHT
#define DHTTYPE DHT11 // DHT 11
DHT dht(DHTPIN, DHTTYPE);
int ledPin1 = 2;  
int ledPin2 = 3;  
int ledPin3 = 4;  
int ledPin4 = 5;  
char caracter;
// Gás
int pin_buzzer = 10;
int pin_d0 = 7;
int pin_a0 = A0;
int nivel_sensor = 400;

void setup() {
  Serial.begin(9600);
  dht.begin();
  pinMode(ledPin1,OUTPUT) ;  
  pinMode(ledPin2,OUTPUT) ;  
  pinMode(ledPin3,OUTPUT) ;  
  pinMode(ledPin4,OUTPUT) ;  
  //Gás
  pinMode(pin_d0, INPUT);
  pinMode(pin_a0, INPUT);
  pinMode(pin_buzzer, OUTPUT);
}

void loop() {
  //Gás
  int gas;
  int valor_digital = digitalRead(pin_d0);
  int valor_analogico = analogRead(pin_a0);
  if (valor_analogico > nivel_sensor)
  {
    digitalWrite(pin_buzzer, HIGH);
    gas = 1;
  }
  else
  {
    digitalWrite(pin_buzzer, LOW);
    gas = 0;
  }
  
  // --------

  int h = dht.readHumidity();
  int t = dht.readTemperature();
  Serial.print(t);
  Serial.print("|");
  Serial.print(h);
  Serial.print("|");
  Serial.print(gas);
  Serial.println("|");
   
    if(Serial.available()){
          caracter = Serial.read();
    }

    if(caracter == 'a'){
           digitalWrite(ledPin1,HIGH);  
   }
   
   if(caracter == 'b'){
      digitalWrite(ledPin2,HIGH);
   }
          
   if(caracter == 'c'){
     digitalWrite(ledPin3,HIGH);
   }
          
   if(caracter == 'd'){
    digitalWrite(ledPin4,HIGH);
   }
   
    if(caracter == '1'){
      digitalWrite(ledPin1,LOW);
    }
     
    if(caracter == '2'){
      digitalWrite(ledPin2,LOW);
    }
    
    if(caracter == '3'){
      digitalWrite(ledPin3,LOW);
    }
    
    if(caracter == '4'){
      digitalWrite(ledPin4,LOW);
    }
}
