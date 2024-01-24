# NIVEL-DE-AGUA
PRACTICA 6
# PRACTICA-NIVEL-DE-AGUA
## Este repositorio muestra como podemos programar una ESP32 con el sensor HC-SR04 ULTRASONICO
# Descripción

## La Esp32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (HC-SR04) para adquirir el nivel del agua, tambien se utulizan LED's para avisar cuando el recipiente se encuentra vacio; Cabe aclarar que esta practica se usara un simulador llamado WOKWI.
# Material Necesario
## Para realizar esta practica necesitas lo siguiente

### WOKWI

Tarjeta ESP 32

Sensor HC-SR04

Luces LED

Resistor

Instrucciones

Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.


Instrucciones de preparación de entorno

![image](https://github.com/ErickRomeroRamos/NIVEL-DE-AGUA/assets/153964793/100c32be-ee67-4a47-b933-a7e26af8111c)

![image](https://github.com/ErickRomeroRamos/NIVEL-DE-AGUA/assets/153964793/4eb80cdf-77cc-4ef4-93c6-e8718da73490)

## CODIGO
// defines pins numbers
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 22;
const int led2 = 21;
const int led3 = 19;
const int led4 = 18;

// defines variables
long duration;
int distance;
int safetyDistance;


void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
}


void loop() {
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
if (safetyDistance>=10 && safetyDistance<=100)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}
else if(safetyDistance>=100 && safetyDistance<=200) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}
else if(safetyDistance>=200 && safetyDistance<=300) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
}
else if(safetyDistance>=300 && safetyDistance<=400) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
}
else
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay (2000);
}

