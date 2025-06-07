# Practica-ESP32-con-sensor-DHT22-y-ultrasonico-LCD
Se mostrarán los valores de ambos sensores en el display con retardo de 2 segundos para cada sensor

## Introduccion

### Descripcion

La display nos mostrará los valores de temperatura y humedad relativa del entorno y el sensor ultrasonico monitorea la distancia o nivel de determinado obejto 

### Material necesario 

- WOKWI
- Tarjeta ESP32
- Sensor ultrasonico
- Sensor DHT22
- LCD 16x2 (I2C)

## Instrucciones

### Requsitos previos 

Para poder usar este repositorio deberás entrar a la plataforma WOKWI

https://wokwi.com/

### Instrucciones de preparacion de entorno 

1. Abrir la terminal de programación y colocar las siguientes líneas

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 18;   //Pin digital 3 para el Echo del sensor
const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
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
  lcd.setCursor(0, 0);
  lcd.print("Diplomado");
  lcd.setCursor(0, 1);
  lcd.print("Automatizacion");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Irving Cardoso");
  lcd.setCursor(0, 1);
  lcd.print("Ing Mecanica");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("  07/06/2025");
  delay (2000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (d)+"cm");
  delay(2000);          //Hacemos una pausa de 100ms
  lcd.clear(); 
}

```

2.Instalar las librerías DHT sensor library for ESPx y LiquidCrystal I2C como se muestra en la siguiente imagen

![image](https://github.com/user-attachments/assets/f48280f6-76bb-4aac-8bd7-de8a14478b06)

3.Hacer la conexión como se muestra en la siguiente imagen

![image](https://github.com/user-attachments/assets/42d21873-4e80-4edb-b20b-e7951cddbdd7)

## Instrucciones de operacion

1.Iniciar el simulador

2.Visualizar los datos en la LCD

3.Colocar la distancia o temperatura y humedad relativa dando doble click en el sensor ultrasonico o en el sensor DHT22 respectivamente

## Resultados

Cuando haya funcionado el display te mandará las siguientes imagenes en retardos de dos segundos

![image](https://github.com/user-attachments/assets/df5f7e14-379d-4538-a7c1-58b71b5cee92)

![image](https://github.com/user-attachments/assets/3742cbb6-aa00-4df2-b53b-03ba4202804e)

![image](https://github.com/user-attachments/assets/74777c1a-fdf6-4487-8f1f-a4ed56fda201)

![image](https://github.com/user-attachments/assets/7e75fc06-edc7-40ea-a31a-68f6f0c3c879)

![image](https://github.com/user-attachments/assets/ade855c6-b3fb-4d27-bd10-e354c64711d2)

## Créditos
Desarrollado por Irving Cardoso estudiante de Ingeniería Mecánica

https://github.com/IrvingM10/Practica-ESP32-con-sensor-DHT22-y-ultras-nico-LCD-/edit/main/README.md


