#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 27;   //Pin digital 3 para el Echo del sensor
#define LCD_COLUMNS 20
#define LCD_LINES   4

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);


void setup() {
   lcd.init();
  lcd.backlight();
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
}

void loop()
{

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
  delay(3000);          //Hacemos una pausa de 100ms

    lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) +"cm");
  lcd.setCursor (0,1);
  lcd.print("Migue");
  delay(3000);
 
 ## EN ESTA PRACTICA LO QUE SE REALIZO FUE REALIZAR LA CONEXIION PARA LOGRAR MANDAR A UNA LCD UN PARAMETROS QUE NOS MARCO UN SENSOR ULTRASONICO ASI COMO AGREGAMOS TAMBIEN PALABRAS
## LOS MATERIALES FUERON:

 ## -ESP32
 ## -DTH22 
 ## - PANTALLA LCD
## -SENSOR ULTRASONICO

![](https://github.com/Miguebt2707/Sensor-ultrasonico-con-LCD/blob/main/Captura%20de%20pantalla%202023-06-10%20091800.png?raw=true)

}