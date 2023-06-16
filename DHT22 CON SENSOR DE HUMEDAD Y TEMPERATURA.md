# Practica ESP32 CON Ultrasonic  Distance Sensor ,Digital Humidity and Temperature sensor Y PANTALLA LED.
Este repositorio muestra como podemos programar una ESP32 con el sensor  y nos muestra  LA HUMEDAD Y LA TEMPERATURA y mandar los resultados A LA PANTALLA LED.


## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```DTH11```) para adquirir la distancia y mandar las señales con el encendido de luces  LED ; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- CON Ultrasonic  Distance Sensor 
- Digital Humidity and Temperature sensor 
- PANTALLA LED


## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h"


const int DHT_PIN = 15;
DHTesp dhtSensor;

const int Trigger = 13;   //Pin digital 2 para el Trigger del sensor
const int Echo = 12;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
Serial.begin(9600);//iniciailzamos la comunicación
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0


  // put your setup code here, to run once:
  Serial.begin(115200);
  Serial.println("Hello, ESP32!");
}

void loop()
{
  
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");
  delay(1500);

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

 lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  lcd.setCursor(0, 1);
  lcd.print("                 " );
  delay (1500);
  lcd.setCursor(0, 0);
  lcd.print("JAVIER  CORTES       ");

  delay(1000);
}

```
2. INTALAMOS LA LIBRERIA "LIBRARY MANAGER"


3. Hacer la conexion de **DHT11** a **Distance Sensor ,Digital Humidity and Temperature sensor**  y conectar  **LA PANTALLA LED** como se muestra en la siguente imagen.

![](https://github.com/javsCOR/SENSOR-HUMEDAD.TEMPERATURA/blob/main/IMAGEN%201.png?raw=true)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia dando *doble click* al sensor **DHT11** 
4. tambien  agregamos comandos diferentes a los resultados  **Distance Sensor ,Digital Humidity and Temperature sensor** COMO SE MUESTRA EN LA SIGUIENTE  IMAGEN 

![](https://github.com/javsCOR/SENSOR-HUMEDAD.TEMPERATURA/blob/main/IMAGEN%202%20EN%20ACCION.png?raw=true)


## Resultados

Cuando haya funcionado, verás COMO NOS MUESTRA LA HUMEDAD Y LA TEMPERATURA QUE NOS MANDAN ESTOS SENSORES EN LA PANTALLA LED   como se muestra en la siguente imagen.

![](hhttps://github.com/javsCOR/SENSOR-HUMEDAD.TEMPERATURA/blob/main/IMAGEN%202%20EN%20ACCION.png?raw=true)







# Créditos

creado por ING javier cortes rojas
