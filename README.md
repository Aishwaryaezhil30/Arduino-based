# Arduino-based
Lets integrate sensors with arduino>>>
1.Fire Detector using Flame Sensor and Arduino Interface:
  sensor used: YL-38

Wire Connections:

Connect the VCC pin of the flame sensor to the 5V output on the Arduino.
Connect the GND (ground) pin of the flame sensor to one of the Arduino's GND pins.
Connect the DO (Digital Output) pin of the flame sensor to a digital input pin on the Arduino (e.g., D2).

SOURCE CODE:

int led_pin = 13 ;// initializing the pin 9 as the led pin
 
int flame_sensor_pin = 8 ;// initializing pin 12 as the sensor output pin
int flame_pin = HIGH ; // state of sensor
 
void setup ( ) {
 
pinMode ( led_pin , OUTPUT ); // declaring led pin as output pin
pinMode ( flame_sensor_pin , INPUT ); // declaring sensor pin as input pin for Arduino
Serial.begin ( 9600 );// setting baud rate at 9600
}
 
void loop ( ) {
flame_pin = digitalRead ( flame_sensor_pin ) ; // reading from the sensor
if (flame_pin == LOW ) // applying condition
{
Serial.println ( " FLAME , FLAME , FLAME " ) ;
digitalWrite ( led_pin , HIGH ) ;// if state is high, then turn high the led
}
 
else
{
Serial.println ( " no flame " ) ;
digitalWrite ( led_pin , LOW ) ; // otherwise turn it low
}
}
-------------------------------------------------------------------------------------------------------------------------------------
2.Interface touch sensor with arduino:
  Sensor used: TTP223 Capacitive Touch Sensor

wire connections:
Sig Pin of TTP223  Touch Sensor ——————->Arduino Digital Pin D7
Vcc Pin of TTP223  Touch Sensor ——————->Arduino 5V
GND Pin of TTP223  Touch Sensor ——————-> Arduino GND
LED positive pin  -------—————————————–> Arduino Digital Pin D13
LED negative pin --------—————————————–>Arduino Ground Pin

SOURCE CODE:
#define ctsPin 7 // Pin for capactitive touch sensor
int ledPin = 13; // pin for the LED
void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);  
  pinMode(ctsPin, INPUT);
}
 
void loop() {
  int ctsValue = digitalRead(ctsPin);
  if (ctsValue == HIGH){
    digitalWrite(ledPin, HIGH);
    Serial.println("TOUCHED");
  }
  else{
    digitalWrite(ledPin,LOW);
    Serial.println("not touched");
  } 
  delay(500); 
}

-------------------------------------------------------------------------------------------------------------------------------------


3.Interfacing humidity sensor with Arduino:
  Sensor used: DHT11

wire connections:
VCC Pin of DHT11 Sensor Module-------> 3.3V pin of Arduino
GND Pin of DHT11 Sensor Module-------> GND pin of Arduino 
DHT11 Data pin ----------------------> Arduino Digital Pin 2.

SOURCE CODE:
#include "DHT.h"
#define DHTPIN 2     // Digital pin connected to the DHT sensor
#define DHTTYPE DHT11   // DHT 11
 
DHT dht(DHTPIN, DHTTYPE);
 
void setup() {
  Serial.begin(9600);
  dht.begin();
}
 
void loop()
{
  // Wait a few seconds between measurements.
  delay(2000);
 
  // Reading temperature or humidity takes about 250 milliseconds!
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  float h = dht.readHumidity();
  // Read temperature as Celsius (the default)
  float t = dht.readTemperature();
  // Read temperature as Fahrenheit (isFahrenheit = true)
  float f = dht.readTemperature(true);
 
  // Check if any reads failed and exit early (to try again).
  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println(F("Failed to read from DHT sensor!"));
    return;
  }
 
  // Compute heat index in Fahrenheit (the default)
  float hif = dht.computeHeatIndex(f, h);
  // Compute heat index in Celsius (isFahreheit = false)
  float hic = dht.computeHeatIndex(t, h, false);
 
  Serial.print(F("Humidity: "));
  Serial.print(h);
  Serial.print(F("%  Temperature: "));
  Serial.print(t);
  Serial.print(F("°C "));
  Serial.print(f);
  Serial.print(F("°F  Heat index: "));
  Serial.print(hic);
  Serial.print(F("°C "));
  Serial.print(hif);
  Serial.println(F("°F"));
}



